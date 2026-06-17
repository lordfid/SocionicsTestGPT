# Test Strategy — Socionics Dalam Diriku

**Versi:** 1.0.0  
**Tanggal:** 17 Juni 2026  
**Status:** CONTROLLED  
**Tahap asal:** 01 — Arsitektur teknis dan manifest proyek

## 1. Tujuan

Strategi ini menetapkan cara membuktikan kontrak, dependency, determinisme, pemisahan holdout, keamanan storage, dan perilaku UI. Coverage angka tidak boleh menggantikan pengujian invariant dan adversarial cases.

Tahap 01 hanya merancang strategi. Tidak ada test produk yang dibuat atau diklaim lulus.

## 2. Prinsip pengujian

1. Test mengikuti risk, bukan hanya struktur folder.
2. Pure domain dan scoring diuji tanpa React, DOM, storage, atau clock nyata.
3. Setiap bug yang diperbaiki harus mendapat regression test.
4. Fixtures sintetis berada di `tests/fixtures`, tidak di production source.
5. Production source tidak mengimpor test helper atau fixture.
6. Test tidak bergantung pada urutan eksekusi.
7. Randomized behavior memakai seed eksplisit dan melaporkan seed pada failure.
8. Snapshot test tidak dipakai untuk mengesahkan logika scoring.
9. Holdout isolation diuji sebagai invariant arsitektur.
10. Test failure tidak boleh diturunkan menjadi warning untuk meloloskan gate.

## 3. Lapisan test

### 3.1 Static and architecture checks

Menguji:

- TypeScript strictness;
- lint rules;
- import boundaries;
- tidak ada dependency cycle;
- tidak ada direct import ke internal module;
- production source tidak mengimpor `tests` atau `audit` runtime;
- scoring tidak mengimpor UI/storage/card/questions data;
- card tidak mengimpor scoring;
- correlation reference content tidak dapat masuk scoring;
- manifest file sesuai filesystem.

Tools utama:

- TypeScript compiler;
- ESLint `no-restricted-imports` dan rules terkait;
- dependency graph checker yang dijalankan dari test/audit;
- manifest verification script.

### 3.2 Domain unit tests

Menguji finite sets dan invariant:

- tepat delapan information elements;
- tepat delapan evidence channels dengan nama yang dikunci;
- tepat delapan Model A positions;
- blok, strong/weak, valued/unvalued, mental/vital derivation konsisten;
- tepat 16 TIM identifiers;
- IDs dan version identifiers valid;
- stable sort total ordering;
- seeded random reproducibility;
- `Math.random` tidak digunakan pada core paths.

Untuk finite domain tables, targetnya exhaustive assertions, bukan sampling.

### 3.3 Question contract tests

Menguji:

- item schema;
- option schema;
- unique item IDs across all phases;
- phase separation;
- exact production counts ketika bank selesai: 192 core, 32 holdout, 32 tie-break;
- no direct TIM labels pada participant-visible fields;
- each option evidence payload valid;
- registry version compatibility;
- seeded order stable;
- adaptive selector hanya memilih eligible item;
- selector tidak memilih holdout saat core/tie-break;
- no exhausted-item repeat kecuali policy eksplisit.

Question content quality memerlukan audit manual dan cognitive interviewing; unit tests tidak dapat membuktikan naturalness atau construct validity.

### 3.4 Scoring unit and contract tests

Menguji:

- functions pure terhadap input;
- no mutation;
- identical input + version menghasilkan identical output;
- 16 candidates selalu dibandingkan;
- 64 expected cells per candidate schema lengkap;
- evidence map memiliki 8 × 8 cells;
- support dan contradiction trace kembali ke source IDs;
- numeric outputs finite;
- stable ordering pada ties;
- holdout observations ditolak dari primary aggregation;
- card/photo/storage metadata tidak memengaruhi score;
- cross-system fields tidak diterima sebagai input;
- confidence tidak dapat melebihi policy ketika person-fit buruk, setelah formula tersedia;
- invalid candidate model menyebabkan failure, bukan fallback.

Formula atau expected values baru diuji setelah Gate 6 menyetujuinya.

### 3.5 Session state machine tests

Menguji event dan transition table:

- idle → mode-selected → core-active;
- pause/resume tanpa kehilangan answer;
- answer hanya untuk presented item;
- back/revision menghasilkan latest valid answer;
- tie-break hanya setelah valid entry condition;
- primary lock terjadi sebelum holdout;
- holdout tidak mengubah primary lock;
- finalize idempotent;
- reload dari checkpoint menghasilkan state yang sama;
- storage failure mengaktifkan memory-only warning tanpa mengubah score;
- reset menghapus resource yang diminta saja.

State transition tests menggunakan table-driven vectors.

### 3.6 Storage contract tests

Adapter diuji terhadap contract yang sama:

- save/read round trip;
- schema version envelope;
- migration berurutan;
- record asal dipertahankan bila migration gagal;
- corrupt JSON;
- missing required field;
- unknown newer version;
- quota exceeded;
- storage unavailable;
- namespace deletion;
- photo tidak disimpan tanpa opt-in;
- result and session versions tidak tertukar.

Browser storage di unit test memakai controlled fake yang meniru failure, bukan sekadar happy-path mock.

### 3.7 Result and profile tests

Menguji:

- result snapshot immutable;
- version metadata lengkap;
- scientific limitation selalu hadir;
- narrative builder tidak mengubah candidate ordering;
- narrative provenance tersedia;
- no cross-system inference;
- different result facets dapat menghasilkan struktur narasi yang bervariasi;
- incomplete profile data fails build/audit;
- CardInput tidak mengandung raw answers.

Kualitas bahasa tetap membutuhkan review manusia terpisah.

### 3.8 Card tests

Menguji:

- render spec menerima ukuran eksplisit;
- output tidak membaca viewport;
- portrait, square, dan story dimensions benar;
- same CardInput + RenderSpec menghasilkan layout decisions yang sama;
- text overflow detected;
- font readiness handling;
- photo decode/crop failure;
- Object URL cleanup;
- Blob export;
- Web Share support, rejection, dan cancellation;
- fallback download/text;
- card changes tidak mengubah result snapshot.

Pixel-perfect image comparison dipakai terbatas karena Canvas/font dapat berbeda antar-runtime. Structural layout assertions dan golden tests hanya dijalankan pada environment yang dipin.

### 3.9 React component tests

Menggunakan React Testing Library untuk perilaku peserta:

- keyboard navigation;
- focus management;
- screen reader names;
- progress semantics;
- error recovery;
- resume flow;
- answer selection and revision;
- route protection berdasarkan session state;
- reduced motion behavior;
- theme persistence;
- Card Studio fallback;
- no participant data printed to error UI.

Test harus memilih elemen melalui role/name bila memungkinkan, bukan class selector internal.

### 3.10 Integration tests

Menguji rangkaian modul dengan data sintetis:

- create session → present → answer → aggregate → compare → lock → holdout → result;
- reload at each phase;
- deterministic replay from reproducibility record;
- corrupt persisted record recovery;
- deployment version change during lazy load;
- result → card input → export fallback;
- no network request containing participant data.

### 3.11 Manual verification

Diperlukan untuk hal yang tidak cukup dibuktikan otomatis:

- bahasa natural dan tidak menghakimi;
- mobile and desktop responsive behavior;
- 200% zoom;
- screen reader smoke test;
- keyboard-only end-to-end;
- reduced motion;
- high contrast and dark/light appearance;
- Android browser download/share behavior;
- foto besar dan orientasi EXIF;
- static deployment route refresh;
- offline interruption behavior setelah asset dimuat;
- clear-all-data behavior.

Hasil manual dicatat per browser/device, bukan dinyatakan lulus secara umum tanpa bukti.

## 4. Test data isolation

### 4.1 Production data

Hanya berada di:

- `src/questions/data`;
- `src/scoring/models`;
- `src/profiles/data`;
- static content yang memang digunakan aplikasi.

### 4.2 Test fixtures

Hanya berada di `tests/fixtures` atau dibuat inline dalam test. Fixture harus:

- jelas sintetis;
- tidak berpura-pura menjadi item produksi;
- tidak disertakan ke production registry;
- memakai ID prefix khusus test;
- tidak digunakan untuk menutup kekurangan production data.

### 4.3 No fixture leakage

Build/audit harus memeriksa bahwa bundle production tidak mengandung path `tests/fixtures` dan production registry tidak mengenali test IDs.

## 5. Deterministic test policy

- setiap test random menerima seed literal;
- failure message mencetak seed non-sensitif;
- fake clock dipakai untuk timestamp behavior;
- locale dan timezone tidak memengaruhi scoring assertions;
- stable sorting diuji pada ties;
- object key order tidak dipakai sebagai oracle;
- no test bergantung pada current date;
- generated session seed dari browser boundary diuji dengan injected fake entropy source.

## 6. Adversarial test catalogue

### 6.1 Typing logic attacks

- satu jawaban ekstrem mencoba mengunci TIM;
- semua jawaban pada satu information element tinggi;
- elemen minimum dipaksa menjadi PoLR;
- skill kerja tinggi tetapi valued signal rendah;
- mask tinggi disalahartikan sebagai producer;
- receiver tinggi disalahartikan sebagai low competence;
- background tinggi disalahartikan sebagai conscious preference;
- contradictory response patterns;
- missing response concentration pada satu channel.

### 6.2 Data quality attacks

- repeated same option position;
- maximum skip;
- monotonic response;
- alternating pattern;
- answer revisions berulang;
- unrealistically fast metadata bila timing policy kelak aktif;
- sparse evidence;
- equal candidate scores;
- one phase entirely missing.

Test hanya memastikan policy bekerja; ia tidak memberi label moral kepada peserta.

### 6.3 Architecture attacks

- scoring import mencoba mengambil localStorage;
- card import mencoba mengambil scoring output internal;
- question data import React component;
- session imports storage adapter;
- UI imports internal candidate weights;
- correlation content imported by scoring;
- production imports test fixture;
- holdout item inserted into core registry.

Semua harus menghasilkan lint/test/build failure.

### 6.4 Persistence attacks

- partial record;
- wrong version;
- stale lock;
- missing seed;
- duplicated item ID;
- write denied after answer;
- migration throws halfway;
- maliciously large local record;
- invalid photo draft reference.

### 6.5 Card and share attacks

- unsupported image;
- huge image dimensions;
- zero-sized render spec;
- very long optional display name;
- missing font;
- share cancellation;
- share capability changes between checks;
- download blocked;
- route reload during export.

## 7. Coverage policy

Coverage adalah diagnostic, bukan satu-satunya gate.

Target awal saat codebase tersedia:

- domain finite invariants: **100% branch pada tabel/invariant kritis**;
- seeded determinism, state machine, holdout isolation, version migration: **100% branch pada jalur kritis**;
- pure scoring modules: minimal **95% statements** dan **90% branches**, sambil mewajibkan adversarial vectors;
- keseluruhan source yang dapat diuji unit: minimal **90% statements** dan **85% branches** sebelum final release;
- UI coverage tidak boleh dikejar dengan snapshot dangkal; behavior kritis harus memiliki assertions.

Threshold dapat dinaikkan. Penurunan membutuhkan keputusan baru dan alasan teknis.

## 8. Canonical commands

| Command | Expected runner | Gate use |
|---|---|---|
| `npm run dev` | Vite dev server | manual development, bukan bukti gate sendiri |
| `npm run typecheck` | TypeScript compiler tanpa emit | setiap tahap kode |
| `npm run lint` | ESLint | setiap tahap kode |
| `npm run test` | Vitest run mode | setiap tahap yang memiliki test |
| `npm run coverage` | Vitest coverage | gate 2 onward sesuai scope |
| `npm run build` | TypeScript build + Vite production build | setiap tahap kode yang mengubah bundle |

Tambahan yang boleh dibuat bila digunakan:

- `npm run test:watch` untuk development;
- `npm run audit` untuk checks proyek;
- `npm run verify` sebagai agregator command, tanpa menggantikan laporan command individual.

## 9. Perintah dan klaim pada Tahap 01

Karena bootstrap kode dilarang:

- `npm run dev`: not available;
- `npm run typecheck`: not available;
- `npm run lint`: not available;
- `npm run test`: not available;
- `npm run coverage`: not available;
- `npm run build`: not available.

Hanya pemeriksaan dokumentasi dan filesystem yang relevan. Tidak ada test produk yang diklaim lulus.

## 10. Gate mapping

| Gate | Bukti test utama |
|---|---|
| Gate 2 | toolchain, domain contracts, Model A invariants, import boundaries, build |
| Gate 3 | question schema validators dan audit contracts |
| Gate 4 | exact counts, coverage, balance, wording/manual review |
| Gate 5 | holdout/tie-break separation, leakage tests, test vectors |
| Gate 6 | candidate completeness, pure scoring, determinism, adversarial vectors |
| Gate 7 | adaptive policy, person-fit, confidence constraints |
| Gate 8 | narrative provenance, variation, scientific limitations |
| Gate 9 | session/storage/UI integration, accessibility behavior |
| Gate 10 | render/export/share/photo matrix |
| Gate 11 | full suite, manual matrix, static deploy, package audit |

## 11. Release-blocking failures

Selalu memblokir gate terkait:

- typecheck failure;
- lint error pada dependency boundary;
- failed unit/integration test;
- build failure;
- dependency cycle;
- missing/duplicate production item;
- holdout leakage;
- non-deterministic replay;
- scoring result dengan invalid input;
- migration data loss;
- Card Studio mengubah result;
- correlation data masuk scoring;
- frozen file berubah tanpa migration;
- accessibility blocker pada alur utama;
- static route refresh failure pada target deployment.

## 12. Perfection Loop integration

Pada setiap tahap:

1. **Implementasi:** tambah test bersama perubahan, bukan sesudahnya.
2. **Self-review:** lihat untested branch, brittle fixture, dan false positive.
3. **Adversarial review:** jalankan attack catalogue yang relevan.
4. **Repair:** perbaiki implementation dan test; jangan melonggarkan assertion agar hijau.
5. **Verification:** jalankan command nyata dan catat exit code, jumlah test, coverage, warning, serta manual checks.
