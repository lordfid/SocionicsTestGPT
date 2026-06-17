# Decisions

**Versi dokumen:** 1.1.0  
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

## DEC-0023 — Modular monolith browser-only

**Status:** LOCKED  
**Keputusan:** Aplikasi memakai modular monolith React yang dibangun sebagai static SPA dengan pure domain core, application modules, infrastructure adapters, serta presentation/composition layer.  
**Alasan:** Memberi isolasi yang dapat diuji tanpa menambah backend, service boundary palsu, atau kompleksitas deployment.

## DEC-0024 — Arah dependency tunggal dan public API

**Status:** LOCKED  
**Keputusan:** Cross-module import hanya melalui public API atau contract path yang dinyatakan stabil. Production module tidak boleh mengimpor `audit` atau `tests`.  
**Alasan:** Mencegah siklus, coupling ke internal file, dan perubahan diam-diam pada kontrak.

## DEC-0025 — Domain tanpa dependency keluar

**Status:** LOCKED  
**Keputusan:** `domain` tidak bergantung pada React, DOM, browser storage, question data, scoring implementation, result, card, UI, audit, atau tests.  
**Alasan:** Invariant Model A dan kontrak pengukuran harus dapat diuji sebagai pure core.

## DEC-0026 — Scoring pure dan menerima normalized observations

**Status:** LOCKED  
**Keputusan:** Scoring tidak membaca bank pertanyaan, UI, route, storage, clock, device, viewport, foto, atau correlation data. Scoring menerima normalized observations dan versioned candidate models melalui input eksplisit.  
**Alasan:** Menjaga determinisme, auditability, dan pemisahan data dari engine.

## DEC-0027 — Session mengorkestrasi melalui port

**Status:** LOCKED  
**Keputusan:** `session` menjadi coordinator alur questions dan scoring. Persistence dipanggil melalui `SessionStorePort`; `session` tidak mengimpor concrete storage adapter.  
**Alasan:** Storage failure tidak boleh mencemari state machine atau membuat session sulit diuji.

## DEC-0028 — Primary result dikunci sebelum holdout

**Status:** LOCKED  
**Keputusan:** Core dan tie-break membentuk primary ranking lock sebelum holdout dinilai. Holdout menghasilkan laporan konsistensi dan tidak mengubah primary ranking pada arsitektur awal.  
**Alasan:** Mencegah leakage dan penggunaan holdout sebagai data pelatihan terselubung.

## DEC-0029 — Randomness inti harus seeded

**Status:** LOCKED  
**Keputusan:** Browser crypto hanya membuat seed pada boundary. Pure core menerima `RandomSource`; `Math.random()` dilarang pada domain, selection, scoring, session, audit, dan card layout.  
**Alasan:** Urutan dan hasil harus dapat direproduksi dari seed, versi, dan jawaban yang sama.

## DEC-0030 — Storage memakai versioned envelope

**Status:** LOCKED  
**Keputusan:** Semua record persisten memiliki schema version, resource type, timestamps, app version, dan payload tervalidasi. Migration harus pure dan mempertahankan record asal sampai hasil baru terverifikasi.  
**Alasan:** Resume dan upgrade tidak boleh bergantung pada field guessing atau overwrite berisiko.

## DEC-0031 — Foto memory-only secara default

**Status:** LOCKED  
**Keputusan:** Foto Card Studio diproses melalui memory/Object URL dan tidak dipersistenkan secara default. IndexedDB hanya boleh digunakan setelah opt-in eksplisit.  
**Alasan:** Foto tidak diperlukan untuk pengukuran dan memiliki risiko privasi serta ukuran storage lebih tinggi.

## DEC-0032 — Card Studio menerima proyeksi hasil

**Status:** LOCKED  
**Keputusan:** Card Studio hanya menerima immutable `CardInput`. Renderer menerima ukuran output eksplisit dan tidak membaca viewport untuk menentukan hasil ekspor.  
**Alasan:** Perubahan foto, crop, warna, format, atau viewport tidak boleh mengubah scoring maupun layout file secara tidak terkontrol.

## DEC-0033 — Route dan data berat di-lazy-load

**Status:** LOCKED  
**Keputusan:** Assessment, result, references, Card Studio, profile narratives, candidate model data, serta photo/export modules dipisahkan menjadi chunk yang relevan. Critical shell dan recovery UI tetap eager.  
**Alasan:** Mengurangi initial bundle tanpa membuat pemulihan bergantung pada chunk yang sama-sama gagal.

## DEC-0034 — Test fixtures terpisah dari production data

**Status:** LOCKED  
**Keputusan:** Fixture sintetis hanya berada di `tests/fixtures` atau test file. Production registry dan bundle dilarang mengimpor fixture.  
**Alasan:** Data tes tidak boleh menyamarkan bank produksi yang belum lengkap atau bocor ke peserta.

## DEC-0035 — Struktur batch bank final

**Status:** LOCKED  
**Keputusan:** Kapasitas final bank adalah 12 file core × 16 item, 4 file holdout × 8 item, dan 4 file tie-break × 8 item.  
**Alasan:** Memberi jumlah persis 192/32/32 dengan review dan diff yang terkendali.

## DEC-0036 — Candidate expectation berbentuk 64 cell

**Status:** LOCKED  
**Keputusan:** Setiap kandidat TIM kelak memiliki schema 8 information elements × 8 evidence channels, yaitu 64 expected cells. Nilai cell belum ditetapkan pada Tahap 01.  
**Alasan:** Bentuk ini mempertahankan delapan kanal permanen dan mencegah scoring berubah menjadi ranking elemen tunggal.

## DEC-0037 — Error tidak boleh menghasilkan hasil pengganti

**Status:** LOCKED  
**Keputusan:** Invalid scoring input, holdout contamination, candidate model tidak lengkap, atau numeric failure menghentikan result assembly. Tidak ada default, random, atau last-known type fallback.  
**Alasan:** Hasil yang tidak dapat dipercaya lebih berbahaya daripada kegagalan yang dijelaskan jujur.

## DEC-0038 — Canonical npm commands

**Status:** LOCKED  
**Keputusan:** Bootstrap harus menyediakan `dev`, `typecheck`, `lint`, `test`, `coverage`, dan `build` dengan exit code nyata.  
**Alasan:** Command lintas tahap harus konsisten dan dapat diverifikasi.

## DEC-0039 — Browser history dengan static rewrite

**Status:** LOCKED  
**Keputusan:** Router menggunakan browser history dan target static host menyediakan rewrite route aplikasi ke `index.html`; tidak ada API route.  
**Alasan:** URL tetap bersih sekaligus mempertahankan deployment statis.

## DEC-0040 — Tahap 01 tidak meluluskan Gate 2

**Status:** LOCKED  
**Keputusan:** Selesainya arsitektur dan manifest adalah prerequisite internal Gate 2, tetapi Gate 2 tetap IN PROGRESS sampai bootstrap, kontrak domain, mapping Model A, tests, lint, typecheck, coverage relevan, dan build lulus. Progres tetap 4%.  
**Alasan:** Progres hanya bertambah dari gate penuh yang lulus, bukan dari substage dokumentasi.


## DEC-0041 — Bootstrap memakai app, theme, dan ui boundary

**Status:** LOCKED  
**Keputusan:** Shell Tahap 02 dibagi menjadi `src/app` untuk composition/router/error boundary, `src/theme` untuk state dan kontrak tema, serta `src/ui` untuk route dan komponen presentasi. Folder domain lain tidak dibuat sebelum mempunyai implementasi nyata.  
**Alasan:** Struktur mengikuti dependency direction tanpa membuat barrel kosong atau file dekoratif.

## DEC-0042 — Konfigurasi dasar TypeScript dibekukan

**Status:** LOCKED  
**Keputusan:** Root project references, strict production config, strict Node config, strict test config, alias `@/*`, `noUncheckedIndexedAccess`, dan `exactOptionalPropertyTypes` menjadi baseline FROZEN setelah Tahap 02.  
**Alasan:** Perubahan compiler semantics dapat mengubah seluruh contract dan harus diperlakukan sebagai migrasi.

## DEC-0043 — Struktur command package dibekukan

**Status:** LOCKED  
**Keputusan:** `dev`, `typecheck`, `lint`, `test`, `coverage`, dan `build` tidak boleh dihapus atau diubah maknanya. Command tambahan boleh dibuat bila mempunyai penggunaan nyata.  
**Alasan:** Semua tahap kode memerlukan interface verifikasi yang konsisten.

## DEC-0044 — Core lint rules dibekukan

**Status:** LOCKED  
**Keputusan:** Typed TypeScript lint, React Hooks rules, zero-warning policy, production import ban terhadap tests/audit, serta larangan `Math.random` langsung menjadi baseline. Aturan dapat diperketat secara aditif; pelemahan memerlukan keputusan migrasi.  
**Alasan:** Boundary dan determinisme tidak boleh hanya menjadi dokumentasi.

## DEC-0045 — Route berat memakai static lazy mapping

**Status:** LOCKED  
**Keputusan:** Page routes dimuat melalui dynamic import yang path-nya statis dan dapat dianalisis Vite. Shell, provider, root error boundary, route error UI, dan loading UI tetap eager.  
**Alasan:** Mendukung code splitting tanpa input-driven import path dan tetap menyediakan recovery ketika chunk gagal.

## DEC-0046 — Coverage baseline Tahap 02

**Status:** LOCKED  
**Keputusan:** Bootstrap menetapkan threshold 90% statements, 80% branches, 90% functions, dan 90% lines untuk source aktif. Target domain kritis pada tahap berikutnya tetap mengikuti threshold yang lebih ketat dalam `TEST_STRATEGY.md`.  
**Alasan:** Threshold cukup tinggi untuk shell tanpa menyamarkan fakta bahwa domain belum ada.

## DEC-0047 — Theme preference adalah satu-satunya persistence Tahap 02

**Status:** LOCKED  
**Keputusan:** Shell hanya menyimpan pilihan `system`, `light`, atau `dark` pada localStorage. Kegagalan storage tidak memblokir aplikasi. Tidak ada jawaban, identitas, foto, sesi, atau hasil yang disimpan.  
**Alasan:** Theme merupakan preferensi UI sederhana dan tidak boleh menjadi pintu masuk penyimpanan data peserta sebelum kontraknya tersedia.

## DEC-0048 — Manifest tidak berarti service worker

**Status:** LOCKED  
**Keputusan:** Tahap 02 menyediakan manifest dan icon lokal, tetapi tidak mendaftarkan service worker atau mengklaim offline installability penuh.  
**Alasan:** Service worker menambah versioning dan stale-chunk risk yang belum berada dalam scope.

## DEC-0049 — Target folder tidak dibuat kosong

**Status:** LOCKED  
**Keputusan:** Folder `domain`, `questions`, `scoring`, `profiles`, `session`, `storage`, `result`, `card`, dan `audit` dibuat hanya ketika tahap pemiliknya menghasilkan file yang digunakan dan diuji.  
**Alasan:** Empty directory, `.gitkeep`, atau barrel kosong tidak memberi kemampuan dan melanggar aturan file harus memiliki fungsi.

## DEC-0050 — Tahap 02 lulus tanpa meluluskan Gate 2

**Status:** LOCKED  
**Keputusan:** Bootstrap, shell, tests, coverage, build, dan dev smoke lulus. Gate 2 tetap IN PROGRESS dan progres tetap 4% sampai kontrak domain serta mapping Model A seluruh 16 TIM lulus.  
**Alasan:** Bobot progres diberikan hanya pada gate penuh, bukan substage teknis.
