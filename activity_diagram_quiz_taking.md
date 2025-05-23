# Activity Diagram - Pengerjaan Kuis oleh Siswa

Diagram aktivitas berikut menggambarkan proses siswa bergabung dengan kuis, mengerjakan soal, dan menerima nilai dalam sistem ExamExpert-AI.

```
+-------------+          +-------------------+          +-------------------+
|             |          |                   |          |                   |
|    Siswa    |          |       Sistem      |          |   Database        |
|             |          |                   |          |                   |
+-------------+          +-------------------+          +-------------------+
       |                           |                            |
       | Login ke Sistem           |                            |
       |-------------------------->|                            |
       |                           |                            |
       | Akses Menu Gabung Kuis    |                            |
       |-------------------------->|                            |
       |                           |                            |
       |    Tampilkan Form         |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Masukkan Kode Akses Kuis  |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Validasi Kode Akses        |
       |                           |--------------------------->|
       |                           |                            |
       |                           |       Hasil Validasi       |
       |                           |<---------------------------|
       |                           |                            |
       |                           | Jika Kode Tidak Valid      |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |   Tampilkan Pesan Error   |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Kode Valid            |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Periksa Status Kuis        |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Status Kuis            |
       |                           |<---------------------------|
       |                           |                            |
       |                           | Jika Kuis Belum Aktif      |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       | Tampilkan Pesan Tunggu    |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Kuis Aktif            |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Ambil Data Kuis & Soal     |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Data Kuis & Soal        |
       |                           |<---------------------------|
       |                           |                            |
       |   Tampilkan Halaman Kuis  |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Mulai Mengerjakan Kuis    |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Mulai Timer Kuis           |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |   Tampilkan Soal Kuis     |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Menjawab Soal             |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Simpan Jawaban Sementara   |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       | Navigasi Antar Soal       |                            |
       |-------------------------->|                            |
       |                           |                            |
       |  Tampilkan Soal Dipilih   |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Kirim Jawaban (Submit)    |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Hentikan Timer             |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Proses Penilaian Otomatis  |
       |                           |   (untuk soal objektif)    |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Simpan Hasil Kuis          |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Simpan       |
       |                           |<---------------------------|
       |                           |                            |
       |   Tampilkan Hasil Kuis    |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Lihat Detail Hasil        |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Detail Hasil         |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Data Detail Hasil       |
       |                           |<---------------------------|
       |                           |                            |
       | Tampilkan Detail Jawaban  |                            |
       | dan Penjelasan            |                            |
       |<--------------------------|                            |
       |                           |                            |
       v                           v                            v
```

## Penjelasan Alur Aktivitas

### 1. Gabung dengan Kuis
1. **Siswa** login ke sistem dan mengakses menu gabung kuis.
2. **Siswa** memasukkan kode akses kuis yang diberikan oleh guru.
3. **Sistem** memvalidasi kode akses kuis.
4. Jika kode tidak valid, sistem menampilkan pesan error.
5. Jika kode valid, sistem memeriksa status kuis (aktif/tidak aktif).
6. Jika kuis belum aktif, sistem memberi tahu siswa untuk menunggu.

### 2. Persiapan Kuis
1. Jika kuis aktif, **Sistem** mengambil data kuis dan soal-soal dari database.
2. **Sistem** menampilkan halaman kuis dengan informasi durasi dan jumlah soal.
3. **Siswa** memulai kuis, dan **Sistem** memulai timer kuis.

### 3. Mengerjakan Kuis
1. **Sistem** menampilkan soal-soal kuis.
2. **Siswa** menjawab soal-soal.
3. **Sistem** menyimpan jawaban sementara.
4. **Siswa** dapat bernavigasi antar soal.
5. **Sistem** menampilkan soal yang dipilih siswa.

### 4. Penyelesaian dan Penilaian
1. **Siswa** mengirimkan semua jawaban (submit).
2. **Sistem** menghentikan timer.
3. **Sistem** melakukan penilaian otomatis untuk soal objektif.
4. **Sistem** menyimpan hasil kuis di database.

### 5. Lihat Hasil
1. **Sistem** menampilkan hasil kuis kepada siswa (nilai total).
2. **Siswa** dapat melihat detail hasil.
3. **Sistem** mengambil detail hasil dari database.
4. **Sistem** menampilkan detail jawaban dan penjelasan untuk setiap soal.
