# Activity Diagram - Autentikasi Pengguna

Diagram aktivitas berikut menggambarkan proses autentikasi pengguna dalam sistem ExamExpert-AI, termasuk registrasi, login, dan verifikasi token.

```
+-------------+          +-------------------+          +-------------------+
|             |          |                   |          |                   |
|  Pengguna   |          |       Sistem      |          |   Database        |
|             |          |                   |          |                   |
+-------------+          +-------------------+          +-------------------+
       |                           |                            |
       | Akses Sistem              |                            |
       |-------------------------->|                            |
       |                           |                            |
       |  Tampilkan Opsi Login     |                            |
       |  atau Registrasi          |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Registrasi/Login    |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Jika Pilih Registrasi      |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Form Registrasi|                            |
       |<--------------------------|                            |
       |                           |                            |
       | Isi Form Registrasi       |                            |
       | (Nama, Email, Password,   |                            |
       |  Role)                    |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Validasi Data Registrasi   |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Jika Data Tidak Valid      |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Pesan Error    |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Data Valid            |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Cek Email Sudah Terdaftar  |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Hasil Pengecekan        |
       |                           |<---------------------------|
       |                           |                            |
       |                           | Jika Email Sudah Terdaftar |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Pesan Error    |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Email Belum Terdaftar |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Hash Password              |
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
       |                           | Generate JWT Token         |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Pesan Sukses   |                            |
       |  dan Token                |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Pilih Login           |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Form Login     |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Isi Kredensial Login      |                            |
       | (Email, Password)         |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Validasi Input             |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Cari User dengan Email     |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Data User               |
       |                           |<---------------------------|
       |                           |                            |
       |                           | Jika User Tidak Ditemukan  |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Pesan Error    |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika User Ditemukan        |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Verifikasi Password        |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Jika Password Salah        |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Pesan Error    |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Password Benar        |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Generate JWT Token         |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Sukses dan     |                            |
       |  Berikan Token            |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Simpan Token di Client    |                            |
       |------------+              |                            |
       |            |              |                            |
       |<-----------+              |                            |
       |                           |                            |
       | Akses Halaman Terproteksi |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Periksa Token JWT          |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Jika Token Tidak Valid     |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Error 401      |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Token Valid           |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Ekstrak Data User          |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Periksa Role dan Izin      |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Jika Tidak Memiliki Izin   |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Error 403      |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Memiliki Izin         |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Berikan Akses ke         |                            |
       |  Halaman                  |                            |
       |<--------------------------|                            |
       |                           |                            |
       v                           v                            v
```

## Penjelasan Alur Aktivitas

### 1. Akses Awal dan Pilihan
1. **Pengguna** mengakses sistem ExamExpert-AI.
2. **Sistem** menampilkan opsi untuk login atau registrasi.
3. **Pengguna** memilih untuk registrasi atau login.

### 2. Alur Registrasi
1. Jika **Pengguna** memilih registrasi, **Sistem** menampilkan formulir registrasi.
2. **Pengguna** mengisi formulir dengan informasi yang diperlukan (nama, email, password, role).
3. **Sistem** memvalidasi data yang dimasukkan.
4. **Sistem** memeriksa apakah email sudah terdaftar di database.
5. Jika email sudah terdaftar atau data tidak valid, **Sistem** menampilkan pesan error.
6. Jika email belum terdaftar dan data valid:
   - **Sistem** mengenkripsi (hash) password.
   - **Sistem** menyimpan informasi pengguna baru di database.
   - **Sistem** membuat JWT token.
   - **Sistem** menampilkan pesan sukses dan token kepada pengguna.

### 3. Alur Login
1. Jika **Pengguna** memilih login, **Sistem** menampilkan formulir login.
2. **Pengguna** memasukkan kredensial (email dan password).
3. **Sistem** memvalidasi input.
4. **Sistem** mencari pengguna dengan email yang dimasukkan.
5. Jika pengguna tidak ditemukan, **Sistem** menampilkan pesan error.
6. Jika pengguna ditemukan, **Sistem** memverifikasi password.
7. Jika password salah, **Sistem** menampilkan pesan error.
8. Jika password benar:
   - **Sistem** membuat JWT token.
   - **Sistem** menampilkan pesan sukses dan memberikan token.
   - **Pengguna** menyimpan token di client side.

### 4. Akses ke Halaman Terproteksi
1. **Pengguna** mencoba mengakses halaman terproteksi dengan token.
2. **Sistem** memeriksa validitas token JWT.
3. Jika token tidak valid, **Sistem** menampilkan error 401 (Unauthorized).
4. Jika token valid, **Sistem** mengekstrak data pengguna dari token.
5. **Sistem** memeriksa role pengguna dan izin untuk halaman yang diminta.
6. Jika pengguna tidak memiliki izin, **Sistem** menampilkan error 403 (Forbidden).
7. Jika pengguna memiliki izin, **Sistem** memberikan akses ke halaman yang diminta.
