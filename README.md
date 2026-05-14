# 🖼️ Kompresi Gambar dengan Algoritma DCT (JPEG Compression)

## 👥 Kelompok 3

### Nama Anggota Kelompok

| Nama                   | NIM        |
| ---------------------- | ---------- |
| Nazwa Yulianti Munjana | 1237050007 |
| Sayyid Maulana         | 1237050126 |
| Tri Febriansyah        | 1237050094 |


> **Praktikum Sistem Multimedia** — Implementasi Discrete Cosine Transform (DCT) untuk kompresi gambar berbasis standar JPEG.

[![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python&logoColor=white)](https://python.org)
[![Colab](https://img.shields.io/badge/Google%20Colab-Ready-F9AB00?logo=googlecolab&logoColor=white)](https://colab.research.google.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 📋 Deskripsi

Proyek ini mengimplementasikan algoritma **Discrete Cosine Transform (DCT)** secara manual (from scratch) untuk melakukan kompresi gambar sesuai standar JPEG. Implementasi mencakup seluruh tahapan inti JPEG: block splitting 8×8, forward DCT, quantization, dan inverse DCT.

### Fitur Utama
- ✅ Implementasi DCT manual menggunakan `scipy.fftpack`
- ✅ Quantization dengan tabel standar JPEG (ITU-T T.81)
- ✅ Batch compression 20 gambar dataset
- ✅ Metrik kualitas objektif — PSNR & SSIM
- ✅ Analisis multi-quality level (Q=10, 30, 50, 70, 90)
- ✅ Visualisasi before/after untuk setiap gambar

---

## 🔬 Pipeline JPEG yang Diimplementasikan

```
Input Image (RGB)
       │
       ▼
┌──────────────┐
│  Convert RGB │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ Split Block  │──── Gambar dibagi menjadi blok 8×8 pixel
│    8 × 8     │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│  Forward DCT │──── Transformasi domain spasial → frekuensi
│   (dct2)     │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ Quantization │──── Pembagian dengan Q-Table (LANGKAH LOSSY)
│  (÷ Q-Table) │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ Dequantize   │──── Perkalian kembali dengan Q-Table
│  (× Q-Table) │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ Inverse DCT  │──── Kembali ke domain spasial
│   (idct2)    │
└──────┬───────┘
       │
       ▼
  Output Image (Compressed)
```

---

## 📁 Struktur Proyek

```
implementasi_dct_compression/
├── 📓 Algoritma_DCT.ipynb          # Notebook utama (Google Colab)
├── 🐍 algoritma_dct.py             # Source code (format Python cell)
├── 📖 README.md
├── 📂 dataset/                      # 20 gambar input
│   ├── gambar1.jpeg
│   ├── gambar2.jpeg
│   └── ... (20 gambar)
├── 📂 output/                       # Hasil kompresi DCT
│   ├── compressed_gambar1.jpg
│   └── ...
└── 📂 results/                      # Laporan CSV
    └── compression_results.csv
```

---

## 📊 Hasil Kompresi (Data Real)

### Ringkasan Metrik (Quality = 50)

| Metrik | Nilai |
|--------|-------|
| Total Gambar | 20 |
| Rata-rata PSNR | **31.03 dB** |
| Rata-rata SSIM | **0.9301** |
| PSNR Tertinggi | 35.91 dB (gambar18) |
| SSIM Tertinggi | 0.9680 (gambar13) |

### Detail per Gambar

| Image | Original (KB) | Compressed (KB) | PSNR (dB) | SSIM |
|-------|---------------|-----------------|-----------|------|
| gambar1.jpeg | 167.95 | 243.45 | 29.36 | 0.9379 |
| gambar2.jpeg | 226.82 | 330.43 | 28.40 | 0.9186 |
| gambar3.jpeg | 225.75 | 330.79 | 31.90 | 0.9257 |
| gambar4.jpeg | 187.39 | 302.43 | 29.68 | 0.9195 |
| gambar5.jpeg | 75.16 | 105.53 | 31.17 | 0.9253 |
| gambar6.jpeg | 76.71 | 110.99 | 26.00 | 0.9016 |
| gambar7.jpeg | 215.48 | 309.03 | 32.83 | 0.9417 |
| gambar8.jpeg | 153.55 | 237.02 | 34.26 | 0.9612 |
| gambar9.jpeg | 169.88 | 243.25 | 33.51 | 0.9417 |
| gambar10.jpeg | 154.45 | 212.96 | 32.43 | 0.9203 |
| gambar11.jpeg | 200.31 | 300.77 | 32.43 | 0.9537 |
| gambar12.jpeg | 205.63 | 307.83 | 31.47 | 0.9300 |
| gambar13.jpeg | 186.65 | 309.23 | 33.58 | 0.9680 |
| gambar14.jpeg | 237.95 | 343.27 | 29.86 | 0.9247 |
| gambar15.jpeg | 205.81 | 294.07 | 32.62 | 0.9339 |
| gambar16.jpeg | 173.40 | 140.01 | 29.65 | 0.9397 |
| gambar17.jpeg | 84.53 | 120.85 | 29.47 | 0.9089 |
| gambar18.jpeg | 44.07 | 64.37 | 35.91 | 0.9440 |
| gambar19.jpeg | 85.03 | 122.64 | 29.58 | 0.9197 |
| gambar20.jpeg | 95.24 | 133.76 | 28.51 | 0.9056 |

> **Catatan:** Ukuran file compressed lebih besar karena DCT manual hanya melakukan
> quantization tanpa entropy coding (Huffman/RLE). Pengurangan kualitas terlihat pada
> metrik PSNR dan SSIM yang menunjukkan adanya kompresi lossy.

---

## 🧮 Penjelasan Metrik

| Metrik | Deskripsi | Interpretasi |
|--------|-----------|-------------|
| **PSNR** | Peak Signal-to-Noise Ratio | > 30 dB = Kualitas baik, > 40 dB = Sangat baik |
| **SSIM** | Structural Similarity Index | > 0.9 = Sangat mirip dengan original |
| **Compression Ratio** | Compressed / Original size | < 1.0 = File mengecil |

---

## 🚀 Cara Menjalankan

### Prasyarat
```bash
pip install numpy pandas matplotlib Pillow scipy scikit-image
```

### Google Colab (Recommended)
1. Upload `Algoritma_DCT.ipynb` ke [Google Colab](https://colab.research.google.com/)
2. Jalankan cell pertama untuk install dependencies
3. Upload 20 gambar dataset saat diminta
4. Jalankan semua cell secara berurutan

### Urutan Eksekusi

| No | Section | Keterangan |
|----|---------|-----------|
| 1 | Setup & Import | Install library & konfigurasi |
| 2 | Fungsi DCT | Definisi algoritma DCT manual |
| 3 | Upload Dataset | Upload gambar ke Colab |
| 4 | Demo DCT | Demonstrasi blok 8×8 pada 1 gambar |
| 5 | Batch Compression | Kompresi semua gambar + tampil before/after |
| 6 | Analisis Hasil | Hitung PSNR, SSIM, compression ratio |
| 7 | Multi-Quality | Perbandingan quality 10, 30, 50, 70, 90 |
| 8 | Visualisasi | Bar chart, scatter plot PSNR vs SSIM |
| 9 | Export CSV | Simpan hasil ke file CSV |

---

## 🛠️ Tech Stack

| Library | Kegunaan |
|---------|----------|
| `numpy` | Operasi matrix untuk pemrosesan blok 8×8 |
| `scipy.fftpack` | Implementasi DCT & Inverse DCT |
| `Pillow (PIL)` | I/O file gambar |
| `scikit-image` | Perhitungan PSNR & SSIM |
| `matplotlib` | Visualisasi grafik & gambar |
| `pandas` | Manajemen data & export CSV |

---


## 📝 Limitasi

- Implementasi DCT manual **tidak menyertakan entropy coding** (Huffman/RLE), sehingga ukuran file output bisa lebih besar dari input.
- Fokus proyek pada pemahaman algoritma DCT & Quantization, bukan optimasi ukuran file.
- Proses DCT manual menggunakan loop Python (lebih lambat dari library C-optimized seperti `libjpeg`).

---

<p align="center">
  <b>Praktikum Sistem Multimedia</b><br>
  Implementasi Algoritma Discrete Cosine Transform untuk Kompresi JPEG
</p>
