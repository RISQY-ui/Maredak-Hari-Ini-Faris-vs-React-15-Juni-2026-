# Maredak-Hari-Ini-Faris-vs-React-15-Juni-2026-

# 📊 Rangkuman Maredak Hari Ini: Dari Backend hingga Frontend

## 15 Juni 2026

---

## 1. Masalah yang Berhasil Kita Selesaikan (Problem Solved)

| Aspek | Keterangan |
|-------|-------------|
| **Akar Masalah** | Saat mencoba membuat proyek React menggunakan perintah `@latest`, muncul error `SyntaxError: ... node:util ... styleText`. Ini terjadi karena installer Vite versi paling baru (Vite 6) tidak mendukung Node.js versi 18.19.1 yang terpasang di laptop |
| **Solusi Jenius** | Menurunkan versi installer menjadi **Vite versi 5** (`npm create vite@5`). Hasilnya 100% cocok, aman, dan lancar tanpa mengubah konfigurasi sistem Linux |

---

## 2. Langkah-Langkah yang Sukses Dieksekusi (Progress Checklist)

| No | Langkah | Status | Keterangan |
|----|---------|--------|-------------|
| 1 | Melahirkan Folder React | ✅ | Berhasil membuat folder `frontend-faris` di dalam folder utama praktek Laravel |
| 2 | Meracik Bahan Dasar | ✅ | `npm install` berhasil mengunduh seluruh paket dasar React.js |
| 3 | Uji Coba Server | ✅ | `npm run dev` berhasil menampilkan halaman template Vite + React di browser Firefox (diklik 29 kali!) |
| 4 | Menanam Kabel Gaib | ✅ | Mematikan server (`Ctrl + C`) dan menginstal Axios (`npm install axios`) sebagai alat penarik data dari Laravel |

---

## 3. Posisi di Roadmap Proyek

| Tahap | Status | Keterangan |
|-------|--------|-------------|
| Tahap 1 | ✅ Selesai | Setup awal |
| Tahap 2 | ✅ Selesai | Persiapan frontend |
| Tahap 3 | ✅ Selesai | Instalasi Axios |
| Tahap 4 | 🔄 Selanjutnya | **Integrasi API** |

### Langkah Selanjutnya (Next Step):

1. Buka file `App.jsx`
2. Bersihkan kode bawaannya
3. Tembakkan kabel Axios ke alamat URL Laravel:
```

http://127.0.0.1:8000/nama-model

```
4. Agar data muncul di layar

---

## 📝 Ringkasan Status

| Komponen | Status |
|----------|--------|
| Backend Laravel | ✅ Selesai |
| Endpoint `/nama-model` | ✅ Siap |
| React + Vite 5 | ✅ Terinstall |
| Axios | ✅ Terinstall |
| Server Frontend | ✅ Bisa jalan (`npm run dev`) |
| Integrasi API | ⏸️ Belum (langkah selanjutnya) |

---

> Dokumentasi perjalanan Full-Stack Faris - 15 Juni 2026. Dari error Vite 6 hingga siap integrasi API.

# 📖 Bedah Syntax Laravel

## 1. Di dalam `NamaController.php` (Otak Aplikasi)

| Kode | Artinya |
|------|---------|
| `namespace App\Http\Controllers;` | Ini seperti alamat rumah file ini di dalam folder proyek. Biar Laravel tidak tersesat saat mencarinya. |
| `use App\Models\NamaModel;` | Perintah untuk "memanggil" file Model yang memegang database. Tanpa baris ini, Controller tidak akan bisa menyentuh tabel data kita. |
| `$data = NamaModel::all();` | Perintah sakti untuk mengambil **SEMUA (all())** isi baris data yang ada di dalam tabel database tanpa terkecuali. |
| `return response()->json($data);` | Mengubah data dari database menjadi format **JSON** (format teks standar internasional yang paling disukai oleh React.js dan AI), lalu mengirimkannya ke layar browser. |

---

## 2. Di dalam `routes/web.php` (Jembatan URL)

| Kode | Artinya |
|------|---------|
| `use App\Http\Controllers\NamaController;` | Mengenalkan `NamaController` kepada sistem jalanan/rute Laravel. |
| `Route::get('/nama-model', [NamaController::class, 'index']);` | `Route::get` artinya membuat rute bertipe GET (membaca halaman). Kalau ada yang mengetik `/nama-model` di browser, oper tugasnya ke `NamaController` khusus pada bagian fungsi `index()`. |

---

## 3. Perintah Membuat Data Palsu di Tinker

```php
App\Models\NamaModel::create([
    'nama_model' => 'Proyek Pertama Faris', 
    'status' => true
]);
