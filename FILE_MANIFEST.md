# File Manifest

**Versi:** 1.0.0  
**Tanggal:** 17 Juni 2026  
**Status:** CONTROLLED

## Manifest Tahap 00

| File | Status | Versi | Fungsi | Aturan perubahan |
|---|---|---:|---|---|
| `docs/PROJECT_CONSTITUTION.md` | FROZEN | 1.0.0 | Otoritas tujuan, batas, tier, teknologi, bahasa, kualitas, gate | Hanya melalui migrasi konstitusi |
| `docs/REFERENCE_MATRIX.md` | CONTROLLED | 1.0.0 | Provenance, klasifikasi sumber, konflik, dan batas verifikasi | Analisis dampak dan changelog |
| `docs/MEASUREMENT_PRINCIPLES.md` | FROZEN | 1.0.0 | Kontrak pengukuran, delapan kanal, anti-inference, model comparison | Hanya melalui migrasi measurement contract |
| `docs/WORKFLOW.md` | CONTROLLED | 1.0.0 | Perfection loop, gate, status, command policy, versioning | Perbarui bila workflow berubah; gate terkait harus ditinjau |
| `docs/PROJECT_STATE.md` | ACTIVE | 1.0.0 | Status terbaru, progres, command, versi, masalah terbuka | Diperbarui pada penutupan setiap tahap |
| `docs/FILE_MANIFEST.md` | CONTROLLED | 1.0.0 | Daftar file, status, tujuan, dan aturan perubahan | Wajib diperbarui saat file bertambah/berubah/dihapus |
| `docs/DECISIONS.md` | CONTROLLED | 1.0.0 | Log keputusan terkunci dan alasannya | Append-only; keputusan lama tidak ditulis ulang |
| `docs/KNOWN_ISSUES.md` | ACTIVE | 1.0.0 | Risiko, keterbatasan, utang validasi, dan blocker | Update saat issue dibuka, berubah, atau ditutup |
| `docs/COVERAGE_REPORT.md` | CONTROLLED | 1.0.0 | Bukti coverage scope dan requirement Tahap 00 | Update saat gate atau kontrak berubah |
| `docs/NEXT_STAGE.md` | ACTIVE | 1.0.0 | Read order, file FROZEN/CONTROLLED, dan tujuan tahap selanjutnya | Diganti pada penutupan tahap berikutnya |
| `docs/CHANGELOG.md` | CONTROLLED | 1.0.0 | Riwayat perubahan proyek | Append-only per versi/tahap |

## Statistik

- Total file: **11**
- FROZEN: **2**
- CONTROLLED: **6**
- ACTIVE: **3**
- File aplikasi: **0**
- File bank pertanyaan: **0**
- File scoring: **0**
- File test produk: **0**

## Dependensi dokumen

```text
PROJECT_CONSTITUTION
├── MEASUREMENT_PRINCIPLES
├── WORKFLOW
├── DECISIONS
├── REFERENCE_MATRIX
└── COVERAGE_REPORT

PROJECT_STATE
├── FILE_MANIFEST
├── KNOWN_ISSUES
├── NEXT_STAGE
└── CHANGELOG
```

## Aturan penambahan file

Sebelum file baru dibuat, tahap aktif harus menjelaskan:

- path;
- status awal;
- pemilik domain;
- alasan keberadaan;
- file yang mengimpor atau membacanya;
- test atau verifikasi;
- dampak terhadap gate;
- apakah file menggantikan file lama.

File yang tidak digunakan tidak boleh masuk paket final.
