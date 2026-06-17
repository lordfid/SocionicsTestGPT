# File Manifest

**Versi:** 1.1.0  
**Tanggal:** 17 Juni 2026  
**Status:** CONTROLLED

## 1. Fungsi manifest

Manifest membedakan:

- **file tersedia** — benar-benar ada pada filesystem tahap ini;
- **file direncanakan** — path final yang baru boleh dibuat pada gate pemiliknya;
- **status governance** — hanya `FROZEN`, `CONTROLLED`, atau `ACTIVE`;
- **gate owner** — gate yang bertanggung jawab membuat dan memverifikasi file.

Path yang tercantum sebagai rencana bukan placeholder file. File tidak boleh dibuat kosong hanya untuk mencocokkan tree.

## 2. File yang tersedia setelah Tahap 01

| File | Status | Versi | Fungsi | Aturan perubahan |
|---|---|---:|---|---|
| `docs/PROJECT_CONSTITUTION.md` | FROZEN | 1.0.0 | Otoritas tujuan, batas, tier, teknologi, bahasa, kualitas, dan gate | Hanya melalui migrasi konstitusi |
| `docs/REFERENCE_MATRIX.md` | CONTROLLED | 1.0.0 | Provenance, klasifikasi sumber, konflik, dan batas verifikasi | Analisis dampak dan changelog |
| `docs/MEASUREMENT_PRINCIPLES.md` | FROZEN | 1.0.0 | Kontrak pengukuran, delapan kanal, anti-inference, dan model comparison | Hanya melalui migrasi measurement contract |
| `docs/WORKFLOW.md` | CONTROLLED | 1.0.0 | Perfection Loop, gate, status, command policy, dan versioning | Tinjau semua gate terkait bila berubah |
| `docs/ARCHITECTURE.md` | CONTROLLED | 1.0.0 | Batas modul, dependency DAG, struktur final, determinisme, storage, splitting | Keputusan baru bila arah dependency berubah |
| `docs/DATA_FLOW.md` | CONTROLLED | 1.0.0 | Ownership dan transformasi data landing sampai share | Update bersama contract/state-flow change |
| `docs/ERROR_STRATEGY.md` | CONTROLLED | 1.0.0 | Taxonomy error, boundary, recovery, dan privacy logging | Update bersama error contract/tests |
| `docs/TEST_STRATEGY.md` | CONTROLLED | 1.0.0 | Lapisan test, adversarial catalogue, coverage, dan command | Update bersama toolchain atau gate test |
| `docs/PROJECT_STATE.md` | ACTIVE | 1.1.0 | Status terbaru, progres, command, versi, dan masalah terbuka | Diperbarui pada penutupan tiap tahap |
| `docs/FILE_MANIFEST.md` | CONTROLLED | 1.1.0 | File tersedia, target tree, owner, consumer, dan gate | Wajib update ketika file berubah |
| `docs/DECISIONS.md` | CONTROLLED | 1.1.0 | Log keputusan terkunci dan alasan | Append-only |
| `docs/KNOWN_ISSUES.md` | ACTIVE | 1.1.0 | Risiko, blocker, mitigasi, dan kriteria tutup | Update saat issue berubah |
| `docs/COVERAGE_REPORT.md` | CONTROLLED | 1.1.0 | Coverage requirement dan hasil pemeriksaan hingga Tahap 01 | Update saat gate atau kontrak berubah |
| `docs/NEXT_STAGE.md` | ACTIVE | 2.0.0 | Read order, file status, dan scope Tahap 02 | Diganti saat tahap berikut ditutup |
| `docs/CHANGELOG.md` | CONTROLLED | 1.1.0 | Riwayat perubahan proyek | Append-only per versi/tahap |

### Statistik file tersedia

- Total file: **15**
- FROZEN: **2**
- CONTROLLED: **10**
- ACTIVE: **3**
- Source aplikasi: **0**
- Pertanyaan produksi: **0**
- Expected profile: **0**
- Profile naratif: **0**
- Test produk: **0**

## 3. Planned root dan static files

File berikut baru dibuat pada Tahap 02 atau gate yang disebut.

| Path | Target status | Gate owner | Fungsi | Digunakan oleh / bukti penggunaan |
|---|---|---:|---|---|
| `package.json` | CONTROLLED | 2 | scripts dan dependency yang benar-benar dipakai | npm, seluruh command |
| `package-lock.json` | CONTROLLED | 2 | dependency lock deterministik | `npm ci`, build |
| `index.html` | CONTROLLED | 2 | entry HTML tunggal dan metadata dasar | Vite |
| `vite.config.ts` | CONTROLLED | 2 | build static, alias, chunk policy dasar | dev/build |
| `vitest.config.ts` | CONTROLLED | 2 | test environment, setup, coverage | test/coverage |
| `tsconfig.json` | CONTROLLED | 2 | TypeScript project references | typecheck/build |
| `tsconfig.app.json` | CONTROLLED | 2 | strict config source browser | typecheck/build |
| `tsconfig.node.json` | CONTROLLED | 2 | config Vite/Vitest/ESLint scripts | typecheck/build |
| `eslint.config.js` | CONTROLLED | 2 | lint dan import boundary enforcement | lint |
| `vercel.json` | CONTROLLED | 2 | static SPA rewrite, tanpa API route | deployment test |
| `.gitignore` | CONTROLLED | 2 | mengecualikan build/cache/local artifacts | repository audit |
| `README.md` | CONTROLLED | 2 | command, scope, privacy, dan deployment | maintainer onboarding |
| `public/manifest.webmanifest` | CONTROLLED | 2 | metadata installable web app | browser manifest |
| `public/favicon.svg` | CONTROLLED | 2 | favicon lokal | `index.html` |
| `public/icons/icon-192.png` | CONTROLLED | 2 | manifest icon | manifest |
| `public/icons/icon-512.png` | CONTROLLED | 2 | manifest icon besar | manifest |

## 4. Planned application composition

| Path | Target status | Gate owner | Fungsi | Consumer/test |
|---|---|---:|---|---|
| `src/main.tsx` | CONTROLLED | 2 | browser entry dan mount composition root | `index.html`, build smoke |
| `src/app/App.tsx` | CONTROLLED | 2 | top-level app shell | `main.tsx`, RTL |
| `src/app/router.tsx` | CONTROLLED | 2 | browser router dan lazy route wiring | `App.tsx`, route tests |
| `src/app/routes.ts` | CONTROLLED | 2 | canonical route IDs/paths | router/UI tests |
| `src/app/providers/AppProviders.tsx` | CONTROLLED | 2 | dependency injection dan global providers | App, integration tests |
| `src/app/errors/RootErrorBoundary.tsx` | CONTROLLED | 2 | recovery terakhir tanpa auto-delete | App, error tests |

Tidak ada file provider untuk service yang tidak dipakai.

## 5. Planned `domain` module

| Path | Target status | Gate owner | Fungsi | Consumer/test |
|---|---|---:|---|---|
| `src/domain/ids.ts` | FROZEN setelah Gate 2 | 2 | branded IDs lintas domain | semua public modules |
| `src/domain/versions.ts` | CONTROLLED | 2 | version identifiers | storage/session/result |
| `src/domain/deterministic/randomSource.ts` | CONTROLLED | 2 | interface random source pure | seeded selector/tests |
| `src/domain/deterministic/seededRandom.ts` | CONTROLLED | 2 | PRNG deterministik dari seed | questions/session/card |
| `src/domain/deterministic/stableSort.ts` | CONTROLLED | 2 | total ordering stabil | scoring/selection/tests |
| `src/domain/socionics/informationElements.ts` | FROZEN setelah Gate 2 | 2 | delapan element IDs dan invariant | domain/questions/scoring |
| `src/domain/socionics/evidenceChannels.ts` | FROZEN setelah Gate 2 | 2 | delapan channel IDs terkunci | questions/scoring/audit |
| `src/domain/socionics/modelAPositions.ts` | FROZEN setelah Gate 2 | 2 | delapan positions dan metadata tier A | Model A tests |
| `src/domain/socionics/modelABlocks.ts` | FROZEN setelah Gate 2 | 2 | Ego/Super-ego/Super-id/Id derivation | Model A tests |
| `src/domain/socionics/quadras.ts` | CONTROLLED | 2 | quadra identifiers sebagai hipotesis nilai | result/domain tests |
| `src/domain/socionics/tims.ts` | FROZEN setelah Gate 2 | 2 | 16 TIM IDs dan Model A mappings | scoring/audit tests |
| `src/domain/measurement/evidence.ts` | CONTROLLED | 2–3 | normalized evidence contract | questions/scoring |
| `src/domain/measurement/candidateModel.ts` | CONTROLLED | 2–6 | schema 64-cell candidate expectation | scoring/audit |
| `src/domain/measurement/personFit.ts` | CONTROLLED | 2–7 | person-fit signal contract, tanpa threshold | scoring/session |
| `src/domain/measurement/holdout.ts` | CONTROLLED | 2–5 | primary lock dan holdout report contract | session/scoring |
| `src/domain/measurement/resultSnapshot.ts` | CONTROLLED | 2–8 | immutable result metadata contract | result/storage/card |
| `src/domain/validation/assertInvariant.ts` | CONTROLLED | 2 | fail-fast invariant helper | domain modules/tests |
| `src/domain/public.ts` | CONTROLLED | 2 | satu public API domain | seluruh modules |

## 6. Planned `questions` module

### Contracts dan behavior

| Path | Target status | Gate owner | Fungsi | Consumer/test |
|---|---|---:|---|---|
| `src/questions/contracts/question.ts` | CONTROLLED | 3 | item/option participant-facing schema | data/validator/session |
| `src/questions/contracts/answer.ts` | CONTROLLED | 3 | normalized answer dan skip states | session/normalization |
| `src/questions/contracts/bank.ts` | CONTROLLED | 3 | bank manifest, phase, version | registry/audit |
| `src/questions/contracts/selection.ts` | CONTROLLED | 3–7 | eligible pool dan selection signal | selector/session |
| `src/questions/registry/createQuestionRegistry.ts` | CONTROLLED | 3 | merge bank dan enforce ID/phase uniqueness | session/audit/tests |
| `src/questions/validation/validateQuestion.ts` | CONTROLLED | 3 | runtime item validation | registry/tests |
| `src/questions/validation/validateQuestionBank.ts` | CONTROLLED | 3 | count, ID, phase, coverage preconditions | build/audit |
| `src/questions/selection/seededOrder.ts` | CONTROLLED | 3 | deterministic Fisher–Yates | session/tests |
| `src/questions/selection/selectNextItem.ts` | CONTROLLED | 7 | adaptive selection dari abstract signal | session/tests |
| `src/questions/public.ts` | CONTROLLED | 3 | public API questions | session/audit |

### Production data files

| Paths | Target status | Gate owner | Fungsi | Consumer/test |
|---|---|---:|---|---|
| `src/questions/data/core/index.ts` | CONTROLLED | 4 | export 12 core batches | registry/count audit |
| `src/questions/data/core/core-01.ts` … `core-12.ts` | CONTROLLED | 4 | masing-masing 16 core items; total 192 | registry/content audits |
| `src/questions/data/holdout/index.ts` | CONTROLLED | 5 | export 4 holdout batches | holdout registry |
| `src/questions/data/holdout/holdout-01.ts` … `holdout-04.ts` | CONTROLLED | 5 | masing-masing 8 holdout items; total 32 | leakage/audit tests |
| `src/questions/data/tie-break/index.ts` | CONTROLLED | 5 | export 4 tie-break batches | tie-break registry |
| `src/questions/data/tie-break/tie-break-01.ts` … `tie-break-04.ts` | CONTROLLED | 5 | masing-masing 8 tie-break items; total 32 | distinction audits |

## 7. Planned `scoring` module

| Path | Target status | Gate owner | Fungsi | Consumer/test |
|---|---|---:|---|---|
| `src/scoring/contracts/input.ts` | CONTROLLED | 6 | normalized engine input | session/scoring tests |
| `src/scoring/contracts/output.ts` | CONTROLLED | 6 | immutable scoring snapshot | session/result |
| `src/scoring/aggregate/aggregateEvidence.ts` | CONTROLLED | 6 | membuat 8×8 evidence map | comparison/tests |
| `src/scoring/evidence/buildEvidenceMap.ts` | CONTROLLED | 6 | trace source→cell→candidate | result/audit |
| `src/scoring/models/expectedProfiles/index.ts` | CONTROLLED | 6 | registry 16 candidate models | engine/audit |
| `src/scoring/models/expectedProfiles/ile.ts` | CONTROLLED | 6 | ILE 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/sei.ts` | CONTROLLED | 6 | SEI 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/ese.ts` | CONTROLLED | 6 | ESE 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/lii.ts` | CONTROLLED | 6 | LII 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/eie.ts` | CONTROLLED | 6 | EIE 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/lsi.ts` | CONTROLLED | 6 | LSI 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/sle.ts` | CONTROLLED | 6 | SLE 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/iei.ts` | CONTROLLED | 6 | IEI 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/see.ts` | CONTROLLED | 6 | SEE 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/ili.ts` | CONTROLLED | 6 | ILI 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/lie.ts` | CONTROLLED | 6 | LIE 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/esi.ts` | CONTROLLED | 6 | ESI 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/lse.ts` | CONTROLLED | 6 | LSE 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/eii.ts` | CONTROLLED | 6 | EII 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/iee.ts` | CONTROLLED | 6 | IEE 64-cell expected profile | registry/model tests |
| `src/scoring/models/expectedProfiles/sli.ts` | CONTROLLED | 6 | SLI 64-cell expected profile | registry/model tests |
| `src/scoring/comparison/compareCandidates.ts` | CONTROLLED | 6 | compare 16 models dengan stable order | session/tests |
| `src/scoring/holdout/evaluateHoldout.ts` | CONTROLLED | 5–6 | evaluasi frozen primary result | result/leakage tests |
| `src/scoring/personFit/evaluatePersonFit.ts` | CONTROLLED | 7 | response-quality signals non-diagnostic | session/result/tests |
| `src/scoring/confidence/deriveConfidence.ts` | CONTROLLED | 7 | quality-aware confidence policy | result/tests |
| `src/scoring/public.ts` | CONTROLLED | 6 | public scoring facade | session/audit |

## 8. Planned `profiles` and `result` modules

### Profiles

| Paths | Target status | Gate owner | Fungsi | Consumer/test |
|---|---|---:|---|---|
| `src/profiles/contracts/profile.ts` | CONTROLLED | 8 | profile/narrative schema dan provenance | data/result/audit |
| `src/profiles/data/index.ts` | CONTROLLED | 8 | registry 16 profile narratives | result/audit |
| `src/profiles/data/ile.ts`, `sei.ts`, `ese.ts`, `lii.ts`, `eie.ts`, `lsi.ts`, `sle.ts`, `iei.ts`, `see.ts`, `ili.ts`, `lie.ts`, `esi.ts`, `lse.ts`, `eii.ts`, `iee.ts`, `sli.ts` | CONTROLLED | 8 | narasi dan metadata terpisah per TIM | result/narrative audit |
| `src/profiles/narrative/buildProfileNarrative.ts` | CONTROLLED | 8 | memilih fragmen sesuai result facets | result/tests |
| `src/profiles/public.ts` | CONTROLLED | 8 | public profile data API | result/audit |

### Result

| Path | Target status | Gate owner | Fungsi | Consumer/test |
|---|---|---:|---|---|
| `src/result/contracts/result.ts` | CONTROLLED | 8 | result snapshot/view contract | UI/storage/tests |
| `src/result/contracts/cardInput.ts` | CONTROLLED | 8–10 | safe projection contract untuk card | card/tests |
| `src/result/build/buildResult.ts` | CONTROLLED | 8 | merge primary lock, holdout, fit, limits | session/UI/tests |
| `src/result/projection/toResultViewModel.ts` | CONTROLLED | 8–9 | participant-facing result model | Result route |
| `src/result/projection/toCardInput.ts` | CONTROLLED | 10 | membuang raw answer/evidence detail | Card Studio/tests |
| `src/result/public.ts` | CONTROLLED | 8 | public result API | UI/card/storage |

## 9. Planned `session` and `storage` modules

### Session

| Path | Target status | Gate owner | Fungsi | Consumer/test |
|---|---|---:|---|---|
| `src/session/contracts/session.ts` | CONTROLLED | 2–9 | state, event, phase, descriptor contracts | reducer/UI/storage |
| `src/session/state/sessionState.ts` | CONTROLLED | 9 | session state constructors/invariants | reducer/tests |
| `src/session/state/sessionReducer.ts` | CONTROLLED | 9 | pure transitions | controller/tests |
| `src/session/state/transitions.ts` | CONTROLLED | 9 | legal transition table | reducer/audit |
| `src/session/orchestration/createSession.ts` | CONTROLLED | 9 | versioned seeded session creation | UI/integration tests |
| `src/session/orchestration/recordAnswer.ts` | CONTROLLED | 9 | answer validation/revision | UI/tests |
| `src/session/orchestration/advanceSession.ts` | CONTROLLED | 7–9 | selection, phase transition, checkpoint request | UI/tests |
| `src/session/orchestration/finalizeSession.ts` | CONTROLLED | 8–9 | primary lock, holdout, result request | UI/tests |
| `src/session/ports/sessionStore.ts` | CONTROLLED | 2–9 | persistence interface | storage adapter/tests |
| `src/session/public.ts` | CONTROLLED | 9 | controller/public session API | UI/app |

### Storage

| Path | Target status | Gate owner | Fungsi | Consumer/test |
|---|---|---:|---|---|
| `src/storage/contracts/persistedEnvelope.ts` | CONTROLLED | 2–9 | versioned persistence envelope | all adapters/migrations |
| `src/storage/keys.ts` | CONTROLLED | 9 | namespaced resource keys | adapters/reset tests |
| `src/storage/migrations/migratePersistedData.ts` | CONTROLLED | 9 | pure sequential migration | adapters/tests |
| `src/storage/adapters/localStorageSessionStore.ts` | CONTROLLED | 9 | session port implementation | app/session integration |
| `src/storage/adapters/localStoragePreferencesStore.ts` | CONTROLLED | 9 | theme/preferences persistence | app/UI tests |
| `src/storage/adapters/indexedDbCardDraftStore.ts` | CONTROLLED | 10 | opt-in large card/photo draft persistence | Card Studio tests |
| `src/storage/recovery/quarantineCorruptRecord.ts` | CONTROLLED | 9 | preserve metadata before reset | storage recovery tests |
| `src/storage/public.ts` | CONTROLLED | 9 | adapter exports for composition root | app |

## 10. Planned `card` module

| Path | Target status | Gate owner | Fungsi | Consumer/test |
|---|---|---:|---|---|
| `src/card/contracts/cardSchema.ts` | CONTROLLED | 10 | versioned card draft/content schema | UI/storage/render |
| `src/card/contracts/renderSpec.ts` | CONTROLLED | 10 | explicit width/height/DPR/font inputs | renderer/tests |
| `src/card/templates/index.ts` | CONTROLLED | 10 | template registry | Card Studio/audit |
| `src/card/templates/portrait.ts` | CONTROLLED | 10 | portrait layout definition | renderer/tests |
| `src/card/templates/square.ts` | CONTROLLED | 10 | square layout definition | renderer/tests |
| `src/card/templates/story.ts` | CONTROLLED | 10 | story layout definition | renderer/tests |
| `src/card/photo/decodePhoto.ts` | CONTROLLED | 10 | local decode/validation/Object URL lifecycle | Card Studio/tests |
| `src/card/photo/cropPhoto.ts` | CONTROLLED | 10 | deterministic crop transform | renderer/tests |
| `src/card/render/renderCard.ts` | CONTROLLED | 10 | viewport-independent Canvas render | export/tests |
| `src/card/export/exportPng.ts` | CONTROLLED | 10 | Blob/File creation and download | UI/tests |
| `src/card/share/shareCard.ts` | CONTROLLED | 10 | capability check, file share, fallback | UI/tests |
| `src/card/public.ts` | CONTROLLED | 10 | public Card Studio API | UI/result |

## 11. Planned `audit` module

| Path | Target status | Gate owner | Fungsi | Consumer/test |
|---|---|---:|---|---|
| `src/audit/architecture/checkImportBoundaries.ts` | CONTROLLED | 2 | cycle and forbidden import audit | audit command/tests |
| `src/audit/questions/auditQuestionBank.ts` | CONTROLLED | 3–5 | count/schema/participant-field audit | coverage report |
| `src/audit/questions/auditCoverage.ts` | CONTROLLED | 3–4 | element/channel/context coverage | coverage report |
| `src/audit/questions/auditLeakage.ts` | CONTROLLED | 5 | core/holdout/tie-break isolation | gate 5 tests |
| `src/audit/scoring/auditCandidateModels.ts` | CONTROLLED | 6 | 16×64 completeness/provenance | gate 6 tests |
| `src/audit/profiles/auditNarrativeProvenance.ts` | CONTROLLED | 8 | cross-system/stereotype provenance checks | gate 8 tests |
| `src/audit/report/createAuditReport.ts` | CONTROLLED | 3 onward | deterministic machine/human report | docs/CI verification |
| `src/audit/public.ts` | CONTROLLED | 2 | audit command exports | scripts/tests only |

Production runtime tidak boleh mengimpor file audit.

## 12. Planned `ui` module

| Path | Target status | Gate owner | Fungsi | Consumer/test |
|---|---|---:|---|---|
| `src/ui/components/AppShell.tsx` | CONTROLLED | 2–9 | semantic shell dan route outlet | App/RTL |
| `src/ui/components/ActionButton.tsx` | CONTROLLED | 9 | accessible shared action | routes/RTL |
| `src/ui/components/ErrorNotice.tsx` | CONTROLLED | 2–9 | typed recovery actions | route boundaries |
| `src/ui/components/ProgressIndicator.tsx` | CONTROLLED | 9 | accessible session progress | assessment tests |
| `src/ui/hooks/useAssessmentController.ts` | CONTROLLED | 9 | React binding ke session public API | assessment route |
| `src/ui/routes/LandingRoute.tsx` | CONTROLLED | 2–9 | landing dan resume entry | route tests |
| `src/ui/routes/ModeRoute.tsx` | CONTROLLED | 9 | mode selection | route tests |
| `src/ui/routes/AssessmentRoute.tsx` | CONTROLLED | 9 | question session UI | integration/RTL |
| `src/ui/routes/ResultRoute.tsx` | CONTROLLED | 8–9 | result view dan limits | RTL |
| `src/ui/routes/CardStudioRoute.tsx` | CONTROLLED | 10 | card customization/export/share | card integration |
| `src/ui/routes/ReferencesRoute.tsx` | CONTROLLED | 8–9 | secondary references dan scientific status | content tests |
| `src/ui/styles/reset.css` | CONTROLLED | 2 | CSS reset | app build/visual review |
| `src/ui/styles/tokens.css` | CONTROLLED | 2 | design tokens dan theme foundation | all UI |
| `src/ui/styles/global.css` | CONTROLLED | 2 | global typography/layout/accessibility | all UI |

Komponen baru hanya boleh dibuat bila dipakai oleh route atau komponen produksi.

## 13. Planned test files

| Path | Target status | Gate owner | Fungsi |
|---|---|---:|---|
| `tests/setup.ts` | CONTROLLED | 2 | RTL/Vitest environment setup |
| `tests/helpers/renderWithProviders.tsx` | CONTROLLED | 2–9 | shared render harness yang benar-benar dipakai |
| `tests/fixtures/answers.ts` | CONTROLLED | 3–6 | synthetic answer vectors |
| `tests/fixtures/sessions.ts` | CONTROLLED | 9 | synthetic session states |
| `tests/fixtures/candidateModels.ts` | CONTROLLED | 6 | valid/invalid synthetic 64-cell models |
| `tests/domain/modelA.test.ts` | CONTROLLED | 2 | finite Model A invariants |
| `tests/domain/determinism.test.ts` | CONTROLLED | 2 | seeded PRNG dan stable order |
| `tests/questions/schema.test.ts` | CONTROLLED | 3 | question contract validation |
| `tests/questions/registry.test.ts` | CONTROLLED | 3–5 | exact count, IDs, phase separation |
| `tests/questions/selection.test.ts` | CONTROLLED | 7 | seeded/adaptive eligibility |
| `tests/scoring/evidenceMap.test.ts` | CONTROLLED | 6 | 8×8 map dan trace |
| `tests/scoring/comparison.test.ts` | CONTROLLED | 6 | 16-candidate pure comparison |
| `tests/scoring/holdoutIsolation.test.ts` | CONTROLLED | 5–6 | primary lock and leakage prevention |
| `tests/scoring/personFit.test.ts` | CONTROLLED | 7 | non-diagnostic quality signals |
| `tests/session/stateMachine.test.ts` | CONTROLLED | 9 | transitions, revision, finalize |
| `tests/storage/migrations.test.ts` | CONTROLLED | 9 | version/corruption/quota recovery |
| `tests/result/buildResult.test.ts` | CONTROLLED | 8 | limitations, provenance, versions |
| `tests/card/renderSpec.test.ts` | CONTROLLED | 10 | explicit formats and viewport independence |
| `tests/card/shareFallback.test.ts` | CONTROLLED | 10 | Web Share/download/text branches |
| `tests/audit/importBoundaries.test.ts` | CONTROLLED | 2 | no cycles/forbidden imports |
| `tests/ui/appShell.test.tsx` | CONTROLLED | 2 | shell/error boundary smoke |
| `tests/ui/assessmentFlow.test.tsx` | CONTROLLED | 9 | participant interaction flow |
| `tests/ui/cardStudio.test.tsx` | CONTROLLED | 10 | local photo/export/share behavior |

Test tambahan wajib memiliki production behavior atau regression yang jelas. File test kosong atau snapshot-only tidak diterima.

## 14. Dependency dokumen

```text
PROJECT_CONSTITUTION
├─ MEASUREMENT_PRINCIPLES
├─ REFERENCE_MATRIX
├─ DECISIONS
├─ WORKFLOW
└─ ARCHITECTURE
   ├─ DATA_FLOW
   ├─ ERROR_STRATEGY
   ├─ TEST_STRATEGY
   └─ FILE_MANIFEST

PROJECT_STATE
├─ FILE_MANIFEST
├─ KNOWN_ISSUES
├─ COVERAGE_REPORT
├─ NEXT_STAGE
└─ CHANGELOG
```

## 15. Aturan penambahan dan penghapusan file

Sebelum file dibuat:

- gate owner aktif;
- consumer nyata telah ditentukan;
- test atau verification path tersedia;
- file tidak menggandakan tanggung jawab path lain;
- tidak ada file data kosong;
- tidak ada barrel yang hanya menambah indirection tanpa public boundary.

Sebelum file dihapus atau digabung:

- seluruh import diperiksa;
- manifest diperbarui;
- test terdampak dijalankan;
- keputusan ditambah bila boundary berubah;
- tidak boleh menyembunyikan scope yang belum selesai dengan menghapus path rencana.
