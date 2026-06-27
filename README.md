# Klasifikasi Penyakit Parkinson dengan Support Vector Machine

Implementasi dan analisis Support Vector Machine (SVM) untuk klasifikasi penyakit Parkinson berbasis suara. Proyek ini mereplikasi paper Elshewey et al. (2023), menganalisis keterbatasannya secara kritis, lalu menerapkan metodologi *best practice* pada dataset yang lebih besar.

> Studi kasus paper: **Elshewey et al. (2023). Bayesian Optimization with Support Vector Machine Model for Parkinson Disease Classification. _Sensors_, 23(4), 2085.** https://doi.org/10.3390/s23042085

---

## Ringkasan Temuan

| Tahap | Dataset | Metodologi | Hasil |
|---|---|---|---|
| 1. Replikasi | UCI (195 rekaman) | Split acak 60/40 | Accuracy **92,3%** (mereproduksi paper persis) |
| 2. Dataset alternatif | Sakar (756 rekaman) | Grid 4 kernel x 3 split, per-subjek | Accuracy terbaik **89,5%** (kernel linear) |
| 3. Best practice | Sakar (756 rekaman) | GroupKFold CV, class-balanced | **Balanced Accuracy 75,8%, ROC-AUC 0,836** |

**Kesimpulan utama:** akurasi tinggi 92-95% pada dataset kecil sebagian besar adalah ilusi akibat kebocoran data antar-subjek dan penggunaan metrik *accuracy* pada data tidak seimbang. Setelah metodologi diperbaiki (dataset lebih besar, pembagian per-subjek, validasi silang, metrik *balanced*), diperoleh estimasi kinerja yang jujur sekitar 76% *balanced accuracy*. Setelah metodologi benar, pilihan kernel hampir tidak berpengaruh.

---

## Struktur Folder

```
parkinson-svm-classification/
├── README.md
├── requirements.txt
├── LICENSE
├── .gitignore
├── data/
│   ├── raw/
│   │   ├── parkinsons.data            # dataset asli (Little 2007)
│   │   └── pd_speech_features.csv     # dataset Sakar 2018
│   └── README.md                      # sumber & lisensi data
├── notebooks/
│   ├── 01_replikasi_paper.ipynb       # replikasi paper (dataset asli)
│   ├── 02_dataset_alternatif.ipynb    # dataset Sakar, split per-subjek
│   └── 03_best_practice.ipynb         # metodologi best practice
└── reports/
    ├── Laporan_SVM_Parkinson.docx     # laporan lengkap
    └── figures/                       # gambar hasil eksperimen
```

---

## Instalasi

```bash
# (opsional) buat virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# pasang dependensi
pip install -r requirements.txt
```

## Cara Menjalankan

```bash
jupyter notebook
```

Buka notebook di folder `notebooks/` sesuai urutan (01 → 02 → 03). Setiap notebook akan mengunduh dataset secara otomatis bila belum tersedia, sehingga dapat dijalankan langsung. Salinan lokal dataset juga tersedia di `data/raw/`.

---

## Metodologi Singkat

Penelitian dilakukan dalam tiga tahap:

1. **Replikasi paper** pada dataset asli (UCI Parkinsons, 195 rekaman): SVM empat kernel disetel dengan Bayesian Optimization, mengikuti pipeline paper.
2. **Replikasi pada dataset alternatif** (Sakar 2018, 756 rekaman): metode yang sama namun dengan pembagian **per-subjek** (GroupShuffleSplit + GroupKFold) untuk mencegah kebocoran data.
3. **Best practice**: Pipeline anti-kebocoran, validasi silang per-subjek (GroupKFold), penanganan ketidakseimbangan kelas (`class_weight='balanced'`), pelaporan *balanced accuracy*/ROC-AUC/sensitivitas/spesifisitas, baseline, dan *feature selection*.

Penyetelan hyperparameter menggunakan **Bayesian Optimization** (scikit-optimize).

---

## Dataset

Lihat [`data/README.md`](data/README.md) untuk sumber, lisensi, dan deskripsi lengkap.

- **Dataset asli**: UCI Parkinsons (Little et al., 2007) — 195 rekaman, 22 fitur, 31 subjek.
- **Dataset alternatif**: Parkinson's Disease Classification (Sakar et al., 2018) — 756 rekaman, 752 fitur, 252 subjek. Lisensi CC BY 4.0.

---

## Sitasi

```bibtex
@article{elshewey2023bosvm,
  title={Bayesian Optimization with Support Vector Machine Model for Parkinson Disease Classification},
  author={Elshewey, Ahmed M. and Shams, Mahmoud Y. and El-Rashidy, Nora and Elhady, Abdelghafar M. and Shohieb, Samaa M. and Tarek, Zahraa},
  journal={Sensors},
  volume={23}, number={4}, pages={2085}, year={2023},
  doi={10.3390/s23042085}
}
```

---

## Lisensi

Kode pada repositori ini dirilis di bawah lisensi MIT — lihat [LICENSE](LICENSE). Dataset mengikuti lisensi masing-masing (lihat `data/README.md`).

## Penulis

Faisal Akbar — 187241107 — Sistem Informasi
