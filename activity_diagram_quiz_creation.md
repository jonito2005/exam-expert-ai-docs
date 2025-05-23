# Activity Diagram - Pembuatan Kuis oleh Guru

Diagram aktivitas berikut menggambarkan proses pembuatan kuis oleh guru dalam sistem ExamExpert-AI.

```
+-------------+          +-------------------+          +-------------------+
|             |          |                   |          |                   |
|    Guru     |          |       Sistem      |          |   Database        |
|             |          |                   |          |                   |
+-------------+          +-------------------+          +-------------------+
       |                           |                            |
       | Login ke Sistem           |                            |
       |-------------------------->|                            |
       |                           |                            |
       | Akses Menu Buat Kuis      |                            |
       |-------------------------->|                            |
       |                           |                            |
       |    Tampilkan Form         |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Isi Informasi Kuis        |                            |
       | (Judul, Deskripsi, Topik) |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Validasi Input Dasar       |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Jika Input Tidak Valid     |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |   Tampilkan Pesan Error   |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Input Valid           |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Ambil Soal yang Disetujui  |
       |                           |--------------------------->|
       |                           |                            |
       |                           |   Daftar Soal Disetujui    |
       |                           |<---------------------------|
       |                           |                            |
       |   Tampilkan Daftar Soal   |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Soal untuk Kuis     |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Tambahkan Soal ke Kuis     |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       | Atur Pengaturan Kuis      |                            |
       | (Durasi, Tanggal, Status) |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Validasi Pengaturan        |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       | Simpan Kuis               |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Buat Kode Akses Unik       |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Simpan Kuis ke Database    |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Simpan       |
       |                           |<---------------------------|
       |                           |                            |
       |   Tampilkan Detail Kuis   |                            |
       |   dengan Kode Akses       |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Salin Kode Akses          |                            |
       |------------+              |                            |
       |            |              |                            |
       |<-----------+              |                            |
       |                           |                            |
       | Bagikan Kode Akses        |                            |
       | kepada Siswa              |                            |
       |------------+              |                            |
       |            |              |                            |
       |<-----------+              |                            |
       |                           |                            |
       | Lihat Status Kuis         |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Status Kuis          |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Data Status Kuis       |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Status Kuis    |                            |
       |<--------------------------|                            |
       |                           |                            |
       v                           v                            v
```

## Penjelasan Alur Aktivitas

### 1. Persiapan Pembuatan Kuis
1. **Guru** login ke sistem dan mengakses menu pembuatan kuis.
2. **Sistem** menampilkan formulir pembuatan kuis.
3. **Guru** mengisi informasi dasar kuis:
   - Judul kuis
   - Deskripsi kuis
   - Topik atau mata pelajaran
4. **Sistem** memvalidasi input dasar.
5. Jika input tidak valid, **Sistem** menampilkan pesan error.

### 2. Pemilihan Soal
1. Jika input valid, **Sistem** mengambil daftar soal yang telah disetujui dari database.
2. **Sistem** menampilkan daftar soal yang tersedia kepada guru.
3. **Guru** memilih soal-soal yang akan dimasukkan ke dalam kuis.
4. **Sistem** menambahkan soal-soal yang dipilih ke dalam kuis.

### 3. Konfigurasi Kuis
1. **Guru** mengatur pengaturan kuis:
   - Durasi kuis (dalam menit)
   - Tanggal mulai dan selesai (opsional)
   - Status kuis (aktif/tidak aktif)
2. **Sistem** memvalidasi pengaturan kuis.

### 4. Finalisasi dan Distribusi
1. **Guru** menyimpan kuis.
2. **Sistem** membuat kode akses unik untuk kuis.
3. **Sistem** menyimpan kuis ke database.
4. **Sistem** menampilkan detail kuis dengan kode akses kepada guru.
5. **Guru** menyalin kode akses.
6. **Guru** membagikan kode akses kepada siswa melalui metode yang diinginkan (di luar sistem).

### 5. Monitoring Kuis
1. **Guru** dapat melihat status kuis.
2. **Sistem** mengambil data status kuis dari database.
3. **Sistem** menampilkan status kuis, termasuk jumlah siswa yang bergabung dan mengerjakan.
