# Data Flow — Socionics Dalam Diriku

**Versi:** 1.0.0  
**Tanggal:** 17 Juni 2026  
**Status:** CONTROLLED  
**Tahap asal:** 01 — Arsitektur teknis dan manifest proyek

## 1. Tujuan

Dokumen ini menetapkan perjalanan data peserta dari landing sampai ekspor dan berbagi. Fokusnya adalah ownership, transformasi, boundary, versioning, dan pemulihan. Dokumen ini tidak menetapkan isi pertanyaan, bobot evidence, formula scoring, atau nilai expected profile.

## 2. Prinsip aliran data

1. Data bergerak satu arah dari input peserta menuju immutable result snapshot.
2. Setiap transformasi menerima input eksplisit dan menghasilkan output baru.
3. Side effect hanya terjadi pada boundary UI, storage, Canvas, file, dan Web Share API.
4. Session state adalah sumber kebenaran alur tes; route bukan sumber kebenaran.
5. Scoring tidak membaca UI, storage, question bank, waktu, device, atau viewport.
6. Holdout terpisah dari pembentukan dan pemilihan bukti utama.
7. Card Studio mengonsumsi proyeksi hasil dan tidak dapat mengubah skor.
8. Data korelasi lintas sistem tidak memasuki aliran pengukuran.
9. Semua data peserta tetap lokal.

## 3. Aliran tingkat tinggi

```text
Landing
  -> Mode Selection
  -> Session Creation
  -> Question Selection
  -> Answer Capture
  -> Evidence Normalization
  -> Core Aggregation
  -> Candidate Comparison
  -> Tie-break Phase, bila diperlukan
  -> Primary Ranking Lock
  -> Holdout Evaluation
  -> Person-fit and Quality Summary
  -> Result Assembly
  -> Local Persistence
  -> Card Input Projection
  -> Local Photo Processing
  -> Deterministic Card Render
  -> Export / Share Fallback
```

## 4. Entitas data utama

### 4.1 `AssessmentModeConfig`

Mewakili kebijakan sesi, bukan teks UI. Memuat:

- mode ID;
- mode version;
- phase policy;
- item eligibility rules;
- minimum dan maximum item policy ketika kelak disetujui;
- holdout policy;
- tie-break eligibility policy;
- stop policy identifier.

Nilai kebijakan belum ditetapkan pada Tahap 01.

### 4.2 `SessionDescriptor`

Dibuat sekali saat sesi dimulai:

- session ID lokal;
- session seed;
- created timestamp;
- mode ID dan version;
- bank version;
- scoring version;
- candidate model version;
- session schema version;
- current phase;
- consent/acknowledgement flags yang diperlukan UI.

Timestamp tidak masuk scoring.

### 4.3 `PresentedItemRecord`

Mencatat apa yang benar-benar dilihat peserta:

- item ID;
- phase;
- display ordinal;
- option order;
- presentation revision;
- selection reason code;
- selection policy version.

Record ini diperlukan agar sesi dapat direproduksi meskipun bank lebih baru tersedia kemudian.

### 4.4 `AnswerRecord`

Mencatat jawaban secara normalized:

- item ID;
- selected option ID atau explicit skip state;
- answer revision;
- phase;
- answered timestamp untuk recovery saja;
- optional interaction quality metadata yang belum boleh memengaruhi scoring tanpa keputusan tersendiri.

Tidak menyimpan nama, alamat, email, lokasi, atau foto.

### 4.5 `EvidenceObservation`

Dibentuk dari item schema dan jawaban:

- source item ID;
- source option ID;
- phase;
- information element target;
- evidence channel target;
- signed evidence payload sesuai schema masa depan;
- provenance tier;
- reliability metadata;
- context metadata;
- exclusion flags.

Tahap 01 hanya menetapkan bentuk aliran. Besaran atau formula payload belum dibuat.

### 4.6 `ScoringSnapshot`

Output pure engine setelah sekumpulan observations:

- aggregate evidence map;
- support dan contradiction map per kandidat;
- ordered candidate comparison;
- unresolved candidate pairs;
- person-fit signals;
- quality flags;
- scoring warnings;
- input fingerprint;
- engine versions.

### 4.7 `PrimaryResultLock`

Record immutable yang dibuat sebelum holdout dinilai:

- candidate ordering utama;
- score components yang diizinkan;
- evidence fingerprint;
- tie-break phase record;
- lock timestamp untuk audit saja;
- lock version.

Holdout tidak dapat mengubah record ini pada arsitektur awal.

### 4.8 `HoldoutReport`

Mengevaluasi kecocokan data holdout terhadap result yang sudah dikunci:

- holdout item IDs;
- model prediction consistency;
- contradiction summary;
- missingness;
- quality limitations;
- report version.

Holdout report dapat memberi konteks terhadap ketahanan hasil, tetapi tidak menjadi jalur tersembunyi untuk mengubah ranking utama.

### 4.9 `ResultSnapshot`

Artefak hasil yang dapat disimpan dan direproduksi:

- primary candidate ranking;
- relative fit labels;
- evidence and contradiction summaries;
- holdout report;
- person-fit and response-quality summary;
- uncertainty and limitations;
- version identifiers;
- reproducibility record;
- scientific status text identifier;
- narrative input facets.

### 4.10 `CardInput`

Proyeksi read-only dari result:

- display name opsional yang dimasukkan peserta secara lokal;
- top result summary;
- limited supporting facets;
- uncertainty label;
- scientific disclaimer token;
- result fingerprint pendek;
- allowed card text fields.

Card input tidak memuat jawaban mentah, evidence map lengkap, atau photo bytes.

## 5. Flow detail per tahap

### 5.1 Landing

**Input**

- static application content;
- local preference record;
- optional resumable session metadata.

**Process**

- membaca preferensi dengan adapter storage;
- memeriksa apakah session checkpoint compatible;
- menampilkan pilihan mulai baru atau melanjutkan bila sah.

**Output**

- navigation intent;
- tidak ada scoring atau question data yang diproses.

**Failure rule**

Kerusakan preferensi tidak boleh memblokir landing. Preference record dapat diabaikan dengan default aman. Session record yang rusak dipindahkan ke quarantine metadata sebelum peserta diberi pilihan reset.

### 5.2 Pemilihan mode

**Input**

- available `AssessmentModeConfig` metadata;
- participant selection.

**Process**

- memvalidasi mode ID dan version;
- menjelaskan perbedaan durasi atau cakupan tanpa menjanjikan akurasi mutlak;
- tidak memuat hasil atau tipologi kandidat.

**Output**

- selected mode ID;
- event `SESSION_CREATE_REQUESTED`.

### 5.3 Pembuatan sesi

**Input**

- selected mode;
- current production version manifest;
- random seed dari browser crypto boundary.

**Pure process**

- membuat `SessionDescriptor`;
- menurunkan phase seed;
- membuat initial eligible pool;
- memastikan version compatibility.

**Side effect**

- menulis checkpoint awal melalui `SessionStorePort`.

**Output**

- state `core-active`;
- first item request.

### 5.4 Pemilihan item core

**Input**

- eligible core item IDs;
- already presented IDs;
- current scoring selection signal;
- session seed dan phase seed;
- selection policy version.

**Process**

- menyaring item tidak eligible;
- mengurutkan candidate items secara seeded dan stabil;
- menerapkan adaptive priority ketika policy mengizinkan;
- memilih satu item;
- mencatat reason code.

**Output**

- `PresentedItemRecord`;
- item view model untuk UI.

Selector tidak membaca candidate profile narratives, correlation data, storage, atau React state langsung.

### 5.5 Penangkapan jawaban

**Input**

- item ID yang sedang aktif;
- participant action;
- current answer revision.

**Process**

- memvalidasi option ID terhadap item yang dipresentasikan;
- membuat atau mengganti latest `AnswerRecord` secara immutable;
- mempertahankan revision metadata;
- menolak answer untuk item yang tidak pernah dipresentasikan.

**Side effect**

- checkpoint ditulis melalui storage port setelah state baru sah.

**Output**

- answer state yang tervalidasi;
- request untuk evidence normalization.

### 5.6 Evidence normalization

**Input**

- `AnswerRecord`;
- corresponding question contract;
- bank version.

**Pure process**

- mengubah selected option menjadi satu atau lebih `EvidenceObservation`;
- memvalidasi target element/channel;
- mempertahankan provenance dan source IDs;
- menandai excluded or missing response secara eksplisit.

**Output**

- normalized observations;
- no candidate result yet.

Pertanyaan tidak mengandung direct TIM label di UI, dan normalization tidak mengakses profile naratif.

### 5.7 Agregasi dan scoring snapshot

**Input**

- seluruh normalized core/tie-break observations yang eligible;
- candidate model version;
- scoring version.

**Pure process**

- membuat 8 × 8 evidence map;
- membangun support and contradiction traces;
- membandingkan seluruh 16 kandidat;
- menghasilkan total ordering stabil;
- menentukan unresolved pairs melalui policy yang kelak diformalkan;
- menghitung person-fit dan quality signals yang telah disetujui.

**Output**

- `ScoringSnapshot`;
- `SelectionSignal` ringkas untuk session/questions selector.

Scoring snapshot tidak disimpan otomatis oleh engine. Session memutuskan checkpoint.

### 5.8 Tie-break phase

**Entry condition**

- core policy selesai;
- unresolved pair atau ambiguity condition yang sah ditemukan;
- tie-break budget belum habis.

**Input**

- unresolved candidate pair identifiers;
- tie-break item registry;
- presented history;
- tie-break seed.

**Process**

- selector memilih item yang telah dideklarasikan untuk distinction target;
- item tetap melalui answer capture dan normalization yang sama;
- tie-break observations diberi phase tag agar dapat diaudit terpisah.

**Exit condition**

- pair resolved menurut policy;
- budget selesai;
- tidak ada eligible item;
- participant chooses supported exit path.

Tidak ada tie-break item yang boleh masuk pool core secara diam-diam.

### 5.9 Primary ranking lock

Setelah core dan tie-break selesai:

1. scoring dijalankan atas evidence yang diizinkan;
2. input fingerprint dibuat;
3. ranking utama dikunci;
4. lock record disimpan dalam session state;
5. holdout phase baru boleh dimulai.

Setelah lock, holdout observations tidak dapat ditambahkan ke primary aggregation collection.

### 5.10 Holdout phase

**Input**

- holdout registry;
- fixed primary result lock;
- holdout seed;
- holdout phase policy.

**Process**

- mempresentasikan holdout tanpa menggunakan performance holdout sebelumnya untuk memilih model yang lebih disukai;
- menormalisasi jawaban ke holdout-only observations;
- mengevaluasi konsistensi terhadap kandidat yang sudah dikunci;
- menghasilkan `HoldoutReport`.

**Output**

- quality/generalization context;
- tidak ada mutasi primary ranking.

Jika aturan holdout berubah pada masa depan, diperlukan keputusan baru, migration, dan leakage tests.

### 5.11 Person-fit dan response quality

Person-fit menerima pola respons dan metadata yang diizinkan. Ia menghasilkan signal, bukan diagnosis peserta. Signal dapat mencakup indikasi data terlalu tipis, terlalu seragam, terlalu kontradiktif, atau terlalu banyak skip, tetapi label final dan threshold belum ditetapkan pada Tahap 01.

Aturan wajib:

- tidak menyebut peserta malas, bohong, manipulatif, atau tidak stabil;
- tidak memakai device, lokasi, atau identitas;
- tidak menyembunyikan hasil tanpa alasan yang dapat dijelaskan;
- tidak meningkatkan confidence hanya karena banyak jawaban tersedia bila fit buruk.

### 5.12 Result assembly

**Input**

- primary result lock;
- holdout report;
- person-fit summary;
- profile narrative data;
- scientific limitation identifiers;
- all versions.

**Process**

- membangun immutable `ResultSnapshot`;
- membentuk participant-facing view model;
- memilih narasi berdasarkan evidence facets tanpa cross-system conversion;
- menghubungkan statements ke provenance tags internal.

**Output**

- result route data;
- optional persistable result record;
- card input projection source.

### 5.13 Penyimpanan hasil

Peserta dapat melihat hasil tanpa mewajibkan persistensi jangka panjang.

**Default behavior**

- checkpoint sesi disimpan agar dapat resume;
- result snapshot dapat disimpan lokal sesuai product decision pada gate UI;
- clear result dan clear all data harus tersedia;
- foto tetap memory-only secara default.

**Version mismatch**

- record compatible: migrate pure lalu validate;
- record unknown newer version: jangan downgrade diam-diam;
- record corrupt: quarantine metadata dan tawarkan reset;
- storage unavailable: lanjut memory-only bila aman.

### 5.14 Card Studio

**Input**

- `CardInput` immutable;
- local image file optional;
- selected template ID;
- explicit output format;
- crop and theme settings.

**Local process**

- decode image;
- validate file type and practical size;
- crop/rotate in browser;
- render using explicit `RenderSpec`;
- produce Blob/File.

Foto tidak pernah menjadi input scoring atau result narrative.

### 5.15 Ekspor dan berbagi

Urutan kemampuan:

1. hasil render menghasilkan Blob/File;
2. bila Web Share API mendukung file dan user gesture sah, gunakan share;
3. bila tidak, gunakan download lokal;
4. bila file export gagal tetapi text share tersedia, tawarkan text fallback yang tidak memuat jawaban mentah;
5. failure tidak mengubah result atau card draft.

## 6. Read/write ownership matrix

| Data | Pemilik utama | Pembaca | Penulis yang diizinkan |
|---|---|---|---|
| Domain constants | domain | seluruh modul melalui public API | domain build-time source |
| Question registry | questions | session, audit | questions data modules |
| Answer state | session | scoring melalui normalized input, UI | session reducer |
| Evidence observations | normalization boundary | scoring, audit | pure normalization function |
| Candidate models | scoring | scoring, audit | scoring data modules pada Gate 6 |
| Profile narratives | profiles | result, audit | profiles data modules pada Gate 8 |
| Session checkpoint | storage adapter | session composition | storage adapter atas request session |
| Result snapshot | result/session | UI, card projection, storage | result builder |
| Card draft | card | Card Studio UI, optional storage | card controller |
| Photo bytes | card boundary | local photo processor | user file selection only |

## 7. Data yang dilarang memasuki scoring

- participant name;
- foto;
- device model;
- browser name;
- lokasi;
- IP address;
- viewport size;
- route history;
- theme preference;
- share behavior;
- card customization;
- cross-system types;
- profession stereotype;
- celebrity resemblance;
- timestamps selain bila kelak ada quality policy yang disetujui secara eksplisit;
- UI wording variants.

## 8. Version compatibility

Satu hasil hanya dapat direproduksi bila versi berikut tersimpan:

- question bank;
- assessment mode;
- selection policy;
- scoring engine;
- candidate models;
- person-fit policy;
- holdout policy;
- result schema;
- session schema;
- storage schema.

Perubahan yang mengubah meaning memerlukan version bump. Result lama tidak boleh dihitung ulang dengan versi baru lalu ditampilkan seolah sama.

## 9. Data retention dan reset

Arsitektur menyediakan tiga tingkat penghapusan:

1. **Reset sesi aktif** — menghapus checkpoint sesi, mempertahankan preferensi.
2. **Hapus hasil tersimpan** — menghapus result snapshot dan card draft.
3. **Hapus seluruh data lokal** — menghapus semua namespace produk termasuk IndexedDB opt-in.

Penghapusan harus lokal, terkonfirmasi, dan tidak memerlukan jaringan.

## 10. Invariant aliran data

- Answer hanya sah untuk item yang telah dipresentasikan.
- Item ID unik di seluruh core, holdout, dan tie-break.
- Phase membership tidak dapat berubah setelah bank version dirilis.
- Core aggregation tidak menerima holdout observation.
- Primary ranking dikunci sebelum holdout evaluation.
- Holdout report tidak menulis primary score.
- Card input tidak memuat raw answers.
- Foto tidak masuk result snapshot.
- Storage failure tidak boleh menghasilkan skor berbeda dari memory-only execution.
- Seed dan input yang sama menghasilkan urutan serta hasil yang sama.
- UI tidak dapat langsung memutasi storage atau scoring internals.
