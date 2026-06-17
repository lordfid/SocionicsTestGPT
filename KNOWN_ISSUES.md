# Known Issues

**Versi:** 1.1.0  
**Tanggal:** 17 Juni 2026  
**Status:** ACTIVE

## Skala prioritas

- **P0:** memblokir klaim aman atau dapat menghasilkan hasil berbahaya.
- **P1:** harus diselesaikan sebelum gate terkait lulus.
- **P2:** penting, tetapi dapat dijadwalkan setelah fondasi terkait tersedia.
- **P3:** peningkatan atau riset lanjutan.

Status issue:

- `OPEN` — belum diselesaikan;
- `PARTIALLY DESIGNED` — mitigasi arsitektur ada, implementasi dan test belum ada;
- `DOCUMENTED` — discrepancy diterima dan dikendalikan;
- `CLOSED` — kriteria tutup telah dibuktikan.

## Issues terbuka

### KI-0001 — Sumber eksternal belum diaudit satu per satu

- **Prioritas:** P1 untuk validasi ilmiah; tidak memblokir bootstrap teknis.
- **Status:** OPEN.
- **Masalah:** Peta riset mencantumkan 208 entri, tetapi masing-masing sumber primer belum dievaluasi.
- **Risiko:** Bibliografi dapat disalahartikan sebagai validasi lengkap.
- **Mitigasi:** Semua klaim diberi tier dan batas; daftar sumber tidak diperlakukan setara.
- **Kriteria tutup:** Audit sumber prioritas dengan provenance, jenis studi, sampel, metode, dan batas klaim.

### KI-0002 — Ketidaksesuaian nama file 180 versus isi 208

- **Prioritas:** P3.
- **Status:** DOCUMENTED.
- **Masalah:** Nama file menyebut 180, judul dan daftar menyebut 208.
- **Mitigasi:** Nama file dipertahankan untuk provenance; isi disebut 208 entri.
- **Kriteria tutup:** Tidak membutuhkan perubahan teknis selama penamaan konsisten.

### KI-0003 — Variasi definisi antarsekolah Socionics

- **Prioritas:** P1 sebelum kontrak domain Gate 2 dibekukan.
- **Status:** OPEN.
- **Masalah:** SCS, SSS, SHS, WSS, dan tradisi lain dapat memberi penekanan berbeda pada elemen dan TIM.
- **Risiko:** Mapping domain menjadi campuran sekolah yang tidak koheren.
- **Mitigasi:** Model A Tier A dijadikan baseline; provenance per field diwajibkan.
- **Kriteria tutup:** Glossary domain, source policy, dan mapping 16 TIM memiliki provenance yang konsisten serta tests.

### KI-0004 — Belum ada kalibrasi empiris

- **Prioritas:** P0 untuk klaim akurasi; P1 untuk scoring final.
- **Status:** OPEN.
- **Masalah:** Tidak ada data responden untuk diskriminasi item, reliabilitas, likelihood, prior, threshold, atau confidence calibration.
- **Risiko:** False precision dan overfitting teori.
- **Mitigasi:** Angka pra-kalibrasi disebut indeks kecocokan relatif.
- **Kriteria tutup:** Dataset berizin, protokol validasi, test-retest, holdout, DIF, calibration report, dan evaluasi lintas budaya.

### KI-0005 — Terminologi Bahasa Indonesia belum diuji

- **Prioritas:** P1 sebelum Gate 4 lulus.
- **Status:** OPEN.
- **Masalah:** Terjemahan valued, vital, accepting, producing, threat, relief, dan background dapat dipahami berbeda.
- **Risiko:** Item mengukur interpretasi bahasa, bukan konstruk.
- **Mitigasi:** Glossary internal dan adegan konkret; istilah teori tidak ditampilkan pada pertanyaan.
- **Kriteria tutup:** Cognitive interviewing lintas latar peserta dan revisi terdokumentasi.

### KI-0006 — Delapan kanal belum diimplementasikan sebagai schema teknis

- **Prioritas:** P1 pada Gate 2.
- **Status:** PARTIALLY DESIGNED.
- **Masalah:** Nama, dependency owner, dan target path telah ditetapkan, tetapi TypeScript contract, runtime validator, dan tests belum ada.
- **Mitigasi:** `ARCHITECTURE.md` mengunci `domain/socionics/evidenceChannels.ts` dan larangan dependency keluar.
- **Kriteria tutup:** Type-safe contract, exact-set invariant, runtime validation, dan tests lulus.

### KI-0007 — Model A 16 TIM dan expected profiles belum diformalisasi

- **Prioritas:** P1 pada Gate 2 untuk mapping struktural; P1 pada Gate 6 untuk expected profiles.
- **Status:** PARTIALLY DESIGNED.
- **Masalah:** Target file 16 TIM dan bentuk 64-cell per kandidat tersedia, tetapi tidak ada data nilai atau mapping teruji.
- **Risiko:** Expected profile berubah menjadi direct type hints atau campuran sekolah.
- **Kriteria tutup Gate 2:** Mapping delapan posisi seluruh TIM lengkap, unik, dan invariant-tested.
- **Kriteria tutup Gate 6:** 16 × 64 expected cells, provenance, support/contradiction logic, dan adversarial tests lengkap.

### KI-0008 — Question schema dan content audit belum dibuat

- **Prioritas:** P1 pada Gate 3.
- **Status:** OPEN.
- **Masalah:** Target file sudah dirancang, tetapi schema, validator, coverage matrix, social-desirability audit, dan context audit belum ada.
- **Kriteria tutup:** Gate 3 lulus dengan runtime validation dan audit contracts.

### KI-0009 — Holdout leakage safeguards belum diimplementasikan

- **Prioritas:** P1 pada Gate 5.
- **Status:** PARTIALLY DESIGNED.
- **Masalah:** Arsitektur telah mengunci primary ranking sebelum holdout, tetapi registry, phase enforcement, dan tests belum ada.
- **Mitigasi:** Separate directories, `PrimaryResultLock`, holdout-only observations, dan forbidden import/data paths telah ditetapkan.
- **Kriteria tutup:** 32 holdout items, phase validators, lock enforcement, leakage tests, dan report lulus.

### KI-0010 — Person-fit dan response-style policy belum ditetapkan

- **Prioritas:** P1 pada Gate 7.
- **Status:** OPEN.
- **Masalah:** Bentuk signal direncanakan, tetapi indikator, threshold, missingness, dan bahasa peserta belum ditetapkan.
- **Risiko:** Confidence palsu atau label yang menghakimi.
- **Kriteria tutup:** Policy non-diagnostic, synthetic vectors, threshold rationale, confidence constraints, dan wording review.

### KI-0011 — Storage dan privasi foto belum diimplementasikan

- **Prioritas:** P1 sebelum Gate 9–10.
- **Status:** PARTIALLY DESIGNED.
- **Masalah:** localStorage/IndexedDB boundaries, envelope, opt-in, dan reset levels telah dirancang, tetapi browser behavior belum diuji.
- **Mitigasi:** Foto memory-only secara default; session tidak mengimpor adapter.
- **Kriteria tutup:** Data inventory, adapters, migrations, opt-in flow, quota/corruption tests, dan clear-all verification.

### KI-0012 — Web Share fallback dan format card belum diuji

- **Prioritas:** P1 pada Gate 10.
- **Status:** PARTIALLY DESIGNED.
- **Masalah:** Portrait, square, story, file share, download, dan text fallback telah dipisahkan secara arsitektural, tetapi belum ada browser matrix.
- **Kriteria tutup:** Export/share capability matrix dan tests pada target Android/desktop browser.

### KI-0013 — Accessibility belum memiliki acceptance matrix final

- **Prioritas:** P1 pada Gate 9 dan 11.
- **Status:** OPEN.
- **Masalah:** Keyboard, focus, screen reader, reduced motion, contrast, zoom, touch target, dan error recovery belum diformalisasi per route.
- **Kriteria tutup:** Automated behavior tests dan manual matrix terdokumentasi.

### KI-0014 — Potensi false precision pada model comparison

- **Prioritas:** P1 pada Gate 6–7.
- **Status:** OPEN.
- **Masalah:** Bahasa posterior atau confidence dapat memberi kesan probabilitas tervalidasi.
- **Mitigasi:** `ResultSnapshot` wajib membawa batas ilmiah; label saat ini tetap indeks kecocokan relatif.
- **Kriteria tutup:** Calibration study atau wording yang terus membatasi klaim tanpa celah.

### KI-0015 — Korelasi komunitas dapat merembes ke narasi

- **Prioritas:** P1 pada Gate 8.
- **Status:** PARTIALLY DESIGNED.
- **Masalah:** Scoring path sudah diisolasi, tetapi profile narrative belum ada sehingga stereotype leakage belum dapat diuji.
- **Mitigasi:** Correlation content hanya boleh berada pada route referensi dan narrative provenance audit telah direncanakan.
- **Kriteria tutup:** Profiles, audit provenance, forbidden inference tests, dan human review lulus.

### KI-0016 — Dependency boundary enforcement belum tersedia

- **Prioritas:** P1 pada Gate 2.
- **Status:** PARTIALLY DESIGNED.
- **Masalah:** Dependency DAG memiliki urutan topologis, tetapi ESLint restrictions dan cycle checker belum diimplementasikan.
- **Risiko:** Developer dapat mengimpor internal module dan membentuk siklus tanpa sadar.
- **Kriteria tutup:** Lint/audit test gagal pada fixture serangan dan lulus pada tree produksi.

### KI-0017 — PRNG dan golden determinism vectors belum dipilih di kode

- **Prioritas:** P1 pada Gate 2 dan Gate 7.
- **Status:** PARTIALLY DESIGNED.
- **Masalah:** Seed lifecycle dan `RandomSource` telah dikunci, tetapi algoritma implementasi serta golden vectors belum diuji lintas runtime.
- **Kriteria tutup:** Algoritma pure terdokumentasi, fixed vectors lulus, dan core path bebas `Math.random()`.

### KI-0018 — Static SPA rewrite belum diverifikasi pada deployment nyata

- **Prioritas:** P1 pada Gate 2 dan Gate 11.
- **Status:** PARTIALLY DESIGNED.
- **Masalah:** Browser history + rewrite telah dipilih, tetapi refresh route dan asset base belum diuji.
- **Kriteria tutup:** Production build dan deployed route refresh lulus tanpa function/API.

### KI-0019 — Quota dan private-mode storage berbeda antar-browser

- **Prioritas:** P1 pada Gate 9.
- **Status:** OPEN.
- **Masalah:** localStorage/IndexedDB dapat ditolak, dibatasi, atau dihapus oleh browser.
- **Risiko:** Peserta mengira sesi dapat dilanjutkan padahal checkpoint gagal.
- **Mitigasi:** Memory-only path dan warning dirancang.
- **Kriteria tutup:** Browser matrix, write verification, quota simulation, dan honest resume status.

### KI-0020 — Canvas dan font dapat mengurangi determinisme visual

- **Prioritas:** P1 pada Gate 10.
- **Status:** OPEN.
- **Masalah:** Font metrics, Canvas rasterization, EXIF orientation, dan memory limit berbeda antar-browser.
- **Mitigasi:** Explicit RenderSpec, font readiness, structural layout tests, environment-pinned golden tests.
- **Kriteria tutup:** Cross-browser export matrix dan documented tolerance.

### KI-0021 — Adaptive stop policy belum ditetapkan

- **Prioritas:** P1 pada Gate 7.
- **Status:** OPEN.
- **Masalah:** Arsitektur mendukung adaptive selection, tetapi minimum evidence, unresolved threshold, item budget, dan stop conditions belum ditetapkan.
- **Risiko:** Sesi terlalu cepat berhenti atau terlalu panjang tanpa manfaat.
- **Kriteria tutup:** Simulated vectors, fairness review, holdout check, dan documented policy.

### KI-0022 — Deployment version skew saat lazy chunk belum diuji

- **Prioritas:** P2 sebelum Gate 11.
- **Status:** OPEN.
- **Masalah:** Tab lama dapat meminta chunk yang hilang setelah deployment baru.
- **Mitigasi:** Chunk error recovery dan compatibility check telah dirancang.
- **Kriteria tutup:** Simulated stale-tab test, reload policy, dan checkpoint compatibility verification.

### KI-0023 — Gate 2 belum dapat lulus tanpa codebase

- **Prioritas:** P1 pada Tahap 02.
- **Status:** OPEN.
- **Masalah:** Tahap 01 hanya menghasilkan arsitektur; package, source, tests, lint, typecheck, coverage, dan build belum ada.
- **Kriteria tutup:** Acceptance Gate 2 dijalankan dan seluruh command relevan lulus.
