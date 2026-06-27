# Ringkasan Proyek

| Atribut | Keterangan |
|---|---|
| **Dataset** | CHIRPS v2.0 — daily precipitation (NetCDF 3D: waktu × lintang × bujur) |
| **Wilayah** | Provinsi Jawa Barat, Indonesia |
| **Periode** | 2000–2025 (±26 tahun, ±9.500 hari) |
| **Target** | Rata-rata intensitas curah hujan 3 hari ke depan (mm/hari) |
| **Model Utama** | Bidirectional LSTM + Bahdanau Attention |
| **Baseline** | Auto-ARIMA & Persistence (Rata-rata 7 hari) |
| **Validasi** | Walk-Forward Validation 5-Fold |

```

```
# Pipeline ini mencakup:

- Load data spasial CHIRPS 3D (NetCDF: time × latitude × longitude)
- Ekstraksi fitur spasial (mean, std, max, p75, p90, pct_rain, regional sub-area)
- Feature engineering rolling statistics bebas data leakage
- Normalisasi MinMaxScaler (fit hanya pada train)
- Sliding-window sequences (timestep = 14 hari)
- Split kronologis 80 / 10 / 10 (train / val / test)
- Model Bi-LSTM + Bahdanau Attention Mechanism
- Baseline Auto-ARIMA
- Walk-Forward Validation (5-fold, val loss monitoring)
- Evaluasi metrik: R², MAE, RMSE pada data validation & test
- Visualisasi lengkap: EDA, peta spasial, kurva training, scatter, residual, per musim

```

# Catatan Ilmiah

Prediksi curah hujan harian berbasis data historis memiliki batas atas teoretis R² ≈ 45–55% (Poornima & Pushpalatha, 2019; Tao et al., 2021). Angka ini adalah rentang yang valid dan umum di literatur — bukan kelemahan model, melainkan sifat inheren data hidrologi. Data NetCDF 3D menambah informasi distribusi spasial yang meningkatkan performa dibandingkan pendekatan rata-rata provinsi tunggal.
