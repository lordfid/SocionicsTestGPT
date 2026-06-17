# Decisions

**Versi dokumen:** 1.0.0  
**Tanggal:** 17 Juni 2026  
**Status:** CONTROLLED, append-only

Keputusan lama tidak boleh diedit untuk menyesuaikan implementasi. Bila keputusan berubah, tambahkan keputusan baru yang menyatakan penggantian dan dampaknya.

## DEC-0001 — Nama produk tunggal

**Status:** LOCKED  
**Keputusan:** Seluruh UI memakai nama **Socionics Dalam Diriku**.  
**Alasan:** Menjaga identitas produk dan mencegah nama historis atau nama alat muncul.

## DEC-0002 — Scope ilmiah

**Status:** LOCKED  
**Keputusan:** Produk adalah alat refleksi tipologi, bukan diagnosis, pengukur kecerdasan, nilai manusia, atau instrumen profesional tervalidasi.  
**Alasan:** Status bukti Socionics belum mendukung klaim berisiko tinggi.

## DEC-0003 — Model A sebagai hipotesis generatif

**Status:** LOCKED  
**Keputusan:** Model A menjadi struktur teoritis utama untuk membangun dan membandingkan hipotesis, bukan fakta biologis atau psikometrik yang dianggap sudah terbukti.  
**Alasan:** Memungkinkan desain yang koheren tanpa menyembunyikan keterbatasan validasi.

## DEC-0004 — Perbandingan 16 kandidat

**Status:** LOCKED  
**Keputusan:** Semua 16 TIM dibandingkan sebagai 16 expected profiles lengkap.  
**Alasan:** Ranking elemen tunggal tidak dapat membedakan posisi kuat, lemah, valued, unvalued, mask, threat, seeking, dan background.

## DEC-0005 — Delapan kanal permanen

**Status:** LOCKED  
**Keputusan:** Kanal domain adalah `producer`, `flexible`, `mask`, `threat`, `receiver`, `aspiration`, `dismissive`, dan `background`.  
**Alasan:** Kanal membedakan pola penggunaan elemen yang tidak dapat ditangkap oleh frekuensi perilaku.

## DEC-0006 — Facet bukan kanal pengganti

**Status:** LOCKED  
**Keputusan:** Strength, valued, comfort, aversion, seeking, overcompensation, automaticity, dan facet serupa kelak menjadi indikator atau metadata di bawah kanal; mereka tidak mengganti delapan kanal.  
**Alasan:** Menyatukan istilah berbeda dalam referensi tanpa merusak kontrak pengguna.

## DEC-0007 — Tier pengguna mengalahkan tier referensi

**Status:** LOCKED  
**Keputusan:** Bila referensi menempatkan komponen lebih tinggi daripada brief Tahap 00, tier yang lebih ketat dari pengguna dipakai.  
**Alasan:** Instruksi eksplisit pengguna adalah otoritas tertinggi proyek.

## DEC-0008 — `signs` adalah Tier C

**Status:** LOCKED  
**Keputusan:** Signs tidak memengaruhi skor utama dan hanya dapat dipakai sebagai eksperimen terpisah.  
**Alasan:** Brief pengguna menempatkannya pada Tier C meski sebagian materi internal memperlakukannya lebih dekat ke fitur pendukung.

## DEC-0009 — Intertype relations ditunda

**Status:** LOCKED  
**Keputusan:** Intertype relations hanya boleh dibahas setelah tipe cukup stabil dan tidak menjadi mesin penentuan tipe.  
**Alasan:** Kualitas hubungan nyata dipengaruhi banyak faktor dan klaim relasi belum tervalidasi secara memadai.

## DEC-0010 — Korelasi lintas tipologi tidak masuk scoring

**Status:** LOCKED  
**Keputusan:** Dokumen Polaris Australis hanya menjadi referensi sekunder dan bukti keberagaman komunitas.  
**Alasan:** Dokumen bersifat kompilasi subjektif, antarsekolah, dan memperingatkan agar sistem dipelajari terpisah.

## DEC-0011 — Tidak ada konversi MBTI

**Status:** LOCKED  
**Keputusan:** Huruf MBTI, fungsi MBTI, Enneagram, Psychosophy, AP, Big Five, atau sistem lain tidak boleh dikonversi langsung menjadi TIM.  
**Alasan:** Definisi, notasi, dan sasaran konstruk berbeda.

## DEC-0012 — Quadra adalah hipotesis nilai

**Status:** LOCKED  
**Keputusan:** Quadra diperlakukan sebagai pola valued information dan iklim interaksi, bukan penjumlahan elemen kuat atau jaminan kompatibilitas.  
**Alasan:** Mencegah quadra mengalahkan susunan Model A dan menghindari klaim relasi mutlak.

## DEC-0013 — PoLR tidak berasal dari nilai minimum

**Status:** LOCKED  
**Keputusan:** Indikasi PoLR memerlukan pola `threat`, rigidity, pain, shame, freeze, avoidance, dan kurangnya adaptasi; skor elemen rendah tidak cukup.  
**Alasan:** Low skill, kurang pengalaman, state, dan tidak tertarik dapat menghasilkan nilai rendah tanpa pola Vulnerable.

## DEC-0014 — Suggestive tidak berasal dari kelemahan

**Status:** LOCKED  
**Keputusan:** Indikasi Suggestive memerlukan `receiver`, relief, trust, seeking, dan kenyamanan saat dibantu.  
**Alasan:** Fungsi lemah dapat berada pada Role, PoLR, Suggestive, atau Mobilizing dengan pengalaman berbeda.

## DEC-0015 — Output pra-kalibrasi adalah indeks relatif

**Status:** LOCKED  
**Keputusan:** Sebelum validasi empiris, angka hasil disebut indeks kecocokan relatif, bukan probabilitas ilmiah atau akurasi.  
**Alasan:** Prior, likelihood, dan bobot teoritis belum terkalibrasi terhadap data.

## DEC-0016 — Browser-only dan local-first

**Status:** LOCKED  
**Keputusan:** Produk dibangun statis, tanpa backend, database online, autentikasi, API key, serverless API, pengunggahan data peserta, atau analytics invasif.  
**Alasan:** Privasi, kesederhanaan deployment, dan kesesuaian dengan brief.

## DEC-0017 — Foto diproses lokal

**Status:** LOCKED  
**Keputusan:** Foto Card Studio diproses di perangkat dan tidak dikirim ke jaringan. Penyimpanan persisten harus opsional.  
**Alasan:** Foto adalah data personal dan tidak diperlukan untuk scoring.

## DEC-0018 — Progress hanya dari gate lulus

**Status:** LOCKED  
**Keputusan:** Stage 00 memberi 4%; panjang dokumentasi tidak menambah progres di luar Gate 1.  
**Alasan:** Mencegah angka progres subjektif.

## DEC-0019 — Tidak ada aplikasi pada Tahap 00

**Status:** LOCKED  
**Keputusan:** Tahap 00 hanya menghasilkan dokumentasi governance; jumlah pertanyaan, scoring, app source, dan product test tetap nol.  
**Alasan:** Scope pengguna secara eksplisit melarang memulai aplikasi atau tahap berikutnya.

## DEC-0020 — Metadata peta riset dipertahankan

**Status:** LOCKED  
**Keputusan:** Nama file `peta_riset_socionics_180_rujukan.pdf` dipertahankan dalam provenance, sedangkan isi dirujuk sebagai peta 208 entri.  
**Alasan:** Nama file dan judul internal berbeda; keduanya perlu dicatat jujur.

## DEC-0021 — File FROZEN membutuhkan migrasi

**Status:** LOCKED  
**Keputusan:** `PROJECT_CONSTITUTION.md` dan `MEASUREMENT_PRINCIPLES.md` tidak dapat diubah langsung pada tahap berikutnya.  
**Alasan:** Menjaga kontrak domain dari drift implementasi.

## DEC-0022 — Test yang tidak relevan tidak boleh diklaim

**Status:** LOCKED  
**Keputusan:** Typecheck, lint, Vitest, React Testing Library, dan build dicatat not applicable pada Tahap 00.  
**Alasan:** Codebase belum dibuat; klaim kelulusan akan menyesatkan.
