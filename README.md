# Analisis Perbandingan CNN from Scratch dan Transfer Learning untuk Klasifikasi Citra

Proyek ini mengeksplorasi dua pendekatan klasifikasi gambar dua kelas (biner) menggunakan arsitektur CNN yang dibangun dari dasar (*from scratch*) dan strategi *Transfer Learning* memanfaatkan model *pretrained* MobileNetV2. 

---

## 📊 Hasil Eksperimen dan Perbandingan Model

Berikut adalah tabel perbandingan performa komprehensif dari kedua model setelah melalui proses pengujian:

| Aspek Evaluasi            | CNN from Scratch (CIFAR-10) | Transfer Learning (MobileNetV2) |
| :---                      |            :---:            |              :---:              |
| **Akurasi Training**      | 82.45%                      | 98.10%                          |
| **Akurasi Validation**    | 71.20%                      | 96.50%                          |
| **Akurasi Testing**       | 70.85%                      | 96.25%                          |
| **Loss Training**         | 0.3952                      | 0.0621                          |
| **Loss Validation**       | 0.6841                      | 0.0915                          |
| **Waktu Training**        | ~5 Menit (30 Epochs)        | ~3 Menit (20 Epochs)            |
| **Jumlah Parameter**      | ~250.000 parameter          | ~2.3 Juta (Base) + Classifier   |
| **Risiko Overfitting**    | Tinggi                      | Rendah                          |
| **Kemudahan Implementasi**| Sedang (Tuning Manual)      | Mudah (Pretrained API)          |
| **Kesesuaian Dataset**    | Kurang untuk data kecil     | Sangat Optimal                  |

---

## 🔍 Analisis Hasil Projek

### 1. Analisis Dataset terhadap Performa Model
* **Kecukupan Data:** Jumlah dataset minimal (2.000 sampel) terbukti **tidak cukup** untuk melatih model CNN dari dasar agar mendapatkan kemampuan generalisasi yang baik. Akibatnya, model cenderung menghafal pola data *training*.
* **Kompleksitas Gambar:** Citra pada dataset memiliki variasi pencahayaan dan latar belakang yang kompleks. CNN dasar kesulitan mengekstrak fitur tingkat tinggi pada kondisi ini, berbeda dengan MobileNetV2 yang ekstraktor fiturnya sudah matang karena dilatih pada ImageNet.

### 2. Analisis Performa dan Stabilitas
* **Model Terbaik:** Pendekatan **Transfer Learning (MobileNetV2)** menghasilkan performa yang jauh lebih unggul dan stabil di setiap metrik evaluasi.
* **Identifikasi Overfitting:** Model CNN *from scratch* terindikasi mengalami *overfitting* yang cukup tinggi. Hal ini ditunjukkan oleh adanya *gap* (jarak) yang besar antara Akurasi Training (82.45%) dengan Akurasi Validation (71.20%). Sementara itu, model Transfer Learning menunjukkan grafik yang rapat dan konvergen stabil.

### 3. Argumentasi Pemilihan Pendekatan (Konteks Nyata)
Berdasarkan hasil eksperimen nyata ini, berikut adalah acuan krusial dalam pengambilan keputusan arsitektur:
* **Transfer Learning** wajib dipilih apabila ketersediaan data sangat terbatas, membutuhkan waktu pengerjaan yang cepat (efisiensi waktu), dan menginginkan akurasi tinggi langsung pada iterasi awal.
* **CNN from Scratch** baru relevan didesain jika kita memiliki volume data yang masif (ratusan ribu hingga jutaan gambar) dan karakteristik objeknya sangat spesifik/unik (tidak menyerupai objek umum di ImageNet).

---

## 📂 Struktur Repositori

```text
project-cnn-vs-transfer-learning/
│
├── dataset/
│   └── link_dataset.txt          # Sumber/tautan data CIFAR-10 & Cats vs Dogs 
├── notebook/
│   └── cnn_vs_transfer_learning.ipynb  # Source code eksperimen lengkap 
├── report/
│   └── laporan.pdf               # Laporan PDF formal 10 halaman (Template IEEE) 
└── README.md                     # Dokumentasi hasil projek 