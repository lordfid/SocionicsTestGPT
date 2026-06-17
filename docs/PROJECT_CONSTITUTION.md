# Konstitusi Proyek — Socionics Dalam Diriku

**Versi:** 1.0.0  
**Tanggal dikunci:** 17 Juni 2026  
**Status:** FROZEN  
**Tahap asal:** 00 — Konstitusi proyek, pembacaan referensi, dan sistem progres

## 1. Fungsi dokumen

Dokumen ini adalah otoritas tertinggi proyek setelah instruksi eksplisit pengguna. Semua keputusan desain, domain, pengukuran, implementasi, pengujian, UI, penyimpanan, dan packaging harus konsisten dengannya.

Urutan otoritas:

1. Instruksi eksplisit pengguna yang terbaru.
2. `docs/PROJECT_CONSTITUTION.md`.
3. Keputusan terkunci dalam `docs/DECISIONS.md`.
4. Prinsip pengukuran dalam `docs/MEASUREMENT_PRINCIPLES.md`.
5. Matriks referensi dan dokumen proses.
6. Implementasi kode dan data.

Perubahan terhadap dokumen FROZEN hanya sah melalui migrasi tertulis yang menjelaskan alasan, dampak, risiko, file terdampak, test yang harus berubah, dan nomor keputusan baru.

## 2. Identitas dan tujuan produk

Nama produk pada seluruh UI adalah **Socionics Dalam Diriku**.

Produk ini adalah alat pendidikan, refleksi diri, dan eksplorasi tipologi Socionics. Produk tidak boleh diposisikan sebagai diagnosis klinis, pengukur kecerdasan, penentu nilai manusia, penentu kelayakan kerja, atau instrumen profesional tervalidasi.

Tujuan metodologisnya adalah memperkirakan kecocokan relatif pola respons terhadap 16 TIM melalui Model A sebagai model kandidat lengkap, sambil mempertahankan ketidakpastian, bukti penyangkal, kualitas respons, dan kemungkinan pengaruh konteks.

## 3. Batas ilmiah yang wajib tampil

Aplikasi harus menjelaskan secara mudah dipahami bahwa:

- Socionics adalah kerangka tipologi dan refleksi.
- Socionics bukan diagnosis klinis.
- Hasil bukan ukuran kecerdasan, moralitas, kesehatan mental, atau nilai manusia.
- Socionics belum merupakan instrumen ilmiah mapan yang setara dengan alat klinis tervalidasi.
- Bobot awal dan expected profile bersifat teoritis sampai dikalibrasi dengan data.
- Persentase atau indeks yang ditampilkan adalah kecocokan relatif dalam model aplikasi, bukan probabilitas ilmiah yang telah tervalidasi.
- Validasi nyata membutuhkan data responden, pemeriksaan validitas isi, cognitive interviewing, analisis item, test-retest, person-fit, pemeriksaan lintas budaya, dan evaluasi model alternatif.

Aplikasi tidak boleh digunakan untuk seleksi kerja, hukuman, keputusan medis, keputusan hukum, keputusan pendidikan berisiko tinggi, atau penilaian kecocokan hubungan secara mutlak.

## 4. Hierarki pengetahuan Socionics

### Tier A — fondasi utama

Boleh membentuk kontrak domain dan expected profile awal:

- delapan information elements;
- Model A;
- delapan posisi fungsi;
- strong versus weak;
- valued versus unvalued;
- blok Ego, Super-ego, Super-id, dan Id;
- 16 TIM;
- quadra sebagai hipotesis pola nilai dan iklim informasi.

Tier A adalah fondasi teoritis aplikasi, bukan bukti bahwa struktur tersebut telah tervalidasi secara independen.

### Tier B — dukungan terbatas dan terkalibrasi

Boleh membantu interpretasi atau diskriminasi setelah fondasi utama stabil:

- dimensionality;
- mental versus vital;
- accepting versus producing;
- inert versus contact;
- club;
- temperament Socionics;
- intertype relations setelah tipe cukup stabil.

Komponen Tier B tidak boleh mengalahkan pola Model A yang lebih lengkap hanya karena satu indikator cocok.

### Tier C — eksperimental

Harus dipisahkan dari skor utama:

- signs;
- Reinin dichotomies;
- DCNH;
- romance styles;
- cognitive styles;
- small groups selain yang benar-benar diperlukan.

Komponen Tier C hanya boleh muncul sebagai eksperimen berlabel jelas, setelah ada keputusan tahap khusus dan test pemisahan dari skor inti.

### Tier D — bukan bukti utama

Tidak boleh memengaruhi scoring inti:

- visual typing;
- bentuk tubuh;
- celebrity typing;
- stereotip profesi;
- integral type bangsa;
- klaim kompatibilitas mutlak;
- konversi langsung MBTI menjadi Socionics.

## 5. Aturan referensi lintas tipologi

Dokumen korelasi lintas tipologi hanya boleh digunakan untuk:

- menunjukkan bahwa korelasi komunitas beragam;
- menunjukkan perbedaan antarsekolah;
- menjadi materi referensi sekunder;
- memperingatkan bahwa tiap sistem harus dipelajari dengan kontraknya sendiri.

Dokumen korelasi tidak boleh:

- memberi bobot TIM;
- menghapus kandidat TIM;
- membuat kombinasi tertentu mustahil;
- mengubah Model A;
- menjadi sumber direct type hint;
- mengonversi MBTI, Enneagram, Psychosophy, AP, Big Five, atau sistem lain menjadi Socionics.

## 6. Prinsip pengukuran konstitusional

Aplikasi wajib membedakan sekurang-kurangnya:

- kemampuan;
- otomatisitas;
- fleksibilitas;
- kenyamanan;
- penghargaan terhadap informasi;
- perilaku karena tuntutan sosial;
- rasa sakit atau ancaman;
- kelegaan ketika dibantu;
- aspirasi dan kebutuhan pengakuan;
- kompetensi yang dianggap bukan inti;
- kemampuan otomatis di latar belakang;
- state situasional;
- social-role mask;
- response style;
- noise.

Delapan kanal bukti permanen adalah:

1. `producer`
2. `flexible`
3. `mask`
4. `threat`
5. `receiver`
6. `aspiration`
7. `dismissive`
8. `background`

Nama kanal adalah kontrak domain. Perubahan nama atau maknanya memerlukan migrasi.

Aplikasi tidak boleh menyimpulkan bahwa:

- elemen tertinggi otomatis Base;
- elemen terendah otomatis PoLR;
- elemen lemah otomatis Suggestive;
- kemampuan kerja otomatis fungsi utama;
- satu jawaban menentukan tipe;
- satu korelasi tipologi membatalkan tipe.

Semua 16 TIM harus dibandingkan sebagai 16 model kandidat lengkap.

## 7. Privasi dan arsitektur teknologi

Teknologi yang diizinkan:

- React;
- TypeScript;
- Vite;
- CSS biasa atau CSS Modules;
- localStorage atau IndexedDB hanya bila diperlukan;
- Vitest;
- React Testing Library;
- ESLint;
- static deployment;
- pemrosesan foto lokal;
- Web Share API dengan fallback.

Teknologi dan praktik yang dilarang:

- backend;
- database online;
- API key;
- autentikasi;
- Firebase;
- Supabase;
- serverless API;
- pengunggahan data peserta;
- model generatif eksternal;
- analytics invasif.

Data peserta harus tetap di perangkat. Foto tidak boleh dikirim ke jaringan. Penyimpanan foto harus bersifat opsional dan dijelaskan secara transparan.

## 8. Identitas UI yang dilarang

UI tidak boleh menampilkan nama penyedia model, platform generatif, atau label yang membuat produk tampak sebagai keluaran alat generatif. Larangan ini mencakup nama dan frasa yang disebut eksplisit dalam brief Tahap 00, serta variasi kapitalisasinya.

UI juga tidak boleh memakai label yang merendahkan status produk sebagai contoh sementara, arena percobaan, atau purwarupa.

## 9. Aturan bahasa

Teks UI harus:

- natural dan jelas;
- tidak kaku;
- tidak sok puitis;
- tidak terdengar seperti promosi;
- tidak terlalu santai;
- tidak menghakimi;
- tidak diagnostik;
- tidak menjanjikan kepastian;
- bervariasi menurut fungsi komponen dan makna hasil.

Contoh kalimat dalam dokumentasi tidak boleh dijadikan template yang disalin berulang ke seluruh tipe. Narasi harus berasal dari bukti hasil, bukan dari pergantian nama tipe pada paragraf yang sama.

## 10. Aturan kualitas kode dan data

Tidak boleh ada:

- placeholder;
- TODO;
- pseudocode;
- fungsi kosong;
- data palsu sementara;
- import rusak;
- file tidak digunakan;
- komentar yang menunda implementasi;
- instruksi agar pengguna melengkapi sendiri;
- elipsis yang menggantikan implementasi;
- hasil random;
- hardcode hasil berdasarkan identitas peserta;
- klaim command berhasil tanpa eksekusi nyata.

Setiap file harus memiliki tujuan, pemilik domain, dependensi yang sah, dan test atau verifikasi yang sesuai.

## 11. Status file

### FROZEN

Tidak boleh diubah tanpa migrasi dan alasan teknis tertulis.

### CONTROLLED

Boleh diubah setelah dampak dianalisis, keputusan dicatat, dan test yang relevan diperbarui.

### ACTIVE

Menjadi fokus tahap berjalan dan dapat berubah dalam batas scope tahap.

Status setiap file dicatat di `docs/FILE_MANIFEST.md`.

## 12. Perfection Loop

Setiap tahap harus melewati:

1. **PASS 1 — Implementasi:** menyelesaikan ruang lingkup tahap.
2. **PASS 2 — Self-review:** mencari kesalahan, repetisi, inkonsistensi, import rusak, dan kedangkalan.
3. **PASS 3 — Adversarial review:** mencoba membuktikan hasil salah atau rapuh.
4. **PASS 4 — Repair:** memperbaiki temuan yang masih berada dalam scope.
5. **PASS 5 — Verification:** menjalankan test, typecheck, lint, build, atau verifikasi dokumentasi yang relevan.

Sebuah tahap tidak boleh dinyatakan selesai bila satu lintasan belum dilakukan.

## 13. Gate dan progres

Bobot proyek:

| Gate | Bobot |
|---|---:|
| Referensi dan konstitusi | 4% |
| Fondasi proyek dan kontrak domain | 8% |
| Schema pertanyaan dan audit | 5% |
| Bank pertanyaan inti | 24% |
| Holdout dan tie-break | 5% |
| Scoring dan model comparison | 20% |
| Anti-mistype, adaptive, dan confidence | 8% |
| Profil serta narasi hasil | 8% |
| UI, session, dan storage | 7% |
| Card Studio | 7% |
| QA, accessibility, packaging | 4% |
| **Total** | **100%** |

Progres hanya bertambah ketika acceptance criteria gate lulus. Banyaknya file, panjang kode, atau tampilan visual tidak menambah progres dengan sendirinya.

## 14. Definition of Done proyek

Proyek baru dapat dinyatakan 100% ketika:

- seluruh gate lulus;
- tidak ada gate gagal yang disembunyikan;
- seluruh command final berhasil dijalankan;
- coverage domain dan pertanyaan lulus audit;
- scoring lolos synthetic vectors dan adversarial cases;
- UI lolos aksesibilitas dasar, responsivitas, storage, dan export;
- tidak ada import rusak, fungsi kosong, data sementara, atau file tak terpakai;
- batas ilmiah dan privasi tampil jelas;
- paket final dapat dibangun dan dipakai secara statis.
