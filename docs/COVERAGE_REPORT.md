# Coverage Report — Tahap 02

**Versi:** 3.0.0  
**Tanggal:** 17 Juni 2026  
**Status:** CONTROLLED

## 1. Scope

Tahap 02 mengukur bootstrap dan shell saja. Angka coverage tidak mencakup domain Socionics, question bank, scoring, profiles, session engine, result, atau Card Studio karena modul tersebut belum dibuat.

## 2. Acceptance Tahap 02

| Kriteria | Status | Bukti |
|---|---|---|
| `npm install` nyata dan lockfile konsisten | PASS | 253 package added; 254 audited; 0 vulnerability saat install |
| TypeScript strict | PASS | `npm run typecheck`, exit 0 |
| ESLint | PASS | `npm run lint`, exit 0, zero warnings |
| Vitest | PASS | 6 suite dan 21 test lulus |
| Coverage | PASS | threshold terlampaui |
| Production build | PASS | 41 module transformed |
| Dev server smoke | PASS | `/` dan `/status` HTTP 200 |
| Static-only Vercel config | PASS | filesystem-first SPA fallback; no API route |
| Local manifest/favicon/icons | PASS | config test dan build copy |
| Lazy route chunks | PASS | home, status, dan 404 menjadi chunk terpisah |
| Root dan route error boundary | PASS | behavior tests |
| Theme foundation | PASS | pure dan integration tests |
| No fake result/test data | PASS | architecture scope test dan manual review |
| FROZEN docs unchanged | PASS | SHA-256 sama dengan Tahap 01 |

## 3. Hasil coverage

Command:

```text
npm run coverage
```

Hasil source aktif:

| Metric | Hasil | Threshold Tahap 02 |
|---|---:|---:|
| Statements | **96.34%** | 90% |
| Branches | **86.66%** | 80% |
| Functions | **94.28%** | 90% |
| Lines | **97.46%** | 90% |

Uncovered paths terutama tombol reload browser dan beberapa fallback optional browser APIs. Tidak ada domain atau scoring yang tersembunyi dari denominator.

## 4. Test inventory

| Suite | Test |
|---|---:|
| App shell dan lazy routes | 4 |
| Root error boundary | 2 |
| Route error | 3 |
| Theme | 5 |
| Import boundaries | 3 |
| Project configuration | 4 |
| **Total** | **21** |

## 5. Build awal

Command:

```text
npm run build
```

Build terakhir sebelum final packaging memuat:

- `index.html`;
- satu CSS asset;
- satu main JS asset;
- chunk `HomeRoute`;
- chunk `DevelopmentStatusRoute`;
- chunk `NotFoundRoute`;
- manifest, favicon, dan dua local PNG icons.

Total folder `dist`: **307,858 byte** (sekitar **0.31 MB**). Output Vite final:

| Asset | Raw | Gzip |
|---|---:|---:|
| `index.html` | 0.73 kB | 0.40 kB |
| CSS utama | 7.92 kB | 2.39 kB |
| `NotFoundRoute` | 0.54 kB | 0.32 kB |
| `DevelopmentStatusRoute` | 1.06 kB | 0.51 kB |
| `HomeRoute` | 1.52 kB | 0.62 kB |
| JavaScript utama | 290.16 kB | 92.41 kB |

Icon, manifest, dan favicon juga berada di `dist`, tetapi Vite tidak menampilkan gzip line untuk static-copy assets.

## 6. Architecture checks

Checks yang berjalan sebagai test:

- production source tidak mengimpor `tests`, fixtures, atau `audit`;
- production source tidak memakai `Math.random`;
- TSX tidak memuat identitas UI yang dilarang;
- canonical command tersedia;
- runtime dependency hanya React, React DOM, dan React Router;
- manifest merujuk icon lokal yang ada;
- Vercel config tidak memiliki API route;
- domain/questions/scoring/profiles/card belum dibuat.

Lint juga meng-enforce test/audit import ban dan direct `Math.random` ban pada production source.

## 7. Hash file FROZEN dari Tahap 00

| File | SHA-256 | Status |
|---|---|---|
| `docs/PROJECT_CONSTITUTION.md` | `877ccaaa7a92d6668b8f1ebab1437ec66c417e3ed73550758a3341661ef26502` | UNCHANGED |
| `docs/MEASUREMENT_PRINCIPLES.md` | `c4eff2a028a422fdcb9cd5c9f1929d28d1f89aff4ee639bdbf4f1a9300ea3b14` | UNCHANGED |

## 8. Gate impact

Tahap 02: **PASS**. Gate 2: **IN PROGRESS**. Progres proyek: **4%**.

Coverage bootstrap tidak dapat menggantikan kontrak domain dan mapping Model A yang menjadi sisa Gate 2.
