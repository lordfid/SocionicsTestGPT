# Next Stage

**Versi:** 1.0.0  
**Tanggal:** 17 Juni 2026  
**Status:** ACTIVE  
**Tahap berikutnya belum dimulai.**

## 1. Tahap yang disiapkan

**Tahap 01 — Fondasi proyek dan kontrak domain**  
**Gate:** 2  
**Bobot:** 8%

Tujuan tahap berikutnya adalah menyiapkan codebase React + TypeScript + Vite dan kontrak domain yang dapat diuji, tanpa membuat bank pertanyaan, scoring final, narasi hasil, atau Card Studio.

## 2. File yang wajib dibaca sebelum mulai

Urutan baca:

1. `docs/PROJECT_CONSTITUTION.md`
2. `docs/MEASUREMENT_PRINCIPLES.md`
3. `docs/DECISIONS.md`
4. `docs/REFERENCE_MATRIX.md`
5. `docs/WORKFLOW.md`
6. `docs/KNOWN_ISSUES.md`
7. `docs/COVERAGE_REPORT.md`
8. `docs/FILE_MANIFEST.md`
9. `docs/PROJECT_STATE.md`
10. `docs/CHANGELOG.md`
11. `docs/NEXT_STAGE.md`

## 3. File FROZEN

Tidak boleh diubah pada Tahap 01 tanpa proposal migrasi:

- `docs/PROJECT_CONSTITUTION.md`
- `docs/MEASUREMENT_PRINCIPLES.md`

Kontrak yang wajib dipertahankan:

- nama produk;
- local-first, no backend;
- Tier A–D;
- delapan kanal;
- 16 model kandidat;
- status ilmiah;
- larangan korelasi lintas sistem dalam scoring;
- status file dan gate progress.

## 4. File CONTROLLED

Perubahan hanya setelah dampak dianalisis dan verifikasi diperbarui:

- `docs/REFERENCE_MATRIX.md`
- `docs/WORKFLOW.md`
- `docs/FILE_MANIFEST.md`
- `docs/DECISIONS.md`
- `docs/COVERAGE_REPORT.md`
- `docs/CHANGELOG.md`

`DECISIONS.md` dan `CHANGELOG.md` bersifat append-only.

## 5. File ACTIVE saat Tahap 01 dibuka

- `docs/PROJECT_STATE.md`
- `docs/KNOWN_ISSUES.md`
- `docs/NEXT_STAGE.md`
- file codebase dan domain contracts yang dinyatakan dalam scope Tahap 01.

## 6. Tujuan teknis Tahap 01

Tahap 01 kelak harus mencakup:

- toolchain React, TypeScript, Vite, Vitest, React Testing Library, ESLint;
- scripts build, typecheck, lint, dan test yang benar-benar dijalankan;
- kontrak TypeScript untuk information elements, Model A positions, blocks, quadra, TIM, evidence channels, provenance tier, dan version identifiers;
- mapping Model A seluruh 16 TIM;
- runtime invariants untuk memastikan setiap TIM memiliki delapan elemen unik dan posisi lengkap;
- pemisahan domain stable state, situational state, mask, response style, dan noise pada level kontrak;
- baseline unit tests;
- keputusan storage awal tanpa mengimplementasikan Card Studio;
- dokumentasi provenance per kontrak.

## 7. Yang tidak boleh dikerjakan pada Tahap 01

- bank pertanyaan;
- holdout item;
- tie-break item;
- scoring weights;
- Bayesian prior atau likelihood;
- adaptive selection;
- confidence formula;
- narasi hasil;
- UI kuis lengkap;
- pemrosesan foto;
- Card Studio;
- integrasi jaringan;
- korelasi MBTI/Enneagram/AP ke TIM.

## 8. Acceptance criteria awal Gate 2

Gate 2 baru dapat lulus bila:

- seluruh command toolchain berhasil;
- mapping 16 TIM lengkap dan diuji;
- semua information elements muncul tepat satu kali pada tiap Model A;
- blok, strength, value, dan mental/vital dapat diturunkan secara konsisten;
- delapan kanal tersedia sebagai type-safe contract;
- tidak ada import rusak, fungsi kosong, data palsu, atau file tak digunakan;
- file FROZEN tidak berubah;
- `PROJECT_STATE`, manifest, decisions, known issues, coverage, next stage, dan changelog diperbarui.

## 9. Status saat ini

Tahap 01 belum dibuka. Tidak ada file codebase, question bank, scoring, UI, atau test produk yang dibuat dalam Tahap 00.
