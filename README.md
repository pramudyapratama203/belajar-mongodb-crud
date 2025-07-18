
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
- Jalankan CMD baru dan ketik `mongosh`.
- Gunakan database:  
  ```js
  use perpustakaanDigital
  ```

## Operasi CRUD Dasar

### C: Create (Menambahkan Data)
```js
db.buku.insertOne({
  judul: "Laskar Pelangi",
  penulis: "Andrea Hirata",
  tahunTerbit: 2005,
  genre: ["Fiksi", "Edukasi", "Petualangan"],
  stok: 10,
  tersedia: true
})
```

### R: Read (Melihat Data)
```js
db.buku.find()
db.buku.find({ penulis: "Andrea Hirata" })
```

### U: Update (Memperbarui Data)
```js
db.buku.updateOne(
  { judul: "Laskar Pelangi" },
  { $set: { tahunTerbit: 2006, rating: 4.9 } }
)
```

### D: Delete (Menghapus Data)
```js
db.buku.deleteOne({ judul: "Bumi Manusia" })
```

## Penting: Indeks Unik (Unique Index)
```js
db.anggota.createIndex( { email: 1 }, { unique: true } )
```

## Konsep Penting Lainnya
- Flexible Schema
- Embedded Documents & Arrays
- Tidak ada trigger bawaan (gunakan Change Streams)

---
Semoga README ini membantu kamu belajar dan mengulang MongoDB dengan lebih mudah! Selamat belajar!
