# Activity Diagram - Kelola Profil Pengguna

Diagram aktivitas berikut menggambarkan proses pengelolaan profil oleh semua jenis pengguna (Admin, Guru, dan Siswa) dalam sistem ExamExpert-AI.

```
+-------------+          +-------------------+          +-------------------+
|             |          |                   |          |                   |
|   Pengguna  |          |       Sistem      |          |   Database        |
|             |          |                   |          |                   |
+-------------+          +-------------------+          +-------------------+
       |                           |                            |
       | Login ke Sistem           |                            |
       |-------------------------->|                            |
       |                           |                            |
       | Pilih Menu Profil         |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Data Profil          |
       |                           | Pengguna                   |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Data Profil            |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Halaman Profil |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Aksi                |                            |
       | (Edit Profil/Ubah Password|                            |
       | /Kelola Preferensi)       |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Jika Aksi = Edit Profil    |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Form Edit      |                            |
       |  Profil                   |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Edit Data Profil          |                            |
       | (Nama, Email, dll)        |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Validasi Data              |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Update Profil              |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Update       |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Konfirmasi     |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Aksi = Ubah Password  |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Form Ubah      |                            |
       |  Password                 |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Masukkan Password Lama    |                            |
       | dan Password Baru         |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Verifikasi Password Lama   |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Hasil Verifikasi        |
       |                           |<---------------------------|
       |                           |                            |
       |                           | Validasi Password Baru     |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Jika Password Valid        |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Update Password            |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Update       |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Konfirmasi     |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Aksi = Kelola         |
       |                           | Preferensi                 |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Ambil Preferensi Pengguna  |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Data Preferensi         |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Form Preferensi|                            |
       |<--------------------------|                            |
       |                           |                            |
       | Ubah Preferensi           |                            |
       | (Notifikasi/Tema/Bahasa)  |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Update Preferensi          |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Update       |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Konfirmasi     |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Upload Foto Profil  |                            |
       | (opsional)                |                            |
       |-------------------------->|                            |
       |                           |                            |
       |  Tampilkan Form Upload    |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Upload Foto               |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Validasi File              |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Simpan Foto Profil         |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Simpan       |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Profil         |                            |
       |  dengan Foto Baru         |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Hapus Akun          |                            |
       | (opsional)                |                            |
       |-------------------------->|                            |
       |                           |                            |
       |  Tampilkan Konfirmasi     |                            |
       |  Hapus Akun               |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Konfirmasi dengan Password|                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Verifikasi Password        |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Hasil Verifikasi        |
       |                           |<---------------------------|
       |                           |                            |
       |                           | Jika Password Benar        |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Hapus/Nonaktifkan Akun     |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Proses       |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Notifikasi     |                            |
       |  & Logout                 |                            |
       |<--------------------------|                            |
       |                           |                            |
       v                           v                            v
```

## Penjelasan Alur Aktivitas

### 1. Akses Profil
1. **Pengguna** (Admin, Guru, atau Siswa) login ke sistem.
2. **Pengguna** memilih menu profil.
3. **Sistem** mengambil data profil pengguna dari database.
4. **Sistem** menampilkan halaman profil dengan informasi lengkap.

### 2. Edit Profil
1. **Pengguna** memilih aksi edit profil.
2. **Sistem** menampilkan formulir edit profil dengan data yang sudah ada.
3. **Pengguna** mengubah data profil (nama, email, informasi kontak, dll).
4. **Sistem** memvalidasi data yang dimasukkan.
5. **Sistem** memperbarui data profil di database.
6. **Sistem** menampilkan konfirmasi keberhasilan.

### 3. Ubah Password
1. **Pengguna** memilih aksi ubah password.
2. **Sistem** menampilkan formulir ubah password.
3. **Pengguna** memasukkan password lama dan password baru.
4. **Sistem** memverifikasi password lama dengan database.
5. **Sistem** memvalidasi password baru (kekuatan, format, dll).
6. Jika valid, **Sistem** memperbarui password di database.
7. **Sistem** menampilkan konfirmasi keberhasilan.

### 4. Kelola Preferensi
1. **Pengguna** memilih aksi kelola preferensi.
2. **Sistem** mengambil preferensi pengguna dari database.
3. **Sistem** menampilkan formulir preferensi.
4. **Pengguna** mengubah preferensi seperti:
   - Pengaturan notifikasi
   - Tema tampilan
   - Bahasa
   - Preferensi privasi
5. **Sistem** memperbarui preferensi di database.
6. **Sistem** menampilkan konfirmasi keberhasilan.

### 5. Upload Foto Profil
1. **Pengguna** memilih untuk upload foto profil.
2. **Sistem** menampilkan formulir upload.
3. **Pengguna** mengupload foto.
4. **Sistem** memvalidasi file (format, ukuran, dll).
5. **Sistem** menyimpan foto profil di database.
6. **Sistem** menampilkan profil dengan foto baru.

### 6. Hapus Akun (Opsional)
1. **Pengguna** memilih opsi hapus akun.
2. **Sistem** menampilkan konfirmasi dengan peringatan.
3. **Pengguna** mengkonfirmasi dengan memasukkan password.
4. **Sistem** memverifikasi password.
5. Jika password benar, **Sistem** menghapus atau menonaktifkan akun di database.
6. **Sistem** menampilkan notifikasi dan mengarahkan pengguna ke halaman logout.
