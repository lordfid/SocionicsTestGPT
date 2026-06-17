# Changelog

Semua perubahan penting proyek dicatat di sini. Dokumen bersifat append-only.

## [0.1.0] — 17 Juni 2026 — Tahap 00

### Added

- `docs/PROJECT_CONSTITUTION.md`
- `docs/REFERENCE_MATRIX.md`
- `docs/MEASUREMENT_PRINCIPLES.md`
- `docs/WORKFLOW.md`
- `docs/PROJECT_STATE.md`
- `docs/FILE_MANIFEST.md`
- `docs/DECISIONS.md`
- `docs/KNOWN_ISSUES.md`
- `docs/COVERAGE_REPORT.md`
- `docs/NEXT_STAGE.md`
- `docs/CHANGELOG.md`

### Locked

- Nama produk **Socionics Dalam Diriku**.
- Tier A–D.
- Delapan kanal `producer`, `flexible`, `mask`, `threat`, `receiver`, `aspiration`, `dismissive`, `background`.
- Perbandingan seluruh 16 TIM sebagai model kandidat lengkap.
- Larangan element-high typing, element-low PoLR, weak-equals-Suggestive, dan direct cross-system conversion.
- Browser-only, local-first, tanpa backend, database online, API key, autentikasi, serverless API, atau analytics invasif.
- Status ilmiah dan larangan false precision.
- Progress gate berbobot.

### Reviewed

- `Atlas_Socionics_Diri_Self_Study.pdf`
- `peta_riset_socionics_180_rujukan.pdf`
- `ilide.info-typology-correlations-summarized-pr_18e3fb3ee5b551cf6263166c984fb3b9.pdf`

### Documented conflicts

- `signs` ditempatkan Tier C sesuai brief pengguna.
- Kanal permanen dibedakan dari facet pengukuran.
- Intertype relations ditunda sampai tipe stabil.
- Korelasi komunitas tidak memengaruhi scoring.
- Angka pra-kalibrasi disebut indeks kecocokan relatif.
- Nama file 180 dibedakan dari isi 208 entri.

### Verification

- 34/34 assertions dokumentasi lulus.
- 11/11 file wajib ditemukan.
- Total bobot gate terverifikasi 100%.
- Progress Tahap 00 terverifikasi 4%.
- Tidak ada file aplikasi, pertanyaan, scoring, atau test produk.

### Not applicable

- TypeScript typecheck.
- ESLint.
- Vitest.
- React Testing Library.
- Production build.

Semua command tersebut belum relevan karena Tahap 00 sengaja tidak membuat codebase.

## [0.2.0] — 17 Juni 2026 — Tahap 01

### Added

- `docs/ARCHITECTURE.md`
- `docs/DATA_FLOW.md`
- `docs/ERROR_STRATEGY.md`
- `docs/TEST_STRATEGY.md`

### Changed

- Memperluas `docs/FILE_MANIFEST.md` menjadi katalog file tersedia dan target tree per gate.
- Memperbarui `docs/PROJECT_STATE.md` dengan penutupan Tahap 01 dan status Gate 2.
- Menambahkan DEC-0023 sampai DEC-0040 ke `docs/DECISIONS.md`.
- Memperbarui `docs/KNOWN_ISSUES.md` dengan mitigasi arsitektur dan blocker implementasi.
- Mengganti `docs/NEXT_STAGE.md` untuk menyiapkan Tahap 02 bootstrap.
- Memperbarui `docs/COVERAGE_REPORT.md` untuk coverage Tahap 01.

### Locked

- Modular monolith browser-only.
- Dependency graph tanpa siklus dan public API boundary.
- Domain tanpa dependency keluar.
- Scoring pure dari normalized observations.
- Session orchestration melalui storage port.
- Primary ranking lock sebelum holdout.
- Seeded randomness dan larangan `Math.random()` pada core paths.
- Versioned persistence envelope dan foto memory-only secara default.
- Card Studio terpisah dari scoring serta viewport.
- Struktur 192 core, 32 holdout, 32 tie-break.
- Bentuk 64 expected cells per kandidat.
- Canonical npm commands.

### Verification scope

- Pemeriksaan dokumen, filesystem, hash file FROZEN, dependency DAG, manifest, dan larangan bootstrap.
- Typecheck, lint, Vitest, React Testing Library, coverage produk, dev server, dan production build tetap not available karena Tahap 01 melarang bootstrap kode.

### Progress

- Tahap 01: PASS sebagai substage arsitektur.
- Gate 2: IN PROGRESS, belum PASS.
- Progres proyek tetap **4%** sesuai gate berbobot.


## [0.3.0] — 17 Juni 2026 — Tahap 02

### Added

- React + TypeScript + Vite bootstrap yang dapat di-install, diuji, dan di-build.
- `package.json`, `package-lock.json`, TypeScript project references, Vite, Vitest, ESLint, dan Vercel static config.
- `docs/DEPENDENCIES.md` dengan versi aktual dan alasan setiap package.
- App composition, provider boundary, browser router, root error boundary, route error recovery, dan eager loading UI.
- Lazy route modules untuk beranda, status internal, dan 404.
- Theme system/light/dark dengan local preference dan storage-failure fallback.
- CSS reset, design tokens, responsive global styles, skip link, focus treatment, dan reduced-motion handling.
- Manifest, favicon SVG, icon PNG 192 × 192 dan 512 × 512.
- 6 test suites dengan 21 test cases.
- Architecture checks untuk import boundary, forbidden UI identity, direct `Math.random`, canonical scripts, local icons, static routing, dan scope exclusions.

### Changed

- `PROJECT_STATE.md` ditutup pada Tahap 02 dengan hasil command nyata.
- `FILE_MANIFEST.md` diubah dari planned tree menjadi manifest 62 file aktual serta future-folder policy.
- `COVERAGE_REPORT.md` diperbarui dengan test, coverage, build, smoke, dan gate impact.
- `NEXT_STAGE.md` menyiapkan Tahap 03 domain contracts dan Model A mapping.
- `KNOWN_ISSUES.md` memperbarui blocker bootstrap dan menambahkan issue domain, theme first paint, accessibility matrix, serta retry persistence.
- `DECISIONS.md` menambahkan DEC-0041 sampai DEC-0050.

### Locked

- Konfigurasi dasar TypeScript.
- Struktur canonical command package.
- Core lint rules dan zero-warning policy.
- Static lazy route mapping dengan eager recovery shell.
- Tidak membuat target folder kosong.

### Verification

- `npm install`: success; 253 package added; 254 audited; 0 vulnerability ditemukan saat eksekusi.
- `npm run typecheck`: success.
- `npm run lint`: success dengan zero warning.
- `npm test`: 6/6 suite dan 21/21 test lulus.
- `npm run coverage`: 96.34% statements, 86.66% branches, 94.28% functions, 97.46% lines.
- `npm run build`: success; lazy route chunks dihasilkan.
- Dev smoke: `/` dan `/status` HTTP 200.
- Hash `PROJECT_CONSTITUTION.md` dan `MEASUREMENT_PRINCIPLES.md` tidak berubah.

### Progress

- Tahap 02: PASS.
- Gate 2: IN PROGRESS karena domain contracts dan mapping Model A belum dibuat.
- Progres proyek tetap **4%**.
