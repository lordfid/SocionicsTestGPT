# File Manifest

**Versi:** 3.0.0  
**Tanggal:** 17 Juni 2026  
**Status:** CONTROLLED

## 1. Statistik paket sumber

Generated directories `node_modules/`, `dist/`, dan `coverage/` tidak dihitung sebagai file paket sumber dan tidak dimasukkan ke ZIP.

| Kategori | Jumlah |
|---|---:|
| Dokumen | 16 |
| Root/config | 13 |
| Public assets | 4 |
| Production source | 21 |
| Test dan test support | 8 |
| **Total** | **62** |

Status file:

- FROZEN: 6 file;
- CONTROLLED: 53 file;
- ACTIVE: 3 file.

## 2. Dokumen

| File | Status | Fungsi |
|---|---|---|
| `docs/PROJECT_CONSTITUTION.md` | FROZEN | Otoritas tertinggi proyek setelah instruksi pengguna |
| `docs/MEASUREMENT_PRINCIPLES.md` | FROZEN | Kontrak pengukuran dan anti-inference |
| `docs/REFERENCE_MATRIX.md` | CONTROLLED | Provenance, tier, konflik referensi, dan batas verifikasi |
| `docs/WORKFLOW.md` | CONTROLLED | Perfection Loop, gate, versioning, dan command policy |
| `docs/ARCHITECTURE.md` | CONTROLLED | Batas modul, dependency graph, target tree, lazy loading |
| `docs/DATA_FLOW.md` | CONTROLLED | Aliran data target dari landing sampai card/share |
| `docs/ERROR_STRATEGY.md` | CONTROLLED | Taksonomi error, boundary, recovery, dan logging policy |
| `docs/TEST_STRATEGY.md` | CONTROLLED | Lapisan test, adversarial catalogue, dan coverage policy |
| `docs/DEPENDENCIES.md` | CONTROLLED | Dependency aktual dan alasan setiap package |
| `docs/FILE_MANIFEST.md` | CONTROLLED | Inventaris file, status, consumer, dan verification |
| `docs/DECISIONS.md` | CONTROLLED | Log keputusan append-only |
| `docs/COVERAGE_REPORT.md` | CONTROLLED | Bukti acceptance dan hasil command |
| `docs/CHANGELOG.md` | CONTROLLED | Riwayat perubahan append-only |
| `docs/PROJECT_STATE.md` | ACTIVE | Snapshot status proyek terbaru |
| `docs/KNOWN_ISSUES.md` | ACTIVE | Risiko dan utang yang masih terbuka |
| `docs/NEXT_STAGE.md` | ACTIVE | Kontrak pembukaan tahap berikutnya |

## 3. Root dan konfigurasi

| File | Status | Consumer / verification | Fungsi |
|---|---|---|---|
| `.gitignore` | CONTROLLED | Git dan packaging review | Mengecualikan dependency serta output generated |
| `README.md` | CONTROLLED | Pengembang | Cara menjalankan, struktur aktif, dan batas tahap |
| `package.json` | CONTROLLED; command surface FROZEN | npm dan config tests | Metadata, dependency, serta canonical scripts |
| `package-lock.json` | CONTROLLED | `npm install`/`npm ci` | Resolusi dependency reproducible |
| `index.html` | CONTROLLED | Vite entry dan smoke test | DOM mount, metadata, manifest, favicon |
| `vite.config.ts` | CONTROLLED | Vite build | React transform, alias, build target |
| `vitest.config.ts` | CONTROLLED | Vitest/coverage | DOM environment, setup, source include, threshold |
| `eslint.config.js` | CONTROLLED; core rules FROZEN | `npm run lint` | Typed lint, hooks, refresh, boundaries, random ban |
| `vercel.json` | CONTROLLED | config test | Static build dan SPA fallback tanpa API |
| `tsconfig.json` | FROZEN | `npm run typecheck` | Root project references |
| `tsconfig.app.json` | FROZEN | TypeScript | Strict production source contract dan alias |
| `tsconfig.node.json` | FROZEN | TypeScript | Strict config-file contract |
| `tsconfig.test.json` | FROZEN | TypeScript | Strict test contract dengan DOM, Vitest, dan Node types |

## 4. Public assets

| File | Status | Consumer / verification | Fungsi |
|---|---|---|---|
| `public/manifest.webmanifest` | CONTROLLED | browser dan config test | Metadata aplikasi web lokal |
| `public/favicon.svg` | CONTROLLED | `index.html` | Favicon lokal |
| `public/icons/icon-192.png` | CONTROLLED | manifest dan config test | Icon 192 × 192 |
| `public/icons/icon-512.png` | CONTROLLED | manifest dan config test | Icon 512 × 512 / safe maskable area |

## 5. Production source

| File | Status | Consumer / verification | Fungsi |
|---|---|---|---|
| `src/main.tsx` | CONTROLLED | `index.html`, build | Mount React dan root error boundary |
| `src/vite-env.d.ts` | CONTROLLED | TypeScript | Vite client type reference |
| `src/app/App.tsx` | CONTROLLED | main dan app tests | Provider dan RouterProvider composition |
| `src/app/routes.ts` | CONTROLLED | router, shell, route pages | Canonical path constants |
| `src/app/router.tsx` | CONTROLLED | App dan app tests | Browser router, lazy route mapping, route boundary |
| `src/app/providers/AppProviders.tsx` | CONTROLLED | App | Eager provider composition |
| `src/app/errors/RootErrorBoundary.tsx` | CONTROLLED | main dan boundary test | Recovery UI untuk render failure |
| `src/theme/theme.ts` | CONTROLLED | provider, UI, tests | Pure theme types dan transition functions |
| `src/theme/ThemeContext.ts` | CONTROLLED | provider dan hook | Context contract |
| `src/theme/ThemeProvider.tsx` | CONTROLLED | AppProviders dan theme tests | Theme resolution, media query, local preference |
| `src/theme/useTheme.ts` | CONTROLLED | ThemeToggle dan tests | Guarded context consumer hook |
| `src/ui/shell/AppShell.tsx` | CONTROLLED | router dan app tests | Eager layout, nav, skip link, outlet, footer |
| `src/ui/theme/ThemeToggle.tsx` | CONTROLLED | AppShell dan app tests | Accessible theme control |
| `src/ui/routes/error/RouteErrorPage.tsx` | CONTROLLED | router dan route tests | Sanitized route error serta recovery actions |
| `src/ui/routes/loading/RouteLoadingPage.tsx` | CONTROLLED | router dan app tests | Eager loading state untuk lazy routes |
| `src/ui/routes/home/HomeRoute.tsx` | CONTROLLED | lazy router dan app tests | Status bootstrap pada route home |
| `src/ui/routes/status/DevelopmentStatusRoute.tsx` | CONTROLLED | lazy router dan app tests | Status implementasi tanpa hasil palsu |
| `src/ui/routes/not-found/NotFoundRoute.tsx` | CONTROLLED | lazy router dan app tests | Wildcard route |
| `src/styles/reset.css` | CONTROLLED | main/build | Reset dan reduced-motion baseline |
| `src/styles/tokens.css` | CONTROLLED | main/build | Design tokens light/dark |
| `src/styles/global.css` | CONTROLLED | main/build | Shell, route, recovery, responsive global styles |

## 6. Tests

| File | Status | Target |
|---|---|---|
| `tests/setup.ts` | CONTROLLED | jest-dom, cleanup, default matchMedia |
| `tests/helpers/renderApp.tsx` | CONTROLLED | Memory-router test composition |
| `tests/app/app-shell.test.tsx` | CONTROLLED | Home, lazy navigation, theme, 404 |
| `tests/app/root-error-boundary.test.tsx` | CONTROLLED | Normal dan failed render paths |
| `tests/app/route-error.test.tsx` | CONTROLLED | HTTP, unknown error, empty status text |
| `tests/theme/theme.test.tsx` | CONTROLLED | Pure contract, storage, system event, hook guard |
| `tests/architecture/import-boundaries.test.ts` | CONTROLLED | Test/audit import ban, random ban, UI identity ban |
| `tests/architecture/project-config.test.ts` | CONTROLLED | Scripts, manifest/icons, static rewrite, scope exclusions |

## 7. Folder target yang sengaja belum dibuat

Folder berikut baru boleh dibuat ketika memiliki production file nyata dan test/consumer:

- `src/domain`;
- `src/questions`;
- `src/scoring`;
- `src/profiles`;
- `src/session`;
- `src/storage`;
- `src/result`;
- `src/card`;
- `src/audit`.

Tidak ada `.gitkeep`, barrel kosong, fungsi kosong, atau file dekoratif.

## 8. Aturan perubahan setelah Tahap 02

- File FROZEN memerlukan migrasi tertulis, alasan teknis, dampak, dan test yang berubah.
- Command canonical tidak boleh dihapus atau diganti maknanya. Command tambahan boleh dibuat bila benar-benar digunakan.
- Core lint rules boleh diperluas secara aditif; pelemahan memerlukan keputusan baru.
- Cross-module import tahap berikutnya harus memakai public API sesuai `ARCHITECTURE.md`.
- File baru wajib mempunyai owner, consumer, test/verification, dan entry manifest.
