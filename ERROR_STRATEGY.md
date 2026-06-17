# Error Strategy — Socionics Dalam Diriku

**Versi:** 1.0.0  
**Tanggal:** 17 Juni 2026  
**Status:** CONTROLLED  
**Tahap asal:** 01 — Arsitektur teknis dan manifest proyek

## 1. Tujuan

Strategi ini memastikan kegagalan tidak berubah menjadi hasil yang menyesatkan, kehilangan data diam-diam, atau kebocoran informasi peserta. Error handling harus membedakan kegagalan yang dapat dipulihkan, pelanggaran invariant, corruption storage, kegagalan browser API, dan kegagalan rendering.

## 2. Prinsip utama

1. Expected failure dikembalikan sebagai typed result, bukan dilempar sebagai exception umum.
2. Unexpected failure ditangkap pada boundary terdekat yang mampu memulihkan atau menghentikan proses dengan aman.
3. Scoring tidak boleh menghasilkan fallback score ketika input invalid.
4. Storage failure tidak boleh mengubah hasil perhitungan.
5. Error UI tidak boleh menyalahkan peserta.
6. Jawaban dan foto tidak ditulis ke log diagnostik.
7. Error code stabil; pesan UI dapat berubah tanpa mengubah identitas error.
8. Recovery harus eksplisit: retry, kembali, lanjut memory-only, reset record, atau berhenti.
9. Fatal error pada satu route tidak boleh merusak data route lain yang masih valid.
10. Tidak ada telemetry jaringan atau error reporting eksternal.

## 3. Kategori kegagalan

### 3.1 Validation failure

Terjadi ketika data tidak memenuhi schema atau invariant yang diketahui.

Contoh kategori:

- question ID ganda;
- option tidak terdaftar;
- phase membership salah;
- candidate model tidak lengkap;
- version identifier kosong;
- card render dimensions tidak valid.

Handling:

- development/test/build: fail fast;
- production: blokir jalur yang dapat menghasilkan output salah;
- simpan detail teknis hanya di memory/dev console yang telah direduksi;
- tampilkan recovery aman atau minta memulai ulang bagian yang terpengaruh.

### 3.2 Domain invariant failure

Terjadi ketika state yang seharusnya mustahil terbentuk.

Handling:

- hentikan operasi terkait;
- jangan memperbaiki data dengan tebakan;
- pertahankan checkpoint terakhir yang telah tervalidasi;
- tandai error sebagai non-recoverable untuk operasi tersebut;
- arahkan peserta kembali ke state aman.

### 3.3 Storage failure

Mencakup:

- quota exceeded;
- localStorage diblokir;
- IndexedDB tidak tersedia;
- record corrupt;
- migration gagal;
- write interrupted;
- version lebih baru daripada aplikasi.

Handling:

- read preference gagal: gunakan default;
- write checkpoint gagal: lanjut memory-only setelah memberi tahu risiko resume;
- corrupt record: jangan overwrite record asal sebelum quarantine metadata dibuat;
- migration gagal: pertahankan raw record, jangan menghasilkan session parsial;
- unknown newer version: blokir resume, izinkan mulai sesi baru tanpa menghapus record kecuali peserta memilih;
- foto gagal disimpan: pertahankan draft memory-only.

### 3.4 Scoring failure

Mencakup input tidak lengkap, candidate model invalid, numeric non-finite, illegal phase contamination, atau version mismatch.

Handling:

- jangan tampilkan hasil ranking;
- jangan mengganti dengan hasil default atau random;
- simpan session checkpoint yang valid;
- izinkan retry setelah module reload;
- bila tetap gagal, tawarkan kembali ke sesi atau reset yang terkontrol;
- error detail tidak boleh menampilkan answer content.

### 3.5 Chunk loading failure

Dapat terjadi saat route atau engine lazy chunk gagal dimuat.

Handling:

- tampilkan route-level recovery UI;
- sediakan retry yang benar-benar mengulang import;
- jangan menandai phase selesai;
- pertahankan checkpoint;
- bila versi deployment berubah di tengah sesi, minta reload dan lakukan compatibility check setelah reload.

### 3.6 Photo processing failure

Mencakup file tidak didukung, decode gagal, dimensi ekstrem, kehabisan memory, atau Canvas gagal.

Handling:

- tolak hanya foto, bukan hasil;
- pertahankan Card Studio tanpa foto;
- bersihkan Object URL yang gagal;
- jelaskan tindakan yang dapat dilakukan tanpa istilah teknis berlebihan;
- jangan mengunggah file untuk mencoba pemulihan.

### 3.7 Card render/export failure

Mencakup font belum siap, layout overflow, Canvas tainted, Blob creation gagal, atau browser tidak mendukung format.

Handling:

- renderer mengembalikan typed failure;
- Card Studio tetap terbuka;
- participant settings tidak hilang;
- izinkan retry setelah font ready atau ukuran foto dikurangi;
- sediakan format/fallback lain bila aman;
- jangan mengubah result snapshot.

### 3.8 Share failure

Mencakup API tidak tersedia, user cancellation, permission denial, file share tidak didukung, atau share promise gagal.

Handling:

- user cancellation tidak diperlakukan sebagai error merah;
- permission/API failure menawarkan download;
- bila file gagal, text fallback dapat ditawarkan;
- share state tidak masuk scoring atau person-fit.

### 3.9 UI render failure

React render error ditangani oleh boundary bertingkat:

- root boundary untuk kegagalan app shell;
- route boundary untuk assessment, result, dan Card Studio;
- component-level recovery hanya untuk area yang independen seperti photo editor.

Root boundary tidak boleh menghapus storage secara otomatis.

## 4. Error code taxonomy

Error code memakai format `AREA_REASON`.

| Prefix | Area | Contoh maksud |
|---|---|---|
| `CFG_` | Configuration | version manifest atau mode config invalid |
| `DOM_` | Domain | invariant internal dilanggar |
| `QST_` | Questions | bank, item, option, atau registry invalid |
| `SES_` | Session | illegal transition atau answer state invalid |
| `STO_` | Storage | read, write, migration, quota, corruption |
| `SCR_` | Scoring | invalid input, contamination, non-finite output |
| `HLD_` | Holdout | leakage atau primary lock missing |
| `FIT_` | Person-fit | policy/input mismatch |
| `RES_` | Result | result assembly atau version mismatch |
| `CRD_` | Card | schema, layout, render, or template failure |
| `PHT_` | Photo | decode, crop, memory, unsupported input |
| `EXP_` | Export | Blob/File/download failure |
| `SHR_` | Share | capability, permission, cancellation, promise failure |
| `CHK_` | Chunk | dynamic import atau deployment version conflict |
| `UI_` | UI | render boundary atau accessibility state failure |

Error code tidak berisi TIM, answer ID, option text, nama peserta, atau nama file foto.

## 5. Typed error envelope

Kontrak konseptual:

```text
code
kind
severity
recoverability
safeContext
causeCategory
userActionIds
retryToken optional
```

`safeContext` hanya memuat metadata non-sensitif seperti schema version, module ID, item count, atau phase. Raw answers dan image metadata pribadi tidak masuk envelope.

## 6. Severity dan recoverability

| Severity | Makna | Contoh tindakan |
|---|---|---|
| info | Bukan kegagalan; capability fallback | gunakan download karena file share tidak tersedia |
| warning | Operasi utama dapat lanjut dengan keterbatasan | storage tidak tersedia, lanjut memory-only |
| error | Operasi saat ini gagal, data valid masih tersedia | retry scoring/chunk/export |
| fatal | State tidak dapat dipercaya untuk jalur tersebut | hentikan sesi atau result assembly, kembali ke checkpoint aman |

Recoverability:

- `retryable`;
- `fallback-available`;
- `requires-reset-resource`;
- `requires-new-session`;
- `non-recoverable-current-version`.

## 7. Boundary map

| Boundary | Menangkap | Tidak boleh dilakukan |
|---|---|---|
| Build/audit | invalid static data, cycles, missing files | membiarkan build lulus dengan warning |
| Domain public API | invalid arguments dan invariant | membaca UI/storage untuk memperbaiki input |
| Session controller | illegal transition, selection/scoring failure | membuat result default |
| Storage adapter | browser exception, quota, migration | menghapus record tanpa tindakan eksplisit |
| Route boundary | lazy chunk/render failure | mereset seluruh app otomatis |
| Card/photo boundary | file, Canvas, export/share failure | mengubah scoring/result |
| Root boundary | unexpected app-shell failure | menampilkan stack atau answer data |

## 8. Recovery matrix per alur

| Titik | Recovery pertama | Recovery kedua | Stop condition |
|---|---|---|---|
| Landing preference read | default preference | clear preference record | app shell tetap jalan |
| Resume session | migrate + validate | mulai sesi baru | jangan resume data invalid |
| Question chunk | retry import | reload app | tidak menampilkan item parsial |
| Answer write | retry checkpoint | memory-only | beri peringatan resume tidak tersedia |
| Scoring | retry pure calculation | reload compatible engine | jangan tampilkan ranking palsu |
| Result profile chunk | retry | tampilkan result factual minimum tanpa narasi hanya bila contract mengizinkan | jangan mengganti tipe |
| Photo decode | pilih file lain | lanjut tanpa foto | result tetap tersedia |
| Card render | retry explicit spec | format lain | result tetap tersedia |
| Share | retry user gesture | download/text fallback | cancellation tidak dianggap fatal |

## 9. Atomicity dan checkpoint

Session reducer menghasilkan state baru lebih dahulu. Storage write terjadi setelah state tervalidasi. Bila write gagal:

- in-memory state tetap menjadi sumber kebenaran selama tab aktif;
- persisted state terakhir tidak ditandai sebagai terbaru;
- UI memberi tahu bahwa resume mungkin tidak tersedia;
- scoring tetap memakai state memory yang tervalidasi;
- aplikasi tidak melakukan rollback jawaban peserta tanpa pemberitahuan.

Result persistence menggunakan write-then-verify bila adapter mendukung. Record lama baru diganti setelah record baru lolos validation.

## 10. Migration failure policy

Migration harus:

1. membaca salinan record;
2. memeriksa source version;
3. menerapkan langkah pure satu per satu;
4. memvalidasi target;
5. menulis target baru;
6. mempertahankan record asal sampai target terverifikasi.

Tidak ada best-effort field guessing. Field wajib yang hilang menyebabkan migration failure yang jujur.

## 11. User-facing language

Pesan error harus:

- menjelaskan apa yang gagal pada level tindakan;
- menyatakan apakah jawaban atau hasil masih aman;
- memberi satu tindakan utama yang jelas;
- tidak menyebut peserta ceroboh, tidak konsisten, atau salah;
- tidak menjanjikan data tersimpan bila write gagal;
- tidak menampilkan stack trace atau internal candidate values.

Dokumen ini tidak menetapkan kalimat UI final.

## 12. Logging policy

### Production

- tidak ada remote logging;
- console logging minimum;
- error detail direduksi;
- answer content, name, image bytes, image filename, dan card text personal tidak dicatat;
- debug mode tidak tersedia melalui query string publik.

### Development/test

- structured diagnostic boleh memuat error code, module, version, count, dan invariant name;
- fixtures sintetis boleh muncul;
- production participant data tetap tidak dicetak secara default.

## 13. Error testing requirements

Minimal test classes:

- setiap typed error branch;
- corrupted storage records;
- quota denial;
- unsupported/newer version;
- illegal session transition;
- answer to unpresented item;
- holdout contamination attempt;
- scoring non-finite guard;
- dynamic import rejection;
- photo decode rejection;
- Canvas/Blob/share API failure;
- user share cancellation;
- error boundary preserves checkpoint;
- reset action only deletes intended namespace.

## 14. Acceptance criteria

- tidak ada catch block yang mengabaikan error tanpa alasan;
- fatal scoring failure tidak menghasilkan result;
- storage failure memiliki memory-only path bila aman;
- recovery tidak menghapus data otomatis;
- error code tidak membocorkan jawaban atau foto;
- route chunk failure dapat di-retry;
- Card Studio failure tidak memengaruhi result;
- expected failure tidak bergantung pada parsing message string;
- semua recovery branch dapat diuji tanpa jaringan.
