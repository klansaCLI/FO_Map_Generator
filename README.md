# FO_Map_Generator
FO Map Generator merupakan aplikasi berbasi Python (GUI) untuk pembuatan peta dasar (Base Map) jaringan fiber optik ke dalam format .DXF (Bisa untuk software CAD seperti AutoCAD). Dapat menghasilkan output file gambar .PNG Google Maps (Citra Default dan Satelit), Serta data vektor berupa bangunan dan jalan dari OpenStreetMap secara otomatis.

# FO Base Map & DXF Generator

Aplikasi desktop berbasis Python dengan antarmuka grafis (GUI) untuk mempercepat pembuatan gambar kerja peta dasar (*Base Map*) perencanaan jaringan Fiber Optik (FO) langsung ke dalam format **AutoCAD DXF (`.dxf`)**.

Cukup masukkan koordinat titik awal (**Titik A**) dan titik akhir (**Titik B**), aplikasi akan secara otomatis mengunduh citra peta, mengekstrak data vektor jalan dan bangunan, lalu menyusunnya menjadi file CAD siap pakai dengan skala meter (UTM).

---

## ✨ Fitur Utama

* **Otomatisasi Peta Dasar Multi-Layer (AutoCAD DXF R2018):**
  * Menghasilkan 3 tampilan peta sejajar dalam satu *modelspace*: **Peta Vektor OSM**, **Citra Google Maps Default**, dan **Citra Google Maps Satelit**.
  * Pemisahan *layer* otomatis: `OSM_BANGUNAN` (lengkap dengan *hatch*), `OSM_JALAN`, `OSM_TEKS` (nama jalan otomatis mengikuti sudut kemiringan jalan), `FRAME_BATAS`, dan `TITIK_ACUAN` (penanda Titik A & Titik B).
  * Konversi koordinat otomatis dari WGS84 (`Lat/Lon`) ke zona proyeksi **UTM (satuan Meter)** yang akurat.
* **Unduhan Citra Resolusi Tinggi:** Mengambil dan menggabungkan *tile* Google Maps (Zoom Level 18) serta memotongnya (*crop*) secara presisi sesuai batas area proyek dan *padding* yang ditentukan.
* **Server Cadangan Otomatis (*Fallback*):** Dilengkapi daftar beberapa server Overpass API (OpenStreetMap) untuk mencegah kegagalan unduhan apabila salah satu server sedang penuh.
* **Manajemen Antrean Proyek (Batch Processing):**
  * Tambah, edit, dan hapus daftar proyek pemetaan dengan penyimpanan konfigurasi lokal (`projects_config.json`).
  * Mendukung pemrosesan satu proyek terpilih maupun seluruh antrean proyek sekaligus di latar belakang (*multithreading*) tanpa membuat aplikasi *freeze*.
* **Sistem Aktivasi Lisensi (HWID Lock):** Dilengkapi dialog aktivasi berbasis *Hardware ID* perangkat serta tombol permintaan lisensi langsung via Gmail.

---

## 🚀 Cara Penggunaan (Versi `.exe`)

1. Unduh file aplikasi (`.exe`) melalui menu **Releases** di sebelah kanan halaman ini.
2. Jalankan aplikasi. Jika muncul jendela **Aktivasi Lisensi Aplikasi**, salin **Hardware ID** Anda dan kirimkan kepada pemilik *software* untuk mendapatkan **Product Key**.
3. Setelah aktif, isi detail proyek pada form **Detail Proyek Pemetaan**:
   * **Nama Proyek:** Nama folder dan file output `.dxf`.
   * **Padding Area (meter):** Jarak perluasan area peta di sekitar titik koordinat (default: `350` meter).
   * **Titik A & Titik B (Lat, Lon):** Koordinat awal dan akhir jalur dalam format desimal.
   * **Direktori Simpan:** Lokasi folder penyimpanan hasil.
4. Klik **+ Tambah Proyek** untuk memasukkan data ke tabel antrean.
5. Pilih proyek di tabel lalu klik **▶ Proses Proyek Terpilih** (atau **▶▶ Proses Semua Proyek**).
6. Pantau progres pada panel **Log Proses Real-Time**. Setelah selesai, buka folder output untuk mengakses file `.dxf` beserta gambar referensi `.png`.

---

## 🛠️ Teknologi yang Digunakan

* **GUI:** `Tkinter`
* **Pemrosesan Geospasial & Peta:** `OSMnx`, `GeoPandas`, `Shapely`
* **Generasi File CAD:** `ezdxf`
* **Pengolahan Citra & Jaringan:** `Pillow (PIL)`, `Requests`
