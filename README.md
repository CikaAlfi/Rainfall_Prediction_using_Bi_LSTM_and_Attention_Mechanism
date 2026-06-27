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

### Alur Pipeline 

```
[1] Setup            → Install library, import, atur seed
[2] Akuisisi Data    → Download otomatis (ClimateSERV API) atau upload manual
[3] Load & Validasi  → Buka NetCDF, hitung missing value, ringkasan data
[4] EDA              → Time series, distribusi, peta spasial, autokorelasi
[5] Feature Eng.     → Fitur rolling anti-leakage, target 3-hari
[6] Persiapan Data   → Sliding window, split 80/10/10, normalisasi
[7] Arsitektur Model → Bi-LSTM + Bahdanau Attention
[8] Pelatihan        → EarlyStopping, ReduceLROnPlateau
[9] Baseline         → Auto-ARIMA, Persistence
[10] Evaluasi        → R², MAE, RMSE — val & test
[11] Walk-Forward    → 5-fold time series cross-validation
[12] Visualisasi     → 8 plot publikasi-siap
[13] Ekspor          → CSV prediksi, metrik, model
```

### Catatan Ilmiah

> Prediksi curah hujan harian berbasis data historis memiliki **batas atas teoretis R² ≈ 45–55%**
> (Poornima & Pushpalatha, 2019; Tao et al., 2021). Angka ini adalah rentang yang valid
> dan umum di literatur — bukan kelemahan model, melainkan sifat inheren data hidrologi.
> Data NetCDF 3D menambah informasi distribusi spasial yang meningkatkan performa
> dibandingkan pendekatan rata-rata provinsi tunggal.
