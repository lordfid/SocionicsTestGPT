# Workflow Proyek

**Versi:** 1.0.0  
**Tanggal:** 17 Juni 2026  
**Status:** CONTROLLED

## 1. Prinsip kerja

Proyek bergerak berdasarkan gate, bukan berdasarkan banyaknya file atau kesan visual. Setiap tahap memiliki scope tertutup. Pekerjaan di luar scope ditahan dalam `KNOWN_ISSUES.md` atau `NEXT_STAGE.md` dan tidak boleh disisipkan diam-diam.

## 2. Siklus lima lintasan

### PASS 1 — Implementasi

- Baca file FROZEN dan CONTROLLED yang diwajibkan.
- Nyatakan scope dan acceptance criteria.
- Buat hanya artefak tahap aktif.
- Pastikan setiap file digunakan dan memiliki tujuan.

### PASS 2 — Self-review

Periksa:

- kontradiksi domain;
- repetisi;
- istilah yang bergeser makna;
- import atau referensi rusak;
- data setengah jadi;
- asumsi tidak tercatat;
- klaim terlalu pasti;
- kebocoran teori ke UI;
- ketidakseimbangan coverage.

### PASS 3 — Adversarial review

Reviewer adversarial harus mencoba membuktikan:

- hasil dapat dimanipulasi oleh satu jawaban;
- mask dianggap fungsi utama;
- strength tertukar dengan valued;
- PoLR tertukar dengan low skill;
- Suggestive tertukar dengan incompetence;
- stereotip profesi atau citra mengunci tipe;
- angka confidence memberi false precision;
- file atau fitur tidak benar-benar digunakan;
- command yang diklaim tidak pernah dijalankan.

### PASS 4 — Repair

- Perbaiki seluruh temuan dalam scope.
- Catat keputusan baru bila makna kontrak berubah.
- Perbarui test yang terpengaruh.
- Jangan menyembunyikan temuan yang belum dapat diperbaiki; pindahkan ke `KNOWN_ISSUES.md`.

### PASS 5 — Verification

Jalankan command yang relevan dengan tahap:

- dokumentasi: integrity assertions, manifest check, forbidden-marker check;
- TypeScript: typecheck;
- kode: lint;
- unit/domain: Vitest;
- komponen: React Testing Library;
- paket: production build;
- artefak visual: export checks dan pemeriksaan ukuran;
- accessibility: automated checks ditambah pemeriksaan manual yang dicatat.

Command yang tidak relevan harus ditulis sebagai **not applicable**, bukan diklaim lulus.

## 3. Gate berbobot

| No. | Gate | Bobot | Syarat umum |
|---:|---|---:|---|
| 1 | Referensi dan konstitusi | 4% | Dokumen wajib tersedia, keputusan konflik dicatat, batas verifikasi jujur |
| 2 | Fondasi proyek dan kontrak domain | 8% | Toolchain, types, constants, Model A mapping, contracts, baseline tests |
| 3 | Schema pertanyaan dan audit | 5% | Schema stabil, validators, coverage/fairness contracts |
| 4 | Bank pertanyaan inti | 24% | Item lengkap, seimbang, audited, tanpa teori di UI |
| 5 | Holdout dan tie-break | 5% | Set pembeda terpisah, leakage dicegah, test vectors |
| 6 | Scoring dan model comparison | 20% | 16 kandidat dibandingkan, evidence/contradiction, normalization, tests |
| 7 | Anti-mistype, adaptive, confidence | 8% | unresolved pairs, selection policy, quality-aware confidence |
| 8 | Profil serta narasi hasil | 8% | result schema, varied narratives, scientific limits |
| 9 | UI, session, storage | 7% | alur peserta, resume, privacy, responsive, accessible |
| 10 | Card Studio | 7% | local photo, themes, adaptive orientations, download/share fallback |
| 11 | QA, accessibility, packaging | 4% | full verification, release package, manifest, no hidden failures |

## 4. Prosedur perubahan file

### FROZEN

1. Buat proposal migrasi.
2. Jelaskan masalah yang tidak dapat diperbaiki tanpa perubahan.
3. Daftar dampak domain dan teknis.
4. Tambahkan keputusan baru.
5. Perbarui version major atau minor sesuai dampak.
6. Perbarui semua test dan dokumen turunan.
7. Jalankan ulang gate terdampak.

### CONTROLLED

1. Analisis dampak.
2. Catat alasan di `DECISIONS.md` atau `CHANGELOG.md`.
3. Perbarui test atau assertions.
4. Jalankan verifikasi terkait.

### ACTIVE

Boleh berubah selama masih berada dalam scope tahap dan tidak melanggar FROZEN contracts.

## 5. Versioning

Gunakan semantic versioning internal:

- **major:** kontrak tidak kompatibel;
- **minor:** kemampuan baru yang kompatibel;
- **patch:** koreksi tanpa mengubah kontrak.

Versi minimum yang dilacak:

- scoring version;
- question bank version;
- card schema version;
- constitution version;
- measurement principles version.

Versi `0.0.0` berarti belum dibuat, bukan versi sementara yang siap dipakai.

## 6. Aturan status progres

Progres dihitung dari bobot gate yang lulus seluruh acceptance criteria.

- Gate parsial tidak memberi persentase parsial kecuali acceptance criteria gate secara eksplisit membaginya menjadi subgate berbobot.
- Gate yang sebelumnya lulus dapat dibuka kembali bila migrasi merusak acceptance criteria.
- Progres tidak boleh mencapai 100% bila ada command final gagal atau gate dibuka kembali.

## 7. Bentuk laporan penutupan tahap

Setiap penutupan tahap harus memuat:

- file dibuat, diubah, atau dihapus;
- status setiap file;
- keputusan baru;
- lima lintasan dan temuannya;
- command yang dijalankan;
- hasil command;
- gate lulus atau gagal;
- progres baru;
- masalah terbuka;
- isi ringkas tahap berikutnya.

## 8. Aturan referensi

- Pisahkan teori internal, metode psikometri, pendapat komunitas, dan korelasi lintas sistem.
- Jangan menganggap panjang bibliografi sebagai validasi.
- Klaim yang belum diverifikasi harus diberi batas.
- Konflik antarsekolah harus dicatat, bukan diselesaikan dengan memilih diam-diam.
- Instruksi pengguna yang lebih ketat mengalahkan tier yang lebih longgar dalam referensi.

## 9. Aturan command

Sebelum mencatat command berhasil:

- jalankan command nyata;
- simpan exit code;
- catat jumlah test atau assertion;
- catat warning yang relevan;
- jangan memotong error yang memengaruhi status gate.

## 10. Larangan workflow

- Memulai tahap berikutnya sebelum tahap aktif ditutup.
- Membuat UI sebelum kontrak domain dan audit siap.
- Membuat scoring sebelum schema dan expected profile stabil.
- Menambah pertanyaan tanpa coverage target dan audit.
- Menambah fitur eksperimental ke skor inti.
- Mengubah file FROZEN demi mempercepat implementasi.
- Menyatakan “selesai” hanya karena file berhasil dibuat.
