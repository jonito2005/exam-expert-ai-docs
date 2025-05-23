# Activity Diagram - Kelola User oleh Admin

Diagram aktivitas berikut menggambarkan proses pengelolaan pengguna oleh admin dalam sistem ExamExpert-AI.

```
+-------------+          +-------------------+          +-------------------+
|             |          |                   |          |                   |
|    Admin    |          |       Sistem      |          |   Database        |
|             |          |                   |          |                   |
+-------------+          +-------------------+          +-------------------+
       |                           |                            |
       | Login sebagai Admin       |                            |
       |-------------------------->|                            |
       |                           |                            |
       | Akses Menu Kelola User    |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Daftar Pengguna      |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Data Pengguna          |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Daftar Pengguna|                            |
       |  dengan Filter & Sorting  |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Aksi (Tambah/Edit/  |                            |
       | Hapus/Lihat Detail)       |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Jika Aksi = Tambah User    |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |    Tampilkan Form Tambah  |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Isi Data User Baru        |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Validasi Data              |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Jika Data Valid            |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Simpan User Baru           |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Simpan       |
       |                           |<---------------------------|
       |                           |                            |
       |    Tampilkan Konfirmasi   |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Aksi = Edit User      |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Ambil Data User            |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Data User              |
       |                           |<---------------------------|
       |                           |                            |
       |    Tampilkan Form Edit    |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Edit Data User            |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Validasi Data              |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Update User                |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Update       |
       |                           |<---------------------------|
       |                           |                            |
       |    Tampilkan Konfirmasi   |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Aksi = Hapus User     |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |    Tampilkan Konfirmasi   |                            |
       |    Hapus                  |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Konfirmasi Hapus          |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Hapus User                 |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Hapus        |
       |                           |<---------------------------|
       |                           |                            |
       |    Tampilkan Notifikasi   |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Aksi = Lihat Detail   |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Ambil Detail User          |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Data Detail User        |
       |                           |<---------------------------|
       |                           |                            |
       |    Tampilkan Detail User  |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Kembali ke Daftar User    |                            |
       |-------------------------->|                            |
       |                           |                            |
       v                           v                            v
```

## Penjelasan Alur Aktivitas

### 1. Akses Menu Pengelolaan User
1. **Admin** login ke sistem dengan kredensial admin.
2. **Admin** mengakses menu kelola user.
3. **Sistem** mengambil daftar pengguna dari database.
4. **Sistem** menampilkan daftar pengguna dengan opsi filter dan sorting.

### 2. Tambah User Baru
1. **Admin** memilih aksi tambah user.
2. **Sistem** menampilkan formulir tambah user.
3. **Admin** mengisi data user baru (nama, email, password, role, dll).
4. **Sistem** memvalidasi data yang dimasukkan.
5. Jika data valid, **Sistem** menyimpan user baru ke database.
6. **Sistem** menampilkan konfirmasi keberhasilan.

### 3. Edit User
1. **Admin** memilih user tertentu dan aksi edit.
2. **Sistem** mengambil data user dari database.
3. **Sistem** menampilkan formulir edit dengan data user yang sudah ada.
4. **Admin** mengubah data yang diperlukan.
5. **Sistem** memvalidasi perubahan.
6. **Sistem** memperbarui data user di database.
7. **Sistem** menampilkan konfirmasi keberhasilan.

### 4. Hapus User
1. **Admin** memilih user tertentu dan aksi hapus.
2. **Sistem** menampilkan konfirmasi hapus.
3. **Admin** mengkonfirmasi penghapusan.
4. **Sistem** menghapus user dari database.
5. **Sistem** menampilkan notifikasi keberhasilan.

### 5. Lihat Detail User
1. **Admin** memilih user tertentu dan aksi lihat detail.
2. **Sistem** mengambil detail lengkap user dari database.
3. **Sistem** menampilkan halaman detail user, termasuk:
   - Informasi profil
   - Aktivitas user (kuis yang dibuat/diikuti)
   - Status akun
   - Log aktivitas
4. **Admin** dapat kembali ke daftar user setelah melihat detail.
