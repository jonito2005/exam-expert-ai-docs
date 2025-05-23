# Activity Diagram - Pendaftaran Guru dengan Persetujuan Admin

Diagram aktivitas berikut menggambarkan proses pendaftaran pengguna sebagai guru yang memerlukan bukti kualifikasi dan persetujuan dari admin dalam sistem ExamExpert-AI.

```
+-------------+          +-------------------+          +----------------+          +------------------+
|             |          |                   |          |                |          |                  |
|  Pengguna   |          |      Sistem       |          |     Admin      |          |  Email Service   |
|             |          |                   |          |                |          |                  |
+-------------+          +-------------------+          +----------------+          +------------------+
       |                           |                            |                           |
       | Akses Halaman Pendaftaran |                            |                           |
       |-------------------------->|                            |                           |
       |                           |                            |                           |
       | Pilih Daftar sebagai Guru |                            |                           |
       |-------------------------->|                            |                           |
       |                           |                            |                           |
       |     Tampilkan Form        |                            |                           |
       |<--------------------------|                            |                           |
       |                           |                            |                           |
       | Isi Data & Upload Dokumen |                            |                           |
       |-------------------------->|                            |                           |
       |                           |                            |                           |
       |                           | Validasi Data              |                           |
       |                           |------------+               |                           |
       |                           |            |               |                           |
       |                           |<-----------+               |                           |
       |                           |                            |                           |
       |                           | Jika Data Valid            |                           |
       |                           |------------+               |                           |
       |                           |            |               |                           |
       |                           |<-----------+               |                           |
       |                           |                            |                           |
       |                           | Buat User (status=pending) |                           |
       |                           |------------+               |                           |
       |                           |            |               |                           |
       |                           |<-----------+               |                           |
       |                           |                            |                           |
       |                           | Simpan Dokumen Kualifikasi |                           |
       |                           |------------+               |                           |
       |                           |            |               |                           |
       |                           |<-----------+               |                           |
       |                           |                            |                           |
       |                           | Kirim Notifikasi ke Admin  |                           |
       |                           |-------------------------------------------+            |
       |                           |                            |              |            |
       |                           |                            |              v            |
       |                           |                            |      Kirim Email Notifikasi
       |                           |                            |              |            |
       |                           |                            |              v            |
       |                           |                            |<-------------+            |
       |                           |                            |                           |
       | Tampilkan Pesan Konfirmasi|                            |                           |
       |<--------------------------|                            |                           |
       |                           |                            |                           |
       |                           |                            | Login ke Dashboard Admin  |
       |                           |                            |-------------------------->|
       |                           |                            |                           |
       |                           |                            | Lihat Daftar Pendaftaran  |
       |                           |                            |-------------------------->|
       |                           |                            |                           |
       |                           |                            | Buka Detail Pendaftaran   |
       |                           |                            |-------------------------->|
       |                           |                            |                           |
       |                           |                            | Periksa Dokumen Kualifikasi
       |                           |                            |-------------------------->|
       |                           |                            |                           |
       |                           |                            | Setujui/Tolak Pendaftaran |
       |                           |                            |-------------------------->|
       |                           |                            |                           |
       |                           |                            | Jika Ditolak              |
       |                           |                            |-------------+             |
       |                           |                            |             |             |
       |                           |                            |<------------+             |
       |                           |                            |                           |
       |                           |                            | Berikan Alasan Penolakan  |
       |                           |                            |-------------------------->|
       |                           |                            |                           |
       |                           | Update Status User         |                           |
       |                           |<--------------------------------------------------------|
       |                           |                            |                           |
       |                           | Kirim Notifikasi ke Pengguna                           |
       |                           |-------------------------------------------------------------->|
       |                           |                            |                           |
       |                           |                            |                           | Kirim Email Hasil
       |                           |                            |                           |-------------+
       |                           |                            |                           |             |
       |                           |                            |                           |<------------+
       |                           |                            |                           |
       | Cek Email untuk Hasil     |                            |                           |
       |<----------------------------------------------------------------------|
       |                           |                            |                           |
       |                           |                            |                           |
       v                           v                            v                           v
```

## Penjelasan Alur Aktivitas

### 1. Pendaftaran Awal
1. **Pengguna** mengakses halaman pendaftaran dan memilih untuk mendaftar sebagai guru.
2. **Sistem** menampilkan formulir pendaftaran khusus guru.
3. **Pengguna** mengisi informasi personal, profesional, dan mengunggah dokumen kualifikasi.
4. **Sistem** memvalidasi data yang dimasukkan.

### 2. Pemrosesan Pendaftaran
1. **Sistem** membuat akun pengguna dengan status "pending".
2. **Sistem** menyimpan dokumen kualifikasi yang diunggah.
3. **Sistem** mengirim notifikasi ke admin tentang pendaftaran guru baru.
4. **Sistem** menampilkan pesan konfirmasi kepada pengguna.

### 3. Review oleh Admin
1. **Admin** login ke dashboard admin.
2. **Admin** melihat daftar pendaftaran guru yang menunggu persetujuan.
3. **Admin** membuka detail pendaftaran untuk ditinjau.
4. **Admin** memeriksa dokumen kualifikasi dan informasi profesional.
5. **Admin** memutuskan untuk menyetujui atau menolak pendaftaran.

### 4. Pemrosesan Keputusan
1. Jika pendaftaran **ditolak**, admin memberikan alasan penolakan.
2. **Sistem** memperbarui status pengguna menjadi "active" atau "rejected".
3. **Sistem** mengirim notifikasi email kepada pengguna tentang hasil pendaftaran.
4. **Pengguna** memeriksa email untuk mengetahui hasil pendaftaran.

### 5. Setelah Persetujuan
1. Jika disetujui, pengguna dapat login dengan hak akses guru.
2. Jika ditolak, pengguna dapat mendaftar ulang dengan perbaikan sesuai alasan penolakan.
