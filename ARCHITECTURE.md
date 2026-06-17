# Architecture — Socionics Dalam Diriku

**Versi:** 1.0.0  
**Tanggal:** 17 Juni 2026  
**Status:** CONTROLLED  
**Tahap asal:** 01 — Arsitektur teknis dan manifest proyek

## 1. Tujuan dokumen

Dokumen ini menetapkan bentuk teknis final aplikasi sebelum bootstrap kode, bank pertanyaan, expected profile, atau scoring dibuat. Arsitektur harus cukup rinci untuk mencegah drift, siklus dependency, pencampuran data dengan UI, kebocoran holdout, dan ketergantungan Card Studio terhadap scoring.

Dokumen ini tunduk pada:

1. `docs/PROJECT_CONSTITUTION.md`;
2. `docs/MEASUREMENT_PRINCIPLES.md`;
3. keputusan terkunci di `docs/DECISIONS.md`;
4. `docs/REFERENCE_MATRIX.md`;
5. `docs/WORKFLOW.md`.

Bila implementasi kelak membutuhkan perubahan arah dependency atau kepemilikan data, perubahan harus dicatat sebagai keputusan baru sebelum kode diubah.

## 2. Ruang lingkup dan non-scope Tahap 01

### Dicakup

- arsitektur static single-page application;
- aliran data dari landing sampai berbagi kartu;
- batas modul dan arah dependency;
- struktur proyek final;
- kontrak bentuk data tingkat tinggi;
- strategi storage, determinisme, error handling, testing, dan code splitting;
- kapasitas untuk 192 core items, 32 holdout items, 32 tie-break items, 16 TIM, matriks 64 kanal per kandidat, adaptive selection, person-fit, evidence map, serta Card Studio multi-format.

### Tidak dicakup

- teks pertanyaan atau opsi jawaban;
- bobot, prior, likelihood, threshold, atau formula scoring final;
- isi expected profile 16 TIM;
- isi profil naratif 16 TIM;
- implementasi Card Studio;
- bootstrap React, TypeScript, Vite, atau package dependencies.

## 3. Gaya arsitektur

Aplikasi menggunakan **modular monolith browser-only** dengan empat lapisan utama:

1. **Pure domain core** — kontrak, identifier, invariant, dan tipe yang tidak bergantung pada React, DOM, browser storage, atau file data produksi.
2. **Pure application modules** — questions, scoring, profiles, result, serta session logic yang menerima data melalui parameter dan mengembalikan nilai tanpa side effect tersembunyi.
3. **Infrastructure adapters** — localStorage, IndexedDB opsional, Canvas, file export, dan Web Share API.
4. **Presentation and composition** — React UI, router, providers, lazy routes, serta wiring adapter ke port.

Tidak ada backend, database online, API key, autentikasi, serverless API, pengunggahan jawaban, atau pengunggahan foto.

## 4. Quality attributes yang menjadi prioritas

Urutan prioritas arsitektur:

1. **Correctness** — invariant domain dan pemisahan holdout tidak boleh bergantung pada kebiasaan developer.
2. **Reproducibility** — seed, versi bank, versi scoring, dan input yang sama menghasilkan output yang sama.
3. **Privacy** — seluruh data peserta tetap lokal dan dapat dihapus.
4. **Auditability** — sumber evidence, versi, transformasi, serta keputusan sesi dapat ditelusuri.
5. **Maintainability** — tiap modul memiliki public API dan satu alasan perubahan.
6. **Accessibility** — UI dan pemulihan error tidak mengunci keyboard atau screen reader.
7. **Performance** — beban route, bank data, profil, dan Card Studio dipisahkan.
8. **Portability** — build berupa aset statis dan tidak memerlukan server aplikasi.

## 5. Batas modul

### 5.1 `domain`

**Tanggung jawab**

- identifier dan union type stabil;
- delapan information elements;
- delapan evidence channels;
- posisi dan blok Model A;
- 16 TIM sebagai identifier, bukan isi profil;
- versi schema dan data;
- bentuk evidence observation, candidate comparison input/output, person-fit signal, holdout report, dan deterministic random source;
- invariant yang bebas dari UI dan storage.

**Boleh mengimpor:** file lain di dalam `domain`.  
**Dilarang mengimpor:** React, browser API, questions, scoring, profiles, session, storage, UI, result, card, audit, atau tests.

### 5.2 `questions`

**Tanggung jawab**

- schema question item, option, answer, bank, phase, dan selection policy;
- registry untuk core, holdout, dan tie-break;
- validator bank;
- seeded ordering;
- adaptive item selection berdasarkan signal abstrak;
- pemisahan fisik dan logis tiga kelompok item.

**Boleh mengimpor:** `domain`.  
**Dilarang mengimpor:** komponen React, storage adapter, profile narratives, card, atau concrete scoring implementation.

Data pertanyaan tidak boleh mengimpor komponen.

### 5.3 `scoring`

**Tanggung jawab**

- agregasi evidence;
- evidence map;
- perbandingan 16 candidate models;
- person-fit evaluation;
- evaluasi holdout terhadap model yang sudah dikunci;
- confidence derivation ketika formula telah disetujui pada gate terkait;
- public result yang immutable.

**Boleh mengimpor:** `domain`.  
**Dilarang mengimpor:** React, DOM, storage, router, card, UI, profile narrative, dan question data konkret.

Scoring menerima normalized observations, bukan membaca bank atau storage sendiri. Semua fungsi inti harus pure.

### 5.4 `profiles`

**Tanggung jawab**

- metadata dan narasi manusiawi untuk 16 TIM;
- provenance narasi;
- variasi paragraf berdasarkan result facets;
- larangan korelasi lintas sistem masuk ke narasi.

**Boleh mengimpor:** `domain`.  
**Dilarang mengimpor:** scoring implementation, question bank, storage, card renderer, atau UI components.

`profiles` tidak menentukan skor. Ia hanya menerjemahkan result contract yang sudah terbentuk.

### 5.5 `session`

**Tanggung jawab**

- state machine sesi;
- orchestration landing-to-result;
- pencatatan jawaban;
- pemilihan phase;
- pemanggilan questions selector dan scoring facade;
- checkpoint request melalui storage port;
- resume, pause, reset, dan finalize;
- pembentukan reproducibility record.

**Boleh mengimpor:** `domain`, public API `questions`, public API `scoring`, serta port milik `session`.  
**Dilarang mengimpor:** concrete storage adapter, React components, card renderer, atau profile data.

`session` adalah application coordinator, bukan tempat formula scoring atau rendering UI.

### 5.6 `storage`

**Tanggung jawab**

- implementasi port persistence;
- versioned envelope;
- migration;
- corruption quarantine;
- localStorage untuk data kecil;
- IndexedDB opsional untuk card draft atau foto bila peserta memilih menyimpan;
- clear/reset dan data inventory.

**Boleh mengimpor:** `domain`, port dan contract publik `session`, serta contract card draft yang stabil.  
**Dilarang mengimpor:** React routes, scoring implementation, atau question data.

`session` tidak bergantung pada `storage`; composition root menyuntikkan adapter storage ke port session.

### 5.7 `result`

**Tanggung jawab**

- membentuk result snapshot dari scoring output;
- menambahkan batas ilmiah dan metadata versi;
- membangun view model peserta;
- memproyeksikan result menjadi input Card Studio.

**Boleh mengimpor:** `domain`, public data `profiles`.  
**Dilarang mengimpor:** question data, storage adapter, React component, dan card renderer.

### 5.8 `card`

**Tanggung jawab**

- card schema;
- format portrait, square, dan story;
- pengolahan foto lokal;
- renderer berbasis ukuran eksplisit;
- export PNG;
- Web Share API dan fallback download/copy.

**Boleh mengimpor:** `domain` dan read-only result/card input contract.  
**Dilarang mengimpor:** scoring, questions, session state internal, atau viewport-derived layout.

Card renderer menerima `width`, `height`, `pixelRatio`, theme, crop, font state, dan content sebagai input eksplisit. Ia tidak membaca `window.innerWidth`, CSS viewport unit, atau ukuran elemen halaman untuk menentukan hasil akhir.

### 5.9 `ui`

**Tanggung jawab**

- route views;
- reusable accessible components;
- form controls;
- progress presentation;
- user-facing error recovery;
- hooks yang menghubungkan controller dengan React.

**Boleh mengimpor:** public API `domain`, `session`, `result`, `card`, dan adapter yang sudah diwiring oleh `app`.  
**Dilarang mengimpor:** internal files modul lain atau production test fixtures.

### 5.10 `audit`

**Tanggung jawab**

- dependency boundary checks;
- question coverage dan leakage audits;
- candidate model completeness checks;
- narrative provenance checks;
- build-time reports.

**Boleh mengimpor:** public data dan registry dari modul yang diaudit.  
**Dilarang diimpor oleh:** seluruh production runtime.

Audit dapat berjalan saat test atau build verification, tetapi tidak menjadi bagian bundle peserta kecuali laporan statis yang sengaja ditampilkan.

### 5.11 `tests`

**Tanggung jawab**

- fixtures sintetis;
- unit, contract, integration, component, dan regression tests;
- test vectors deterministik.

Production source tidak boleh mengimpor `tests` atau fixtures.

## 6. Dependency graph

Arah panah berarti modul di kiri boleh mengimpor modul di kanan.

```text
app      -> ui, session, storage, result, card, domain
ui       -> session, result, card, domain
session  -> questions, scoring, domain
storage  -> session/ports, domain, card/contracts
result   -> profiles, domain
card     -> result/contracts, domain
questions-> domain
scoring  -> domain
profiles -> domain
audit    -> domain, questions, scoring, profiles, session, storage, result, card

tests    -> seluruh public API produksi dan audit
```

Production modules tidak boleh mengimpor `audit` atau `tests`.

### 6.1 Bukti tidak ada siklus pada rancangan

Urutan topologis yang sah:

```text
domain
questions, scoring, profiles
session, result
card
storage
ui
app
audit
tests
```

`storage` berada setelah `session` hanya karena mengimplementasikan `session/ports`; `session` tidak mengimpor `storage`. `card` boleh membaca `result/contracts`, sedangkan `result` tidak mengimpor `card`. Karena itu kedua hubungan tersebut tetap satu arah.

## 7. Public API dan aturan import

Setiap modul produksi mempunyai `public.ts` atau index publik yang sempit. Cross-module import hanya melalui public API, kecuali contract path yang secara eksplisit dinyatakan stabil.

Contoh aturan:

```text
Boleh:     import { createSession } from "@/session/public";
Dilarang:  import { reduceInternalStep } from "@/session/state/sessionReducer";
```

Bootstrap kelak harus menambahkan alias path dan lint restriction agar aturan tidak hanya dokumentatif.

## 8. Struktur proyek target

Struktur berikut adalah target final. File data batch dan profil baru dibuat pada gate yang memilikinya; keberadaannya di dokumen ini bukan izin untuk mengisinya pada Tahap 01.

```text
socionics-dalam-diriku/
├─ package.json
├─ package-lock.json
├─ index.html
├─ vite.config.ts
├─ vitest.config.ts
├─ tsconfig.json
├─ tsconfig.app.json
├─ tsconfig.node.json
├─ eslint.config.js
├─ vercel.json
├─ .gitignore
├─ README.md
├─ public/
│  ├─ manifest.webmanifest
│  ├─ favicon.svg
│  └─ icons/
│     ├─ icon-192.png
│     └─ icon-512.png
├─ docs/
│  └─ ...dokumen governance dan arsitektur...
├─ src/
│  ├─ main.tsx
│  ├─ app/
│  │  ├─ App.tsx
│  │  ├─ router.tsx
│  │  ├─ routes.ts
│  │  ├─ providers/AppProviders.tsx
│  │  └─ errors/RootErrorBoundary.tsx
│  ├─ domain/
│  │  ├─ ids.ts
│  │  ├─ versions.ts
│  │  ├─ deterministic/
│  │  │  ├─ randomSource.ts
│  │  │  ├─ seededRandom.ts
│  │  │  └─ stableSort.ts
│  │  ├─ socionics/
│  │  │  ├─ informationElements.ts
│  │  │  ├─ evidenceChannels.ts
│  │  │  ├─ modelAPositions.ts
│  │  │  ├─ modelABlocks.ts
│  │  │  ├─ quadras.ts
│  │  │  └─ tims.ts
│  │  ├─ measurement/
│  │  │  ├─ evidence.ts
│  │  │  ├─ candidateModel.ts
│  │  │  ├─ personFit.ts
│  │  │  ├─ holdout.ts
│  │  │  └─ resultSnapshot.ts
│  │  ├─ validation/assertInvariant.ts
│  │  └─ public.ts
│  ├─ questions/
│  │  ├─ contracts/
│  │  │  ├─ question.ts
│  │  │  ├─ answer.ts
│  │  │  ├─ bank.ts
│  │  │  └─ selection.ts
│  │  ├─ data/
│  │  │  ├─ core/index.ts
│  │  │  ├─ core/core-01.ts ... core-12.ts
│  │  │  ├─ holdout/index.ts
│  │  │  ├─ holdout/holdout-01.ts ... holdout-04.ts
│  │  │  ├─ tie-break/index.ts
│  │  │  └─ tie-break/tie-break-01.ts ... tie-break-04.ts
│  │  ├─ registry/createQuestionRegistry.ts
│  │  ├─ validation/validateQuestion.ts
│  │  ├─ validation/validateQuestionBank.ts
│  │  ├─ selection/seededOrder.ts
│  │  ├─ selection/selectNextItem.ts
│  │  └─ public.ts
│  ├─ scoring/
│  │  ├─ contracts/input.ts
│  │  ├─ contracts/output.ts
│  │  ├─ aggregate/aggregateEvidence.ts
│  │  ├─ evidence/buildEvidenceMap.ts
│  │  ├─ models/expectedProfiles/
│  │  │  ├─ index.ts
│  │  │  └─ ile.ts, sei.ts, ese.ts, lii.ts, eie.ts, lsi.ts, sle.ts, iei.ts,
│  │  │     see.ts, ili.ts, lie.ts, esi.ts, lse.ts, eii.ts, iee.ts, sli.ts
│  │  ├─ comparison/compareCandidates.ts
│  │  ├─ holdout/evaluateHoldout.ts
│  │  ├─ personFit/evaluatePersonFit.ts
│  │  ├─ confidence/deriveConfidence.ts
│  │  └─ public.ts
│  ├─ profiles/
│  │  ├─ contracts/profile.ts
│  │  ├─ data/index.ts
│  │  ├─ data/ile.ts, sei.ts, ese.ts, lii.ts, eie.ts, lsi.ts, sle.ts, iei.ts,
│  │  │  see.ts, ili.ts, lie.ts, esi.ts, lse.ts, eii.ts, iee.ts, sli.ts
│  │  ├─ narrative/buildProfileNarrative.ts
│  │  └─ public.ts
│  ├─ session/
│  │  ├─ contracts/session.ts
│  │  ├─ state/sessionState.ts
│  │  ├─ state/sessionReducer.ts
│  │  ├─ state/transitions.ts
│  │  ├─ orchestration/createSession.ts
│  │  ├─ orchestration/recordAnswer.ts
│  │  ├─ orchestration/advanceSession.ts
│  │  ├─ orchestration/finalizeSession.ts
│  │  ├─ ports/sessionStore.ts
│  │  └─ public.ts
│  ├─ storage/
│  │  ├─ contracts/persistedEnvelope.ts
│  │  ├─ keys.ts
│  │  ├─ migrations/migratePersistedData.ts
│  │  ├─ adapters/localStorageSessionStore.ts
│  │  ├─ adapters/localStoragePreferencesStore.ts
│  │  ├─ adapters/indexedDbCardDraftStore.ts
│  │  ├─ recovery/quarantineCorruptRecord.ts
│  │  └─ public.ts
│  ├─ result/
│  │  ├─ contracts/result.ts
│  │  ├─ contracts/cardInput.ts
│  │  ├─ build/buildResult.ts
│  │  ├─ projection/toResultViewModel.ts
│  │  ├─ projection/toCardInput.ts
│  │  └─ public.ts
│  ├─ card/
│  │  ├─ contracts/cardSchema.ts
│  │  ├─ contracts/renderSpec.ts
│  │  ├─ templates/index.ts
│  │  ├─ templates/portrait.ts
│  │  ├─ templates/square.ts
│  │  ├─ templates/story.ts
│  │  ├─ photo/decodePhoto.ts
│  │  ├─ photo/cropPhoto.ts
│  │  ├─ render/renderCard.ts
│  │  ├─ export/exportPng.ts
│  │  ├─ share/shareCard.ts
│  │  └─ public.ts
│  ├─ audit/
│  │  ├─ architecture/checkImportBoundaries.ts
│  │  ├─ questions/auditQuestionBank.ts
│  │  ├─ questions/auditCoverage.ts
│  │  ├─ questions/auditLeakage.ts
│  │  ├─ scoring/auditCandidateModels.ts
│  │  ├─ profiles/auditNarrativeProvenance.ts
│  │  ├─ report/createAuditReport.ts
│  │  └─ public.ts
│  └─ ui/
│     ├─ components/AppShell.tsx
│     ├─ components/ActionButton.tsx
│     ├─ components/ErrorNotice.tsx
│     ├─ components/ProgressIndicator.tsx
│     ├─ hooks/useAssessmentController.ts
│     ├─ routes/LandingRoute.tsx
│     ├─ routes/ModeRoute.tsx
│     ├─ routes/AssessmentRoute.tsx
│     ├─ routes/ResultRoute.tsx
│     ├─ routes/CardStudioRoute.tsx
│     ├─ routes/ReferencesRoute.tsx
│     └─ styles/
│        ├─ reset.css
│        ├─ tokens.css
│        └─ global.css
└─ tests/
   ├─ setup.ts
   ├─ helpers/renderWithProviders.tsx
   ├─ fixtures/
   │  ├─ answers.ts
   │  ├─ sessions.ts
   │  └─ candidateModels.ts
   ├─ domain/
   ├─ questions/
   ├─ scoring/
   ├─ session/
   ├─ storage/
   ├─ result/
   ├─ card/
   ├─ audit/
   └─ ui/
```

## 9. Kapasitas data yang diwajibkan

### 9.1 Question bank

- Core: **192 item**, dibagi 12 file × 16 item.
- Holdout: **32 item**, dibagi 4 file × 8 item.
- Tie-break: **32 item**, dibagi 4 file × 8 item.
- Total kapasitas produksi: **256 item**.

Batch file dipakai untuk review, code ownership, dan diff yang terkendali. Registry wajib memastikan setiap ID unik dan jumlah persis sesuai versioned manifest.

### 9.2 Candidate model

Setiap kandidat TIM memiliki matriks:

```text
8 information elements × 8 evidence channels = 64 expected cells
```

Dengan 16 kandidat, schema mendukung **1.024 expected cells** sebelum metadata dan provenance. Tahap 01 hanya menetapkan bentuk; nilai expected cell belum dibuat.

### 9.3 Evidence map

Evidence map harus dapat menelusuri:

```text
answer -> option evidence -> normalized observation -> channel/element cell
       -> candidate support/contradiction -> result explanation
```

Setiap agregat harus dapat menunjuk kembali ke item dan option asal tanpa menyimpan data personal tambahan.

## 10. Session state machine

State konseptual:

```text
idle
  -> mode-selected
  -> core-active
  -> tie-break-active       (hanya bila unresolved condition terpenuhi)
  -> holdout-active
  -> finalizing
  -> result-ready
  -> card-studio            (route terpisah; bukan state scoring)
```

State tambahan yang tidak mengubah fase pengukuran:

- `paused`;
- `recovering-storage`;
- `recoverable-error`;
- `fatal-error`.

Transisi hanya boleh melalui event yang dinyatakan dalam session reducer. Route URL tidak menjadi sumber kebenaran sesi; URL hanya mempresentasikan state yang sah.

## 11. Storage architecture

### 11.1 Media penyimpanan

| Data | Media default | Persisten | Catatan |
|---|---|---:|---|
| Theme dan preferensi non-sensitif | localStorage | Ya | Ukuran kecil |
| Session checkpoint | localStorage | Ya | Jawaban, seed, versi, phase, tanpa foto |
| Result snapshot | localStorage | Opsional | Dapat dihapus dari halaman hasil |
| Card draft tanpa foto | localStorage atau IndexedDB | Opsional | Ditentukan saat implementasi berdasarkan ukuran |
| Foto asli/hasil crop | Memory/Object URL | Tidak | IndexedDB hanya dengan opt-in eksplisit |
| Export PNG | File lokal pengguna | Sesuai tindakan pengguna | Tidak disalin ke storage aplikasi |

### 11.2 Versioned envelope

Semua record persisten memakai envelope konseptual:

```text
schemaVersion
resourceType
createdAt
updatedAt
appVersion
payload
```

Timestamp berguna untuk recovery dan retention, tetapi tidak boleh masuk scoring. Migration harus pure, berurutan, dan dapat gagal dengan aman tanpa menghapus record asal.

### 11.3 Namespace key

Key menggunakan namespace produk dan resource, misalnya:

```text
socionics-dalam-diriku:session:v1
socionics-dalam-diriku:preferences:v1
socionics-dalam-diriku:result:v1
```

Nomor di key adalah storage schema major, bukan scoring version.

## 12. Determinisme

### 12.1 Seed lifecycle

- Sesi baru memperoleh `sessionSeed` dari `crypto.getRandomValues` pada boundary browser.
- Seed disimpan dalam checkpoint.
- Pure core hanya menerima `RandomSource`; ia tidak memanggil browser crypto.
- Sub-seed diturunkan dari seed induk, purpose, bank version, dan phase.
- Fisher–Yates menerima random source sebagai parameter.
- `Math.random()` dilarang pada domain, questions selection, scoring, session transition, audit, dan card layout.

### 12.2 Stable ordering

Semua ranking memakai total ordering eksplisit. Bila nilai numerik sama, urutan lanjutan harus stabil dan terdokumentasi, misalnya evidence quality lalu canonical candidate ID. Object property order, locale, atau insertion order tidak boleh menjadi tie-break tersembunyi.

### 12.3 Reproducibility record

Result snapshot menyimpan sekurang-kurangnya:

- session seed;
- assessment mode ID dan version;
- question bank version;
- scoring version;
- candidate model version;
- answer IDs dan selected option IDs;
- display order;
- phase membership;
- engine version;
- data migration version.

Data waktu, device, ukuran viewport, dan route history tidak memengaruhi hasil.

## 13. Code splitting dan lazy loading

### 13.1 Tetap eager

- app shell;
- root error boundary;
- route map;
- minimal theme tokens;
- domain identifiers yang diperlukan navigasi;
- recovery UI.

### 13.2 Lazy route chunks

- mode selection;
- assessment;
- result;
- Card Studio;
- references.

### 13.3 Lazy data/engine chunks

- core question batches sesuai mode;
- holdout dan tie-break registry hanya saat phase relevan;
- scoring engine dan candidate model data pada assessment route sebelum first scoring snapshot;
- profile narratives pada result route;
- Canvas/photo/export/share modules pada Card Studio route.

### 13.4 Aturan prefetch

- prefetch hanya setelah intent jelas, misalnya setelah peserta memilih mode atau saat result hampir selesai;
- prefetch tidak boleh mengirim data peserta;
- kegagalan chunk menghasilkan recovery UI dan retry, bukan hasil parsial;
- critical recovery chunk tidak boleh lazy.

Dynamic import harus memakai mapping statis yang dapat dianalisis Vite, bukan path dari input peserta.

## 14. Static deployment

- output adalah aset statis Vite;
- routing memakai browser history dengan rewrite seluruh route aplikasi ke `index.html` pada host;
- `vercel.json` hanya berisi static SPA rewrite dan header aman yang relevan;
- tidak ada function directory atau API route;
- asset path harus kompatibel dengan base URL yang ditetapkan Vite;
- aplikasi tetap dapat berjalan tanpa koneksi setelah aset telah dimuat selama sesi, tetapi service worker tidak diasumsikan pada arsitektur awal.

## 15. Card Studio separation

Card Studio menerima immutable `CardInput` yang dibangun dari result snapshot. Ia tidak menerima scoring engine, answer bank, atau session controller.

```text
ResultSnapshot -> toCardInput -> CardDraft -> RenderSpec -> Canvas -> Blob/File
```

Perubahan crop, foto, warna, format, atau teks opsional pada card tidak boleh mengubah result snapshot. Card Studio dapat ditutup tanpa memengaruhi sesi atau hasil.

## 16. Correlation isolation

Korelasi lintas sistem hanya boleh muncul sebagai konten referensi sekunder pada route referensi. Modul scoring, candidate models, questions, adaptive selection, person-fit, confidence, dan result ranking dilarang mengimpor data korelasi.

Audit dependency harus memeriksa larangan tersebut secara eksplisit.

## 17. Canonical commands yang akan dibuat pada bootstrap

| Command | Maksud |
|---|---|
| `npm run dev` | Menjalankan Vite development server |
| `npm run typecheck` | Menjalankan TypeScript tanpa emit |
| `npm run lint` | Menjalankan ESLint pada source, test, dan config |
| `npm run test` | Menjalankan Vitest sekali dan mengembalikan exit code |
| `npm run coverage` | Menjalankan Vitest dengan coverage provider |
| `npm run build` | Menjalankan typecheck/build graph dan menghasilkan bundle production |

Command belum tersedia dan tidak dijalankan pada Tahap 01 karena bootstrap kode dilarang.

## 18. Acceptance architecture

Arsitektur dinyatakan memadai bila:

- dependency graph memiliki urutan topologis;
- domain tidak bergantung pada UI atau browser;
- scoring pure dan tidak membaca storage;
- data tidak mengimpor komponen;
- storage memakai versioning dan migration boundary;
- Card Studio tidak mengimpor scoring dan tidak membaca viewport untuk ukuran output;
- fixtures terpisah dari production data;
- holdout memiliki boundary terpisah;
- korelasi lintas sistem tidak memiliki jalur import ke scoring;
- seluruh route dapat dibangun sebagai static SPA;
- struktur mendukung seluruh kapasitas data yang diminta;
- tidak ada source code, question item, expected profile value, atau formula scoring yang dibuat pada Tahap 01.

## 19. Test fixture boundary

Semua fixture sintetis berada di `tests/fixtures`; production source dan production registry dilarang mengimpornya.
