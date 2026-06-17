# Known Issues

**Versi:** 1.0.0  
**Tanggal:** 17 Juni 2026  
**Status:** ACTIVE

## Skala prioritas

- **P0:** memblokir kelanjutan atau dapat menghasilkan klaim berbahaya.
- **P1:** harus diselesaikan sebelum gate terkait lulus.
- **P2:** penting tetapi dapat dijadwalkan.
- **P3:** peningkatan atau riset lanjutan.

## Issues terbuka

### KI-0001 — Sumber eksternal belum diaudit satu per satu

- **Prioritas:** P1 untuk validasi ilmiah; tidak memblokir fondasi teknis.
- **Status:** OPEN.
- **Masalah:** Peta riset mencantumkan 208 entri, tetapi Tahap 00 tidak membuka dan mengevaluasi masing-masing sumber primer.
- **Risiko:** Bibliografi dapat disalahartikan sebagai validasi lengkap.
- **Mitigasi sementara:** Semua klaim diberi tier dan batas; daftar sumber tidak diperlakukan setara.
- **Kriteria tutup:** Audit sumber prioritas dengan provenance, jenis studi, sampel, metode, dan batas klaim.

### KI-0002 — Ketidaksesuaian nama file 180 versus isi 208

- **Prioritas:** P3.
- **Status:** DOCUMENTED.
- **Masalah:** Nama file menyebut 180, judul dan daftar menyebut 208.
- **Mitigasi:** Nama file dipertahankan; isi disebut 208 entri.
- **Kriteria tutup:** Tidak perlu mengganti file; cukup provenance tetap konsisten.

### KI-0003 — Variasi definisi antarsekolah Socionics

- **Prioritas:** P1 sebelum kontrak domain Gate 2 dikunci.
- **Status:** OPEN.
- **Masalah:** SCS, SSS, SHS, WSS, dan tradisi lain dapat memberi penekanan berbeda pada elemen dan TIM.
- **Risiko:** Expected profile menjadi campuran sekolah yang tidak koheren.
- **Mitigasi:** Model A Tier A menjadi baseline; perbedaan sekolah dicatat eksplisit.
- **Kriteria tutup:** Domain glossary dan source policy per field tersedia.

### KI-0004 — Belum ada kalibrasi empiris

- **Prioritas:** P0 untuk klaim akurasi; P1 untuk scoring final.
- **Status:** OPEN.
- **Masalah:** Tidak ada data responden untuk mengestimasi diskriminasi item, reliabilitas, prior, likelihood, atau threshold confidence.
- **Risiko:** False precision dan overfitting teori.
- **Mitigasi:** Sebut indeks kecocokan relatif; semua bobot awal dilabel teoritis.
- **Kriteria tutup:** Dataset berizin, protokol validasi, analisis item, test-retest, holdout, DIF, dan laporan kalibrasi.

### KI-0005 — Terminologi Bahasa Indonesia belum diuji

- **Prioritas:** P1 sebelum bank pertanyaan dinyatakan selesai.
- **Status:** OPEN.
- **Masalah:** Terjemahan istilah seperti valued, vital, accepting, producing, threat, relief, dan background dapat dipahami berbeda.
- **Risiko:** Item mengukur interpretasi bahasa, bukan konstruk.
- **Mitigasi:** Gunakan glossary internal dan adegan konkret; jangan tampilkan istilah teori di layar pertanyaan.
- **Kriteria tutup:** Cognitive interviewing lintas latar peserta dan revisi berdasarkan temuan.

### KI-0006 — Delapan kanal belum memiliki schema teknis

- **Prioritas:** P1 pada Gate 2.
- **Status:** OPEN.
- **Masalah:** Nama dan makna kanal sudah dikunci, tetapi types, validators, dan invariants belum dibuat.
- **Risiko:** Implementasi dapat mengubah makna kanal secara diam-diam.
- **Kriteria tutup:** TypeScript contracts, runtime validation, fixtures, dan tests tersedia.

### KI-0007 — Expected profile 16 TIM belum diformalisasi

- **Prioritas:** P1 pada Gate 2 dan Gate 6.
- **Status:** OPEN.
- **Masalah:** Mapping Model A dikenal secara teoritis, tetapi belum ada kontrak data dan penyangkal per kandidat.
- **Risiko:** Scoring berubah menjadi direct type hints.
- **Kriteria tutup:** Semua 16 kandidat memiliki mapping delapan posisi, tier provenance, expected channels, dan tests.

### KI-0008 — Belum ada question schema atau audit

- **Prioritas:** P1 pada Gate 3.
- **Status:** OPEN.
- **Masalah:** Belum ada schema, validator, coverage matrix, social-desirability audit, atau context audit.
- **Kriteria tutup:** Gate 3 lulus.

### KI-0009 — Belum ada strategi holdout dan leakage prevention

- **Prioritas:** P1 pada Gate 5.
- **Status:** OPEN.
- **Masalah:** Item holdout dapat bocor ke scoring awal atau dioptimalkan bersama item utama.
- **Kriteria tutup:** Set terpisah, contracts, tests, dan laporan leakage.

### KI-0010 — Belum ada person-fit dan response-style policy

- **Prioritas:** P1 pada Gate 7.
- **Status:** OPEN.
- **Masalah:** Random, idealized, monoton, acquiescent, extreme, atau overly safe responses belum dibedakan.
- **Risiko:** Confidence palsu dan labeling peserta secara tidak adil.
- **Kriteria tutup:** Quality indicators, warnings non-judgmental, synthetic vectors, dan thresholds yang terdokumentasi.

### KI-0011 — Storage dan privasi foto belum dirancang

- **Prioritas:** P1 sebelum Gate 9–10.
- **Status:** OPEN.
- **Masalah:** localStorage memiliki batas ukuran; IndexedDB menambah kompleksitas; foto dapat memuat data sensitif.
- **Kriteria tutup:** Data inventory, retention policy, opt-in, clear/reset flow, local processing tests.

### KI-0012 — Web Share fallback dan orientasi card belum diuji

- **Prioritas:** P1 pada Gate 10.
- **Status:** OPEN.
- **Masalah:** Dukungan Web Share dan file sharing berbeda antar-browser; format platform berbeda.
- **Kriteria tutup:** Export matrix, fallback download/copy, ukuran, crop, dan device tests.

### KI-0013 — Accessibility belum memiliki acceptance matrix

- **Prioritas:** P1 pada Gate 9 dan 11.
- **Status:** OPEN.
- **Masalah:** Keyboard, focus, screen reader, reduced motion, contrast, zoom, dan touch target belum diformalisasi.
- **Kriteria tutup:** Checklist, automated tests, dan pemeriksaan manual terdokumentasi.

### KI-0014 — Potensi false precision Bayesian

- **Prioritas:** P1 pada Gate 6–7.
- **Status:** OPEN.
- **Masalah:** Bahasa posterior dapat memberi kesan probabilitas tervalidasi meski likelihood teoritis.
- **Mitigasi:** Gunakan indeks kecocokan relatif sampai kalibrasi.
- **Kriteria tutup:** Calibration study atau labeling yang tetap membatasi klaim.

### KI-0015 — Korelasi komunitas mudah merembes ke narasi

- **Prioritas:** P1 pada Gate 8.
- **Status:** OPEN.
- **Masalah:** Walau tidak masuk scoring, stereotype lintas tipologi dapat masuk ke subtitle atau profil tipe.
- **Kriteria tutup:** Narrative provenance audit dan tests yang melarang inference lintas sistem.
