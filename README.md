# Analisis Sentimen Media Sosial terhadap Volatilitas IHSG selama Demonstrasi Politik 2025: Pendekatan Random Forest

Repositori ini memuat notebook pipeline yang menjadi lampiran skripsi Akuntansi
[Nama Penulis], [Universitas], [Tahun].

Pipeline terdiri atas delapan notebook Jupyter bernomor yang mendokumentasikan seluruh
proses penelitian secara berurutan: pengumpulan unggahan media sosial, penggabungan data,
praproses teks, pelabelan dan skoring sentimen, pembentukan panel harian bersama data
IHSG, sampai pemodelan Random Forest dan pengujiannya.

Ruang lingkup data:

- Periode unggahan: 1 Juni 2025 sampai 31 Oktober 2025.
- Korpus akhir setelah pembersihan dan pelabelan: 14.050 dokumen.
- Data pasar: IHSG (ticker `^JKSE`) melalui yfinance, volatilitas dihitung dengan jendela 5 hari.
- Panel final untuk pemodelan: [jumlah observasi, sesuaikan dengan Bab IV].

Data mentah hasil scraping tidak disertakan di repositori ini. Lihat bagian
[Sumber data](#sumber-data) dan [Keluaran](#keluaran-yang-diunggah-dan-yang-tidak).

## Struktur repositori

```
ihsg-sentimen/
├── README.md
├── requirements.txt
├── .gitignore
├── 01_scraping_kalimat_ganda.ipynb
├── 01a_scraping_bertahap.ipynb
├── 02_penggabungan_data.ipynb
├── 03_praproses_sentimen.ipynb
├── 04_skor_sentimen.ipynb
├── 05_pra_cleaning.ipynb
├── 05a_label_manual_pendukung.ipynb
├── 06_rantai_pipeline.ipynb
├── data/
│   ├── raw/         (.gitkeep; hasil scraping, tidak diunggah)
│   └── processed/   (.gitkeep; data antara per dokumen, tidak diunggah)
└── outputs/
    └── [daftar berkas agregat, tabel, dan gambar yang diunggah]
```

## Kebutuhan

Python 3.12 dengan pustaka berikut:

```
langdetect
matplotlib
numpy
openpyxl
pandas
pyarrow
requests
scipy
scikit-learn
torch
transformers
yfinance
```

Pemasangan:

```bash
pip install -r requirements.txt
```

## Sumber data

Tidak ada data mentah yang diunggah. Data diperoleh dari sumber aslinya.

| Data | Periode | Sumber | Keterangan |
|---|---|---|---|
| Unggahan media sosial X | 1 Juni 2025 sampai 31 Oktober 2025 | Dikumpulkan melalui layanan twitterapi.io | Memerlukan kunci API sendiri; isi unggahan tidak disebarkan ulang |
| IHSG harian | [periode, sesuaikan] | Yahoo Finance, ticker `^JKSE`, melalui pustaka yfinance | Diunduh ulang oleh notebook 06 |

## Urutan notebook

Notebook dibaca sesuai urutan nomor. Keluaran setiap notebook menjadi masukan notebook
berikutnya.

| No | Notebook | Fungsi |
|---|---|---|
| 01 | `01_scraping_kalimat_ganda.ipynb` | Pengumpulan data dengan kata kunci ganda |
| 01a | `01a_scraping_bertahap.ipynb` | Pengumpulan data per periode |
| 02 | `02_penggabungan_data.ipynb` | Penggabungan data hasil scraping |
| 03 | `03_praproses_sentimen.ipynb` | Penyaringan bahasa, duplikasi, relevansi, dan panjang teks |
| 04 | `04_skor_sentimen.ipynb` | Pelabelan awal dan skoring sentimen |
| 05 | `05_pra_cleaning.ipynb` | Konsensus pelabelan dan pemisahan label netral |
| 05a | `05a_label_manual_pendukung.ipynb` | Pendukung pelabelan manual |
| 06 | `06_rantai_pipeline.ipynb` | NST harian, volatilitas IHSG, panel final, model H1 dan H2, uji ketahanan, uji kontrol |

## Keluaran: yang diunggah dan yang tidak

Diunggah (hasil agregat, tanpa data tingkat dokumen):

- [daftar berkas di `outputs/`, misalnya NST harian, NST per periode, tabel hasil, dan gambar Bab IV]

Tidak diunggah:

- data mentah hasil scraping, karena memuat nama pengguna dan isi unggahan;
- data skor sentimen per dokumen, karena memuat teks unggahan;
- folder model `models_sentimen/`, karena ukurannya besar;
- kunci API.

## Catatan reproduksi

1. Notebook adalah dokumentasi proses, bukan skrip yang dijalankan sekali dari atas ke bawah.
   Nomor eksekusi sel pada notebook 04, 05, dan 06 tidak berurutan karena sebagian sel
   dijalankan ulang selama pengembangan.
2. Path berkas di dalam notebook (misalnya `G:\My Drive\skripsi\...` dan `C:\Users\...`)
   adalah path komputer penulis. Sesuaikan path jika ingin menjalankan ulang.
3. Sel pertama notebook 01a menampilkan Error 401 dari percobaan awal sebelum kunci API aktif.
4. Kunci API tidak disertakan. Ganti `ISI_KEY_ANDA` dengan kunci twitterapi.io milik sendiri.
5. Reproduksi penuh memerlukan pengumpulan ulang data unggahan, sehingga hasilnya dapat
   berbeda bila unggahan asli sudah dihapus atau tidak lagi tersedia.

## Lisensi

Kode dirilis dengan lisensi MIT; lihat berkas `LICENSE`. Lisensi hanya mencakup kode.
Data eksternal tetap tunduk pada ketentuan penyedia aslinya.

## Rujukan

[Nama Penulis]. ([Tahun]). *Analisis Sentimen Media Sosial terhadap Volatilitas IHSG selama
Demonstrasi Politik 2025: Pendekatan Random Forest*. Skripsi, [Program Studi], [Universitas].
