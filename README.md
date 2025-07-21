
# Belajar MongoDB Dasar

Repository ini adalah catatan dan panduan praktis untuk belajar dasar-dasar MongoDB, khususnya bagi yang sudah familiar dengan konsep database relasional seperti MySQL.

## Daftar Isi
- Pengantar MongoDB
- Persiapan: Instalasi MongoDB
  - MongoDB Community Server
  - MongoDB Shell (mongosh)
- Memulai dengan mongosh
- Operasi CRUD Dasar
  - C: Create (Menambahkan Data)
  - R: Read (Melihat Data)
  - U: Update (Memperbarui Data)
  - D: Delete (Menghapus Data)
- Penting: Indeks Unik (Unique Index)
- Konsep Penting Lainnya

## Pengantar MongoDB
MongoDB adalah database NoSQL berorientasi dokumen (document-oriented). Berbeda dengan database relasional (MySQL) yang menggunakan tabel dan skema kaku, MongoDB menyimpan data dalam bentuk dokumen JSON (lebih tepatnya BSON) yang fleksibel.

**Perbandingan Sederhana:**  
- MySQL: Tabel, Baris (Records), Kolom  
- MongoDB: Koleksi (Collections), Dokumen (Documents), Field

**Contoh Dokumen MongoDB:**

```json
{
  "_id": ObjectId("60d5ec49f8c6d1f3e0b2d3e4"),
  "nama": "Budi Santoso",
  "email": "budi.s@example.com",
  "umur": 30,
  "hobi": ["membaca", "bersepeda"],
  "alamat": {
    "jalan": "Jl. Merdeka No. 10",
    "kota": "Surabaya"
  }
}
```

## Persiapan: Instalasi MongoDB
### MongoDB Community Server
- Unduh dari situs resmi MongoDB dan jalankan file `.msi`.
- Pilih instalasi **Complete** dan pastikan MongoDB Compass ikut dicentang.
- Ikuti proses instalasi sampai selesai.

### MongoDB Shell (mongosh)
- Unduh mongosh (.zip), ekstrak, dan salin isinya ke folder `bin` MongoDB Server.
- Tambahkan path ke variabel lingkungan `Path`.

## Memulai dengan mongosh
- Jalankan CMD baru dan ketik `mongosh`. Jika gagal, silahkan buat baru di new environments windows
- Gunakan database:  
  ```js
  use perpustakaanDigital
  ```

## Operasi CRUD Dasar

### C: Create (Menambahkan Data)
```js
// Menambahkan satu dokumen
db.buku.insertOne({
  judul: "Laskar Pelangi",
  penulis: "Andrea Hirata",
  tahunTerbit: 2005,
  genre: ["Fiksi", "Edukasi"],
  stok: 10,
  tersedia: true
})

// Menambahkan beberapa dokumen
db.buku.insertMany([
  {
    judul: "Filosofi Teras",
    penulis: "Henry Manampiring",
    tahunTerbit: 2018,
    genre: ["Filosofi", "Self-Improvement"],
    stok: 5,
    tersedia: true
  },
  {
    judul: "Bumi Manusia",
    penulis: "Pramoedya Ananta Toer",
    tahunTerbit: 1980,
    genre: ["Fiksi", "Sejarah"],
    stok: 7,
    tersedia: true
  }
])
```

### R: Read (Melihat Data)
```js
// Melihat semua dokumen di koleksi 'buku'
db.buku.find()

// Mencari dokumen dengan kriteria (filter)
db.buku.find({ penulis: "Andrea Hirata" }) // Penulis Andrea Hirata
db.buku.find({ tahunTerbit: { $lt: 2000 } }) // Tahun terbit kurang dari 2000 ($lt = less than)
db.buku.find({ stok: { $gt: 8 } }) // Stok lebih dari 8 ($gt = greater than)
db.buku.find({ genre: "Filosofi" }) // Buku yang memiliki genre "Filosofi" (bisa di dalam array)

// Mencari satu dokumen pertama yang cocok
db.buku.findOne({ judul: "Filosofi Teras" })
```

### U: Update (Memperbarui Data)
```js
// Mengubah satu dokumen: ubah tahunTerbit dan tambahkan rating
db.buku.updateOne(
  { judul: "Laskar Pelangi" },
  { $set: { tahunTerbit: 2006, rating: 4.9 } }
)

// Mengubah satu dokumen: kurangi stok
db.buku.updateOne(
  { judul: "Bumi Manusia" },
  { $inc: { stok: -1 } }
)

// Mengubah banyak dokumen: semua buku dengan stok <= 5 menjadi tidak tersedia
db.buku.updateMany(
  { stok: { $lte: 5 } }, // $lte = less than or equal to
  { $set: { tersedia: false } }
)
```

### D: Delete (Menghapus Data)
```js
// Menghapus satu dokumen
db.buku.deleteOne({ judul: "The Alchemist" })

// Menghapus banyak dokumen (misal: yang tidak tersedia dan stok 0)
db.buku.deleteMany({ tersedia: false, stok: 0 })

// HATI-HATI! Menghapus SEMUA dokumen di koleksi. Jika ingin melakukan deleteMany(), lebih baik lakukan seperti di atas
db.buku.deleteMany({})
```

## Penting: Indeks Unik (Unique Index)
```js
// Membuat indeks unik pada field 'email' di koleksi 'anggota'
// Pastikan email tidak ada yang sama
db.anggota.createIndex(
  { "email": 1 }, // 1 untuk ascending, -1 untuk descending (wajib ditulis)
  { unique: true } // Kunci utama untuk indeks unik
)

// Membuat indeks unik gabungan (kombinasi judul dan penulis harus unik)
db.buku.createIndex(
   { "judul": 1, "penulis": 1 },
   { unique: true }
)
```

Semoga README ini membantu kamu belajar dan mengulang MongoDB dengan lebih mudah! Selamat belajar!
