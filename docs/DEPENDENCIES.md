# Dependencies

**Versi dokumen:** 1.0.0  
**Tanggal:** 17 Juni 2026  
**Status:** CONTROLLED

Versi resolusi aktual dikunci oleh `package-lock.json` lockfileVersion 3. Dependency baru hanya boleh ditambahkan apabila mempunyai pemilik modul, consumer nyata, dampak bundle yang dipahami, dan alasan yang tidak dapat dipenuhi dengan Web Platform atau kode sederhana.

## Runtime dependencies

| Package | Versi terpasang | Alasan |
|---|---:|---|
| `react` | 19.2.7 | Menyusun UI deklaratif, state, context, dan error boundary. |
| `react-dom` | 19.2.7 | Merender tree React ke DOM browser. |
| `react-router-dom` | 7.18.0 | Browser router, nested shell, lazy route modules, navigasi, 404, dan route error boundary. |

Tidak ada HTTP client, state manager eksternal, backend SDK, analytics SDK, database SDK, authentication SDK, atau package pemrosesan data peserta.

## Build dan TypeScript

| Package | Versi terpasang | Alasan |
|---|---:|---|
| `vite` | 8.0.16 | Development server dan bundler static production. |
| `@vitejs/plugin-react` | 6.0.2 | Transform JSX React dan Fast Refresh. |
| `typescript` | 6.0.3 | Strict typecheck untuk production source, test, dan konfigurasi. |
| `@types/node` | 25.9.3 | Tipe API Node yang digunakan konfigurasi dan architecture tests. |
| `@types/react` | 19.2.17 | Tipe React. |
| `@types/react-dom` | 19.2.3 | Tipe React DOM. |

## Pengujian

| Package | Versi terpasang | Alasan |
|---|---:|---|
| `vitest` | 4.1.9 | Test runner yang terintegrasi dengan transform Vite. |
| `@vitest/coverage-v8` | 4.1.9 | Menghasilkan coverage berbasis V8 untuk source yang aktif. |
| `jsdom` | 29.1.1 | Lingkungan DOM untuk test komponen di Node. |
| `@testing-library/react` | 16.3.2 | Menguji output dan behavior React dari sudut penggunaan. |
| `@testing-library/jest-dom` | 6.9.1 | Matcher DOM untuk assertion yang jelas. |
| `@testing-library/user-event` | 14.6.1 | Meniru interaksi pointer dan keyboard secara lebih realistis. |

## Lint dan static analysis

| Package | Versi terpasang | Alasan |
|---|---:|---|
| `eslint` | 10.5.0 | Static analysis utama. |
| `@eslint/js` | 10.0.1 | Aturan inti JavaScript untuk flat config. |
| `typescript-eslint` | 8.61.1 | Parser dan aturan TypeScript yang memakai type information. |
| `eslint-plugin-react-hooks` | 7.1.1 | Memeriksa Rules of Hooks dan dependency effect. |
| `eslint-plugin-react-refresh` | 0.5.3 | Menjaga batas export komponen agar aman untuk Fast Refresh. |
| `globals` | 17.6.0 | Definisi global browser, Node, ES2023, dan Vitest untuk lint. |

## Dependency yang sengaja belum dipasang

- Package canvas, image crop, atau export: Card Studio belum berada dalam scope.
- Package schema validation: kontrak domain dan pertanyaan belum dibuat.
- Package state management: shell saat ini cukup dengan React context dan router.
- Service worker tooling: offline-installable PWA belum menjadi acceptance Tahap 02.
- Backend, database, autentikasi, telemetry, atau generative API SDK: dilarang oleh konstitusi proyek.

## Hasil instalasi

Command nyata:

```text
npm install
```

Ringkasan hasil:

```text
added 253 packages, audited 254 packages, found 0 vulnerabilities
```
