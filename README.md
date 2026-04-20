# 🌊 GEOGLOWS Flood Hydrograph Analysis — DAS Randangan, Gorontalo

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_GITHUB_USERNAME/geoglows-randangan-flood/blob/main/notebooks/GEOGLOWS_Randangan_flood_analysis.ipynb)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Analisis hidrograf banjir 
menggunakan data retrospektif **GEOGLOWS v2** berbasis ERA5 reanalysis ECMWF.

---

## 📋 Deskripsi

| Item | Detail |
|---|---|
| **River ID** | XXXXXXXXX (GEOGLOWS v2 / TDX-Hydro LINKNO) |
| **Data sumber** | GEOGLOWS v2 S3 Zarr hourly (ERA5), 1940–sekarang |

## 🔬 Metodologi

```
ERA5 Hourly (S3 Zarr)
        ↓
   Resample → Daily Max
        ↓
   FDC Bias Correction (ungauged)
        ↓
   Annual Maximum Series (AMS)
        ↓
   Frequency Analysis: LP3 / Gumbel / Log-Normal
        ↓
   Design Hydrograph (hourly, scaled)
        ↓
   Export → HEC-RAS / LISFLODD-FP
```

## 📁 Struktur Repo

```
hidrograf_geoglows/
│
├── notebooks/
│   └── Analisis_Hidrograf_Banjir_GEOGLOWS.ipynb   # Notebook utama
│
├── data/
│   └── output/                                    # Hasil export (gitignored)
│       ├── hydrograph_T100.csv
│       ├── HECRAS_T100.txt
│       ├── debit_rancangan.csv
│       └── hourly_all_events.csv
│
├── requirements.txt
├── LICENSE
└── README.md
```

## 🚀 Cara Menggunakan

### 1. Jalankan di Google Colab (direkomendasikan)

Klik badge **Open in Colab** di atas. Semua dependensi diinstall otomatis di dalam notebook.

### 2. Jalankan lokal

```bash
git clone https://github.com/seniarwan/hidrograf_geoglows.git
cd hidrograf_geoglows
pip install -r requirements.txt
jupyter notebook notebooks/Analisis_Hidrograf_Banjir_GEOGLOWS.ipynb
```

## 📦 Dependensi

Lihat `requirements.txt`. Dependensi utama:

- `xarray` + `zarr` + `s3fs` — akses data S3
- `scipy` — analisis statistik frekuensi
- `pandas` / `numpy` — manipulasi data
- `matplotlib` — visualisasi

## 📊 Output

| File | Deskripsi |
|---|---|
| `hydrograph_T{T}_Randangan.csv` | Hidrograf desain per periode ulang (hourly) |
| `HECRAS_T{T}_Randangan.txt` | Format input HEC-RAS |
| `debit_rancangan_Randangan.csv` | Tabel debit rancangan semua T |
| `hourly_Event{N}_{date}.csv` | Data debit hourly per event historis |
| `hourly_all_events_Randangan.csv` | Semua event dalam satu file (long format) |

## 📚 Referensi

- Hales, R.C., et al. (2022). Advancing global hydrologic modeling with the GEOGloWS ECMWF streamflow service. *Journal of Flood Risk Management*. https://doi.org/10.1111/jfr3.12859
- Hales, R.C., et al. (2023). Bias correcting discharge simulations from the GEOGloWS global hydrologic model. *Journal of Hydrology*, 626, 130279. https://doi.org/10.1016/j.jhydrol.2023.130279
- GEOGLOWS Hydrological Model Version 2. AWS Open Data Registry. https://registry.opendata.aws/geoglows-v2

## 📄 Lisensi

MIT License — bebas digunakan dan dimodifikasi dengan atribusi.
