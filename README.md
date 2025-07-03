# MarshandaGwi_DE_Challenge

Repository ini berisi solusi dan dokumentasi untuk **Data Engineering Challenge** dari *Synapsis Data Engineer Intern Program*.

## 📁 Struktur Folder

- `challenge1/`  
  Berisi perencanaan (planning) proses anotasi untuk label dataset.

- `challenge2/`  
  Berisi dataset mentah (raw) yang belum diberi label, beserta deskripsi proses pengumpulan data (*data collection*).

- `challenge3/`  
  Berisi dataset yang sudah diberi label (annotated), lengkap dengan notebook Python untuk:
  - menampilkan contoh gambar dan bounding box,
  - serta menganalisis statistik distribusi label dari tiap kelas PPE.
 
## ✅ Checklist Fitur dan Kendala

- **Skema Labeling dan Pertimbangan**  (Done)

- **Panduan Anotasi**  (Done)

- **Dataset Gambar Tanpa Anotasi**  (Done)

- **Dataset Gambar dengan Anotasi**  (Done)

- **Dataset Preview Script**  (Done)

- **Dataset Summary Statistics**  (Done)

## 📸 Proses Pengumpulan & Pelabelan Dataset

### 1. Pengumpulan Dataset (Data Collection)
Dataset dikumpulkan dengan pendekatan **manual crawling** menggunakan mesin pencari gambar seperti Google Images serta diambil manual dari Kaggle, dengan kata kunci terkait alat pelindung diri (PPE) seperti:

- `"construction worker gloves"`
- `"person wearing hard hat"`
- `"safety glasses on site"`
- `"high visibility vest"`
- `"steel toe boots"`
- `"PPE Dataset"`
- `"SH17 Dataset"`

Gambar yang dikumpulkan merupakan representasi berbagai kondisi lingkungan kerja, sudut pandang kamera, dan beragam pencahayaan untuk memperkaya *variasi data*. File disimpan dalam folder `challenge2/dataset` sebagai dataset mentah.

### 2. Persiapan Labeling di Roboflow
Setelah gambar terkumpul, langkah berikutnya adalah proses pelabelan (*annotation*), dilakukan menggunakan [Roboflow](https://roboflow.com/) karena kemudahan UI dan integrasi ekspor.

Berikut tahapannya:

1. **Upload Dataset ke Roboflow**
   - Masuk ke Roboflow dan buat proyek baru dengan tipe `Object Detection`.
   - Unggah seluruh gambar dari `challenge2/dataset`.

2. **Anotasi Label**
   - Gunakan tools `bounding box` di Roboflow untuk melabel objek sesuai 5 kategori PPE:
     - `gloves`
     - `hard_hat`
     - `safety_glasses`
     - `safety_vest`
     - `steel_toe_boot`
   - Setiap objek diberi label manual dengan perhatian terhadap akurasi dan konsistensi anotasi juga size dari bounding box tersebut.

3. **Ekspor Dataset**
   - Setelah semua gambar selesai dilabeli, dataset diekspor dengan format `YOLOv12`.
   - File hasil ekspor berisi:
     - Folder `images/` (gambar asli)
     - Folder `labels/` (file `.txt` format YOLO)

4. **Integrasi ke Google Drive**
   - Dataset hasil anotasi dimasukkan ke folder `challenge3/` di Google Drive.
   - Seluruh struktur dataset (images & labels) siap digunakan untuk visualisasi dan analisis statistik.

## 🛠️ Cara Menjalankan Program

Proyek ini dijalankan menggunakan **Python Notebook** di **Google Colab**. Berikut adalah langkah-langkah untuk menjalankannya:

1. **Siapkan Folder di Google Drive**  
   Buat folder baru di Google Drive untuk menyimpan dataset yang sudah dilabel:
   your-folder/
   ├── images/ ← folder berisi gambar
   └── labels/ ← folder berisi file label (.txt)

3. **Buat File Notebook**
   Di dalam folder yang sama (`your-folder`), buat file notebook Colab (contoh: `preview_dataset.ipynb`).

4. **Mount Google Drive di Colab**
   Di awal notebook, jalankan kode berikut untuk mengakses file di Google Drive:
```python
from google.colab import drive
drive.mount('/content/drive')
```
5. **Sesuaikan Path Folder**
   Ubah IMAGE_DIR dan LABEL_DIR pada kode agar sesuai dengan lokasi folder di Drive. Contoh:
   IMAGE_DIR = "/content/drive/MyDrive/your-folder/images"
   LABEL_DIR = "/content/drive/MyDrive/your-folder/labels"

7. Jalankan Semua Cell Notebook
   Setelah path disesuaikan, jalankan seluruh cell untuk melihat hasil bounding box dan distribusi label.

Catatan:
Tidak ada framework tambahan yang dibutuhkan selain library Python standar seperti cv2, matplotlib, dan os, yang sudah tersedia di Google Colab.


## 📬 Kontak

**Marshanda Gwi**  
📧 Email: marshandasugiarto@gmail.com
