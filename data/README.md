# Dataset

Folder ini berisi dua dataset suara untuk klasifikasi penyakit Parkinson.

## 1. `raw/parkinsons.data` — Dataset Asli (UCI Parkinsons)

- **Sumber**: UCI Machine Learning Repository
- **Pembuat**: Max A. Little (University of Oxford), bekerja sama dengan National Centre for Voice and Speech (2007)
- **Tautan**: https://archive.ics.uci.edu/dataset/174/parkinsons
- **Ukuran**: 195 rekaman, 22 fitur fonetik, 31 subjek (23 PD, 8 sehat)
- **Target**: kolom `status` (1 = Parkinson, 0 = sehat)
- **Catatan**: setiap subjek menyumbang ± 6 rekaman; kelas tidak seimbang (± 75% PD).

Sitasi:
> Little, M. A., McSharry, P. E., Roberts, S. J., Costello, D. A., & Moroz, I. M. (2007). Exploiting Nonlinear Recurrence and Fractal Scaling Properties for Voice Disorder Detection. UCI Machine Learning Repository.

## 2. `raw/pd_speech_features.csv` — Dataset Alternatif (Sakar 2018)

- **Sumber**: UCI Machine Learning Repository (ID 470)
- **Pembuat**: C. O. Sakar dkk. (2018)
- **Tautan**: https://archive.ics.uci.edu/dataset/470/parkinson+s+disease+classification
- **DOI**: https://doi.org/10.24432/C5MS4X
- **Lisensi**: Creative Commons Attribution 4.0 (CC BY 4.0)
- **Ukuran**: 756 rekaman, 752 fitur suara, 252 subjek (188 PD, 64 sehat)
- **Target**: kolom `class` (1 = Parkinson, 0 = sehat)
- **Catatan penting**: file memiliki dua baris header (baris pertama nama grup fitur), sehingga dibaca dengan `header=1`. Kolom `id` adalah identitas subjek dan dipakai untuk pembagian per-subjek (bukan sebagai fitur). Setiap subjek memiliki 3 rekaman.

Sitasi:
> Sakar, C. O., Serbes, G., Gunduz, A., Nizam, H., & Sakar, B. (2018). Parkinson's Disease Classification [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5MS4X

---

Kedua dataset bersifat publik dan disertakan di sini untuk kemudahan reproduksi. Notebook juga akan mengunduh dataset secara otomatis bila tidak ditemukan.
