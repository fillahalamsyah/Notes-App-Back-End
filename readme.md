# Aplikasi Backend Catatan (Notes App)

Layanan RESTful API backend untuk aplikasi catatan yang dibangun dengan Hapi.js. Aplikasi ini memungkinkan pengguna untuk membuat, membaca, memperbarui, dan menghapus catatan.

## Fitur Aplikasi

- Membuat catatan baru dengan judul, tag, dan konten
- Mengambil semua catatan yang tersimpan
- Mendapatkan catatan berdasarkan ID
- Memperbarui catatan yang sudah ada
- Menghapus catatan yang tidak diperlukan lagi

## Teknologi yang Digunakan

- **Node.js** - Runtime JavaScript untuk menjalankan aplikasi server
- **Hapi.js** - Framework web server yang kuat dan fleksibel
- **nanoid** - Library untuk menghasilkan ID unik

## Struktur Proyek

```
notes-app-back-end/
├── src/
│   ├── handler.js      # Penangan permintaan untuk setiap rute API
│   ├── notes.js        # Penyimpanan data catatan (array)
│   ├── routes.js       # Definisi endpoint API
│   └── server.js       # Konfigurasi server Hapi.js
├── package.json        # Informasi proyek dan dependensi
├── postman_test/       # Koleksi dan environment untuk pengujian API
│   ├── notes-api-test.postman_collection.json
│   └── notes-api-test.postman_environment.json
└── README.md           # Dokumentasi proyek
```

## Endpoint API

| Metode | Endpoint    | Deskripsi                          | Response Code              |
| ------ | ----------- | ---------------------------------- | -------------------------- |
| POST   | /notes      | Membuat catatan baru               | 201 (Created)              |
| GET    | /notes      | Mengambil semua catatan            | 200 (OK)                   |
| GET    | /notes/{id} | Mengambil catatan berdasarkan ID   | 200 (OK) / 404 (Not Found) |
| PUT    | /notes/{id} | Memperbarui catatan berdasarkan ID | 200 (OK) / 404 (Not Found) |
| DELETE | /notes/{id} | Menghapus catatan berdasarkan ID   | 200 (OK) / 404 (Not Found) |

## Langkah-langkah Instalasi

1. Clone repositori dari GitHub:

   ```bash
   git clone [URL repositori Anda]
   cd notes-app-back-end
   ```

2. Instalasi semua dependensi:
   ```bash
   npm install
   ```

## Cara Menjalankan Aplikasi

Jalankan server pengembangan dengan fitur restart otomatis saat ada perubahan kode:

```bash
npm start
```

Server akan berjalan pada alamat: http://localhost:5000

## Struktur Data Catatan

Setiap catatan (note) memiliki struktur data sebagai berikut:

```json
{
  "id": "string (dihasilkan otomatis)",
  "title": "string (judul catatan)",
  "tags": ["array of strings (tag catatan)"],
  "body": "string (isi catatan)",
  "createdAt": "string (timestamp ISO saat pembuatan)",
  "updatedAt": "string (timestamp ISO saat pembaruan)"
}
```

## Panduan Penggunaan API

### 1. Membuat Catatan Baru

**Endpoint:** `POST /notes`

**Request Body:**

```json
{
  "title": "Judul Catatan",
  "tags": ["tag1", "tag2"],
  "body": "Isi catatan di sini"
}
```

**Response (201):**

```json
{
  "status": "success",
  "message": "Catatan berhasil ditambahkan",
  "data": {
    "noteId": "ID-yang-dihasilkan"
  }
}
```

**Contoh dengan curl:**

```bash
curl -X POST http://localhost:5000/notes \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Catatan Penting",
    "tags": ["penting", "tugas"],
    "body": "Isi catatan penting di sini"
  }'
```

### 2. Mengambil Semua Catatan

**Endpoint:** `GET /notes`

**Response (200):**

```json
{
  "status": "success",
  "data": {
    "notes": [
      {
        "id": "string",
        "title": "string",
        "tags": ["string"],
        "body": "string",
        "createdAt": "string",
        "updatedAt": "string"
      }
      // ...catatan lainnya
    ]
  }
}
```

**Contoh dengan curl:**

```bash
curl http://localhost:5000/notes
```

### 3. Mengambil Catatan Berdasarkan ID

**Endpoint:** `GET /notes/{id}`

**Response Sukses (200):**

```json
{
  "status": "success",
  "data": {
    "note": {
      "id": "string",
      "title": "string",
      "tags": ["string"],
      "body": "string",
      "createdAt": "string",
      "updatedAt": "string"
    }
  }
}
```

**Response Gagal (404):**

```json
{
  "status": "fail",
  "message": "Catatan tidak ditemukan"
}
```

**Contoh dengan curl:**

```bash
curl http://localhost:5000/notes/ID-catatan-anda
```

### 4. Memperbarui Catatan

**Endpoint:** `PUT /notes/{id}`

**Request Body:**

```json
{
  "title": "Judul Catatan yang Diperbarui",
  "tags": ["tag-baru"],
  "body": "Isi catatan yang diperbarui"
}
```

**Response Sukses (200):**

```json
{
  "status": "success",
  "message": "Catatan berhasil diperbarui"
}
```

**Response Gagal (404):**

```json
{
  "status": "fail",
  "message": "Gagal memperbarui catatan. Id tidak ditemukan"
}
```

**Contoh dengan curl:**

```bash
curl -X PUT http://localhost:5000/notes/ID-catatan-anda \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Catatan Diperbarui",
    "tags": ["penting", "diperbarui"],
    "body": "Konten yang sudah diperbarui"
  }'
```

### 5. Menghapus Catatan

**Endpoint:** `DELETE /notes/{id}`

**Response Sukses (200):**

```json
{
  "status": "success",
  "message": "Catatan berhasil dihapus"
}
```

**Response Gagal (404):**

```json
{
  "status": "fail",
  "message": "Catatan gagal dihapus. Id tidak ditemukan"
}
```

**Contoh dengan curl:**

```bash
curl -X DELETE http://localhost:5000/notes/ID-catatan-anda
```

## Pengujian API

### Pengujian dengan Postman

Proyek ini menyediakan koleksi Postman untuk memudahkan pengujian API. Koleksi dan environment Postman tersedia di folder `postman_test/`. Untuk menggunakan koleksi ini:

1. Pastikan Postman sudah terinstal di komputer Anda
2. Import koleksi dan environment:
   - Buka Postman
   - Klik tombol "Import" di pojok kiri atas
   - Pilih file `notes-api-test.postman_collection.json` dan `notes-api-test.postman_environment.json` dari folder `postman_test/`
3. Pilih environment "Notes API Test" dari dropdown environment di pojok kanan atas
4. Kini Anda dapat menjalankan setiap request yang tersedia di koleksi untuk menguji API

Koleksi Postman ini mencakup pengujian untuk semua endpoint API yang tersedia:

- Membuat catatan baru
- Mengambil semua catatan
- Mengambil catatan berdasarkan ID
- Memperbarui catatan
- Menghapus catatan

### Pengujian Otomatis dengan Newman

Newman adalah command-line collection runner untuk Postman. Anda dapat menggunakan Newman untuk menjalankan pengujian API secara otomatis dari terminal.

1. Instal Newman secara global:

   ```bash
   npm install -g newman
   ```

2. Jalankan pengujian menggunakan koleksi dan environment yang tersedia:

   ```bash
   newman run ./postman_test/notes-api-test.postman_collection.json -e ./postman_test/notes-api-test.postman_environment.json
   ```

3. Newman akan menjalankan semua request dalam koleksi dan menampilkan hasil pengujian di terminal

## Dependensi

- **@hapi/hapi** (v21.4.0) - Framework web server untuk Node.js
- **nanoid** (v3.3.11) - Generator ID unik yang ringan

## Dependensi Pengembangan

- **nodemon** (v3.1.10) - Untuk restart server otomatis saat pengembangan
- **eslint** (v9.26.0) - Untuk pemeriksaan kualitas kode
- **eslint-config-dicodingacademy** (v0.9.4) - Konfigurasi ESLint dari Dicoding Academy
- **@eslint/js** (v9.26.0) - Konfigurasi ESLint berbasis JavaScript
- **globals** (v16.0.0) - Definisi variabel global untuk ESLint

## Script NPM

- **start**: `nodemon ./src/server.js` - Menjalankan server dengan fitur hot reload
- **lint**: `eslint ./src` - Memeriksa kualitas kode
- **lint:fix**: `eslint ./src --fix` - Memperbaiki masalah kode secara otomatis
- **test**: `echo "Error: no test specified" && exit 1` - Placeholder untuk testing

## CORS

Aplikasi ini mengaktifkan CORS (Cross-Origin Resource Sharing) untuk semua origin, sehingga API dapat diakses oleh aplikasi frontend dari domain manapun.

## Catatan Pengembangan

- Aplikasi ini masih menggunakan penyimpanan data di memori (array), sehingga data akan hilang jika server di-restart
- Untuk pengembangan lebih lanjut, pertimbangkan untuk menggunakan database seperti PostgreSQL, MongoDB, atau MySQL
