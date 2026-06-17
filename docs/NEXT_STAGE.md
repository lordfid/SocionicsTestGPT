# Next Stage

**Versi:** 3.0.0  
**Tanggal:** 17 Juni 2026  
**Status:** ACTIVE  
**Tahap berikutnya belum dimulai.**

## 1. Tahap yang disiapkan

**Tahap 03 — Kontrak domain Socionics dan mapping Model A**  
**Gate terkait:** Gate 2 — Fondasi proyek dan kontrak domain  
**Status gate saat masuk:** IN PROGRESS  
**Progres proyek saat masuk:** 4%

Tahap 03 melengkapi bagian domain yang sengaja dilarang pada Tahap 02. Tahap ini belum membuat pertanyaan, scoring weights, expected channel profile, atau narasi tipe.

## 2. Urutan baca wajib

1. `docs/PROJECT_CONSTITUTION.md`
2. `docs/MEASUREMENT_PRINCIPLES.md`
3. `docs/REFERENCE_MATRIX.md`
4. `docs/ARCHITECTURE.md`
5. `docs/DATA_FLOW.md`
6. `docs/ERROR_STRATEGY.md`
7. `docs/TEST_STRATEGY.md`
8. `docs/DEPENDENCIES.md`
9. `docs/DECISIONS.md`
10. `docs/WORKFLOW.md`
11. `docs/FILE_MANIFEST.md`
12. `docs/KNOWN_ISSUES.md`
13. `docs/COVERAGE_REPORT.md`
14. `docs/PROJECT_STATE.md`
15. `docs/CHANGELOG.md`
16. `docs/NEXT_STAGE.md`
17. seluruh source, test, dan config Tahap 02.

## 3. FROZEN

Tidak boleh diubah tanpa migrasi:

- `docs/PROJECT_CONSTITUTION.md`;
- `docs/MEASUREMENT_PRINCIPLES.md`;
- `tsconfig.json`;
- `tsconfig.app.json`;
- `tsconfig.node.json`;
- `tsconfig.test.json`.

FROZEN contract surfaces:

- nama dan maksud scripts `dev`, `typecheck`, `lint`, `test`, `coverage`, `build` pada `package.json`;
- typed lint baseline, React Hooks rules, production test/audit import ban, dan direct `Math.random` ban pada `eslint.config.js`.

## 4. CONTROLLED

- seluruh dokumen arsitektur dan governance selain tiga state files;
- `package.json` dependency lists dan command tambahan;
- lockfile;
- Vite, Vitest, ESLint additive config;
- app shell, theme, router, static assets, dan baseline tests.

Perubahan hanya boleh dilakukan bila diperlukan oleh kontrak domain dan seluruh command diperbarui.

## 5. Tujuan Tahap 03

Buat domain pure tanpa React, DOM, storage, atau network dependency:

- branded/version identifiers yang benar-benar diperlukan;
- delapan information elements;
- delapan evidence channels permanen;
- delapan Model A positions;
- empat Model A blocks;
- quadra identifiers dan valued-element mapping;
- 16 TIM identifiers;
- mapping Model A lengkap seluruh 16 TIM;
- derivation yang konsisten untuk strong/weak, valued/unvalued, mental/vital, accepting/producing, dan inert/contact bila disahkan Tier-nya;
- runtime invariants untuk uniqueness, completeness, block membership, dan candidate count;
- deterministic contracts: `RandomSource`, seeded implementation, dan stable ordering bila dikerjakan dalam scope;
- public API domain yang sempit;
- unit dan property-style table tests untuk seluruh invariant.

Mapping harus mempunyai provenance Tier A/B dan tidak boleh berasal dari konversi MBTI.

## 6. Larangan Tahap 03

- teks atau opsi pertanyaan;
- 192 core, 32 holdout, atau 32 tie-break items;
- evidence weights;
- formula scoring, prior, likelihood, threshold, confidence, atau adaptive selection;
- expected 64-channel profile per TIM;
- profil naratif 16 TIM;
- hasil peserta palsu;
- session/storage/result/Card Studio implementation;
- korelasi lintas sistem pada domain scoring;
- perubahan visual besar yang tidak diperlukan domain.

## 7. Acceptance awal

Tahap 03 baru dapat ditutup bila:

- tepat delapan information elements dan delapan channels tersedia;
- tepat delapan posisi dan empat blok tersedia;
- tepat 16 TIM tersedia;
- setiap TIM mempunyai delapan elemen unik pada delapan posisi;
- derivation strength/value/block konsisten dengan mapping;
- seluruh finite invariant kritis memiliki 100% branch coverage;
- tidak ada React/DOM/storage/network import dalam domain;
- seeded randomness tidak memakai `Math.random`;
- typecheck, lint, test, coverage, dan build lulus;
- FROZEN files tetap sama;
- manifest, decisions, state, issues, coverage, next stage, dan changelog diperbarui.

Bila seluruh acceptance Gate 2 terpenuhi setelah Tahap 03, Gate 2 dapat dinaikkan menjadi PASS dan progres menjadi 12%. Kenaikan tidak boleh dilakukan hanya karena jumlah file bertambah.

## 8. Status

Tahap 03 belum dimulai. Tidak ada file `src/domain` di paket Tahap 02.
