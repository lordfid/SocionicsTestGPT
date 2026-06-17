# Next Stage

**Versi:** 2.0.0  
**Tanggal:** 17 Juni 2026  
**Status:** ACTIVE  
**Tahap berikutnya belum dimulai.**

## 1. Tahap yang disiapkan

**Tahap 02 — Bootstrap proyek yang benar-benar dapat di-build**  
**Gate terkait:** Gate 2 — Fondasi proyek dan kontrak domain  
**Status gate saat masuk:** IN PROGRESS  
**Bobot gate:** 8%

Tahap 02 adalah substage implementasi pertama Gate 2. Tujuannya membuat fondasi React + TypeScript + Vite yang bersih, dapat dijalankan, dapat diuji, dapat dibangun sebagai static SPA, dan sesuai dengan dependency boundaries yang telah ditetapkan.

Tahap 02 tidak otomatis meluluskan Gate 2 bila mapping Model A dan kontrak domain lengkap belum masuk scope atau belum lulus acceptance criteria.

## 2. File yang wajib dibaca sebelum mulai

Urutan baca:

1. `docs/PROJECT_CONSTITUTION.md`
2. `docs/MEASUREMENT_PRINCIPLES.md`
3. `docs/ARCHITECTURE.md`
4. `docs/DATA_FLOW.md`
5. `docs/ERROR_STRATEGY.md`
6. `docs/TEST_STRATEGY.md`
7. `docs/DECISIONS.md`
8. `docs/REFERENCE_MATRIX.md`
9. `docs/WORKFLOW.md`
10. `docs/FILE_MANIFEST.md`
11. `docs/KNOWN_ISSUES.md`
12. `docs/COVERAGE_REPORT.md`
13. `docs/PROJECT_STATE.md`
14. `docs/CHANGELOG.md`
15. `docs/NEXT_STAGE.md`

Seluruh filesystem proyek harus diperiksa sebelum membuat file agar tidak ada duplikasi atau path yang melanggar manifest.

## 3. File FROZEN

Tidak boleh diubah tanpa proposal migrasi:

- `docs/PROJECT_CONSTITUTION.md`
- `docs/MEASUREMENT_PRINCIPLES.md`

Kontrak yang harus dipertahankan:

- nama produk **Socionics Dalam Diriku**;
- status ilmiah;
- Tier A–D;
- delapan kanal permanen;
- perbandingan 16 kandidat;
- local-first dan tanpa backend;
- larangan korelasi lintas sistem masuk scoring;
- progres hanya berdasarkan gate penuh.

## 4. File CONTROLLED

Perubahan memerlukan analisis dampak dan verification:

- `docs/REFERENCE_MATRIX.md`
- `docs/WORKFLOW.md`
- `docs/ARCHITECTURE.md`
- `docs/DATA_FLOW.md`
- `docs/ERROR_STRATEGY.md`
- `docs/TEST_STRATEGY.md`
- `docs/FILE_MANIFEST.md`
- `docs/DECISIONS.md`
- `docs/COVERAGE_REPORT.md`
- `docs/CHANGELOG.md`

`DECISIONS.md` dan `CHANGELOG.md` tetap append-only.

## 5. File ACTIVE pada Tahap 02

Dokumen status:

- `docs/PROJECT_STATE.md`
- `docs/KNOWN_ISSUES.md`
- `docs/NEXT_STAGE.md`

Target implementation files sesuai manifest:

- root package/config files;
- `public/manifest.webmanifest`;
- favicon dan local icons;
- `src/main.tsx`;
- `src/app/**` yang diperlukan shell;
- minimal `src/ui/**` untuk shell, route status, theme, dan recovery;
- test setup dan test yang benar-benar menguji shell/configuration;
- import-boundary scaffolding yang relevan dengan file yang sudah ada.

File tidak boleh dibuat hanya agar tree terlihat penuh.

## 6. Tujuan Tahap 02

Tahap 02 harus membuat atau memperbaiki:

- `package.json` dan lockfile hasil install nyata;
- Vite, TypeScript, ESLint, Vitest, dan React Testing Library;
- canonical commands `dev`, `typecheck`, `lint`, `test`, `coverage`, dan `build`;
- static Vercel rewrite tanpa API route;
- web app manifest dan favicon lokal;
- app shell;
- browser router dengan lazy route wiring;
- root error boundary;
- theme foundation;
- CSS reset, design tokens, dan global styles;
- route shells yang benar-benar dipakai oleh router;
- folder structure yang sesuai `ARCHITECTURE.md` tanpa membuat data gate berikutnya;
- baseline tests untuk shell, error boundary, route load, dan import boundaries yang telah dapat ditegakkan.

Route sementara hanya boleh menunjukkan status pengembangan internal. Route tidak boleh menampilkan hasil Socionics, kandidat TIM, atau data peserta palsu.

## 7. Yang dilarang pada Tahap 02

- teks atau opsi pertanyaan;
- production question data;
- holdout atau tie-break item;
- scoring weights, prior, likelihood, threshold, atau formula;
- expected profile 16 TIM;
- profil naratif 16 TIM;
- adaptive selection implementation;
- person-fit formula;
- confidence formula;
- hasil random atau mock result;
- Card Studio lengkap;
- pemrosesan foto;
- test data yang masuk production source;
- backend, API, serverless function, database, autentikasi, atau analytics;
- import kosong, fungsi kosong, TODO, placeholder, dan route yang tidak pernah digunakan.

## 8. Acceptance criteria Tahap 02

Tahap 02 baru dapat ditutup bila:

- `npm install` atau `npm ci` berhasil dengan lockfile konsisten;
- `npm run typecheck` exit code 0;
- `npm run lint` exit code 0;
- `npm run test` exit code 0 dan jumlah test dicatat;
- `npm run coverage` exit code 0 dan coverage dicatat tanpa mengklaim scope yang belum ada;
- `npm run build` exit code 0;
- dev server dapat start dan entry route dapat dimuat dalam smoke check;
- static route rewrite tidak memperkenalkan API route;
- shell memakai nama produk yang benar;
- tidak ada string identitas terlarang di UI;
- file FROZEN memiliki hash yang sama;
- tidak ada source pertanyaan, scoring, expected profile, profile naratif, atau Card Studio lengkap;
- setiap file baru memiliki consumer dan test/verification;
- manifest, state, decisions, issues, coverage, next stage, dan changelog diperbarui.

## 9. Hubungan dengan Gate 2

Sesudah Tahap 02, Gate 2 hanya boleh berstatus PASS bila acceptance Gate 2 penuh juga terpenuhi, termasuk kontrak domain dan mapping Model A yang lengkap serta teruji. Bila Tahap 02 hanya menyelesaikan toolchain dan shell, Gate 2 tetap IN PROGRESS dan progres proyek tetap 4%.

## 10. Status saat ini

Tahap 01 telah ditutup. Tahap 02 belum dibuka. Tidak ada package, app source, question bank, scoring, profile, test produk, atau Card Studio yang dibuat pada Tahap 01.
