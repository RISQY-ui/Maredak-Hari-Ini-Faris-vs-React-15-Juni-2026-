# 📚 KITAB LENGKAP FARIS: BACKEND → FRONTEND

## Dari Laravel ke React.js - 15-16 Juni 2026

---

## 📊 RANGKUMAN MAREDAK HARI INI: DARI BACKEND HINGGA FRONTEND

### 1. Masalah yang Berhasil Kita Selesaikan (Problem Solved)

| Aspek | Keterangan |
|-------|-------------|
| **Akar Masalah** | Saat mencoba membuat proyek React menggunakan perintah `@latest`, muncul error `SyntaxError: ... node:util ... styleText`. Ini terjadi karena installer Vite versi paling baru (Vite 6) tidak mendukung Node.js versi 18.19.1 yang terpasang di laptop |
| **Solusi Jenius** | Menurunkan versi installer menjadi **Vite versi 5** (`npm create vite@5`). Hasilnya 100% cocok, aman, dan lancar tanpa mengubah konfigurasi sistem Linux |

### 2. Langkah-Langkah yang Sukses Dieksekusi (Progress Checklist)

| No | Langkah | Status | Keterangan |
|----|---------|--------|-------------|
| 1 | Melahirkan Folder React | ✅ | Berhasil membuat folder `frontend-faris` di dalam folder utama praktek Laravel |
| 2 | Meracik Bahan Dasar | ✅ | `npm install` berhasil mengunduh seluruh paket dasar React.js |
| 3 | Uji Coba Server | ✅ | `npm run dev` berhasil menampilkan halaman template Vite + React di browser Firefox |
| 4 | Menanam Kabel Gaib | ✅ | Mematikan server (`Ctrl + C`) dan menginstal Axios (`npm install axios`) sebagai alat penarik data dari Laravel |

### 3. Posisi di Roadmap Proyek

| Tahap | Status | Keterangan |
|-------|--------|-------------|
| Tahap 1 | ✅ Selesai | Setup awal |
| Tahap 2 | ✅ Selesai | Persiapan frontend |
| Tahap 3 | ✅ Selesai | Instalasi Axios |
| Tahap 4 | ✅ Selesai | **Integrasi API + CORS** |

---

## 🚨 CORS ERROR & SOLUSI (16 Juni 2026)

### Masalah yang Ditemukan

| Aspek | Keterangan |
|-------|-------------|
| **Waktu** | 18.21 WIB |
| **Pesan Error** | `Cross-Origin Request Blocked: ... (Reason: CORS header 'Access-Control-Allow-Origin' missing). Status code: 200.` |
| **Biang Keroknya** | Laravel secara default hanya membuka gerbang CORS otomatis untuk file `routes/api.php`. Karena rute `/nama-model` ditaruh di `routes/web.php`, Laravel mendeteksi panggilan Axios dari React sebagai ancaman asing dan langsung mengunci pintunya |

### Solusi

| Langkah | Perintah | Keterangan |
|---------|----------|-------------|
| 1 | Buka file `config/cors.php` | Di VS Code Laravel |
| 2 | Ubah `'paths' => ['api/*', 'sanctum/csrf-cookie']` | Menjadi `'paths' => ['*']` |
| 3 | `Ctrl + S` | Simpan perubahan |

### Hasil Akhir

| Status | Keterangan |
|--------|-------------|
| ✅ **Sukses Total 100%!** | Console Firefox langsung bersih total dari warna merah |
| ✅ **Koneksi Lancar** | Tampilan React berhasil menampilkan data dari Laravel |

---

## 📖 BEDAH SYNTAX LARAVEL

### 1. Di dalam `NamaController.php` (Otak Aplikasi)

| Kode | Artinya |
|------|---------|
| `namespace App\Http\Controllers;` | Alamat rumah file ini di dalam folder proyek. Biar Laravel tidak tersesat saat mencarinya. |
| `use App\Models\NamaModel;` | Perintah memanggil file Model yang memegang database. Tanpa ini, Controller tidak bisa menyentuh tabel data. |
| `$data = NamaModel::all();` | Perintah sakti mengambil **SEMUA (all())** isi baris data di dalam tabel database. |
| `return response()->json($data);` | Mengubah data menjadi format **JSON** (disukai React.js), lalu mengirimkannya ke browser. |

### 2. Di dalam `routes/web.php` (Jembatan URL)

| Kode | Artinya |
|------|---------|
| `use App\Http\Controllers\NamaController;` | Mengenalkan `NamaController` kepada sistem rute Laravel. |
| `Route::get('/nama-model', [NamaController::class, 'index']);` | Membuat rute GET. Kalau ada yang buka `/nama-model`, oper ke `NamaController` fungsi `index()`. |

### 3. Perintah Membuat Data Palsu di Tinker

```php
App\Models\NamaModel::create([
    'nama_model' => 'Proyek Pertama Faris', 
    'status' => true
]);
```

---

💻 KITAB SUCI KODING FARIS: PERINTAH TERMINAL & SYNTAX LENGKAP

1. Kumpulan Perintah Terminal

```bash
# 1. Membuat proyek Laravel baru
composer create-project laravel/laravel nama-proyek-laravel

# 2. Menyalakan server Backend Laravel
php artisan serve

# 3. Membuat Model & Migration sekaligus
php artisan make:model NamaModel -m

# 4. Meresmikan tabel ke database
php artisan migrate

# 5. Membuat Controller API
php artisan make:controller NamaController --api

# 6. Masuk ke mode Tinker
php artisan tinker

# 7. Perintah darurat (bubarkan antrean Linux terkunci)
sudo kill -9 9098
sudo rm /var/lib/dpkg/lock-frontend
sudo rm /var/lib/apt/lists/lock
sudo rm /var/cache/apt/archives/lock
sudo dpkg --configure -a

# 8. Mundur satu folder
cd ..

# 9. Install Node.js & NPM untuk React
sudo apt install nodejs npm
```

2. Kumpulan Kode di Dalam File

A. File Struktur Tabel Database

📍 Lokasi: database/migrations/..._create_nama_models_table.php

```php
public function up(): void
{
    Schema::create('nama_models', function (Blueprint $table) {
        $table->id();
        $table->string('nama_model');
        $table->boolean('status')->default(true);
        $table->timestamps();
    });
}
```

B. File Controller

📍 Lokasi: app/Http/Controllers/NamaController.php

```php
<?php

namespace App\Http\Controllers;

use App\Models\NamaModel;
use Illuminate\Http\Request;

class NamaController extends Controller
{
    public function index()
    {
        $data = NamaModel::all();
        return response()->json($data);
    }
}
```

C. File Routing

📍 Lokasi: routes/web.php

```php
<?php

use App\Http\Controllers\NamaController;

Route::get('/nama-model', [NamaController::class, 'index']);
```

D. File CORS Configuration

📍 Lokasi: config/cors.php

```php
'paths' => ['*'],  // Diubah dari ['api/*', 'sanctum/csrf-cookie']
```

E. File App.jsx (React)

📍 Lokasi: frontend-faris/src/App.jsx

```jsx
import { useState, useEffect } from 'react';
import axios from 'axios';

function App() {
  const [data, setData] = useState([]);

  useEffect(() => {
    axios.get('http://127.0.0.1:8000/nama-model')
      .then(response => {
        setData(response.data);
      })
      .catch(error => {
        console.error('Error fetching data:', error);
      });
  }, []);

  return (
    <div>
      <h1>Data dari Laravel:</h1>
      <ul>
        {data.map(item => (
          <li key={item.id}>
            <strong>{item.nama_model}</strong> - Status: {item.status ? 'Aktif' : 'Tidak Aktif'}
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;
```

---

🗺️ ALUR LENGKAP BACKEND → FRONTEND FARIS

Alur 1: Mengurus Gudang & Bahan (Database ke Laravel)

Langkah Perintah Keterangan
1 php artisan make:model NamaModel -m Bikin kamar di database + kunci kamar (Model)
2 Edit file migration Tambah kolom nama_model dan status
3 php artisan migrate Resmikan tabel ke database
4 php artisan tinker Masuk mode simulasi
5 NamaModel::create([...]) Isi satu contoh data

Alur 2: Mengolah Bahan Menjadi Siap Saji (Laravel ke API)

Langkah Perintah Keterangan
1 php artisan make:controller NamaController --api Bikin Koki (Controller)
2 Edit NamaController.php Isi fungsi index() dengan NamaModel::all() dan response()->json()
3 Edit routes/web.php Tambah Route::get('/nama-model', [NamaController::class, 'index'])
4 php artisan serve Buka jendela toko
5 Akses http://127.0.0.1:8000/nama-model Lihat bungkusan JSON di browser

Alur 3: Menyajikan ke Pengunjung (React.js)

Langkah Perintah Keterangan
1 sudo apt install nodejs npm Siapkan alat kerja React
2 npm create vite@5 Bikin folder proyek React
3 npm install Masak bahan dasar React
4 npm install axios Pasang alat penarik data
5 Edit App.jsx Tulis kode ambil data dari Laravel
6 npm run dev Sajikan ke pengunjung

Alur 4: Mengatasi CORS (Gembok Nakal)

Langkah Perintah Keterangan
1 Buka config/cors.php File konfigurasi CORS Laravel
2 Ubah 'paths' => ['api/*', 'sanctum/csrf-cookie'] Menjadi 'paths' => ['*']
3 Ctrl + S Simpan perubahan
4 Refresh browser Data langsung muncul!

---

🎯 INTI ALUR (PALING SEDERHANA)

Bikin Datanya → Pancarkan lewat Laravel → Buka Gembok CORS → Ambil dan Percantik pakai React.js

---

✅ RINGKASAN STATUS AKHIR

Komponen Status
Backend Laravel ✅ Selesai
Endpoint /nama-model ✅ Siap
CORS Configuration ✅ Diperbaiki (paths => ['*'])
React + Vite 5 ✅ Terinstall
Axios ✅ Terinstall
Server Frontend ✅ Bisa jalan (npm run dev)
Integrasi API ✅ SELESAI! Data muncul di layar
Console Firefox ✅ Bersih, tanpa error merah

---

💡 PELAJARAN PENTING

Pelajaran Keterangan
Vite Vite 6 tidak support Node.js 18.19.1 → pakai Vite 5
CORS Laravel secara default hanya mengizinkan CORS untuk route api/*
Solusi CORS Ubah 'paths' => ['api/*', 'sanctum/csrf-cookie'] menjadi 'paths' => ['*']
Tanda Bintang (*) Artinya mengizinkan semua rute, cocok untuk development lokal
Axios Alat penarik data dari backend ke frontend

---

Kitab Lengkap Faris: Backend → Frontend - Disusun oleh faris untuk belajar dan memahami. Dari Laravel ke React.js, semua perintah, syntax, error, dan solusi ada di sini. 
