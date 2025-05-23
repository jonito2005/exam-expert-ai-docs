# Activity Diagram - Lihat Statistik Sistem oleh Admin

Diagram aktivitas berikut menggambarkan proses admin melihat statistik penggunaan sistem ExamExpert-AI.

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
       | Akses Dashboard Admin     |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Data Statistik Umum  |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Data Statistik Umum     |
       |                           |<---------------------------|
       |                           |                            |
       |                           | Proses Perhitungan Statistik
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Dashboard      |                            |
       |  dengan Statistik Umum    |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Kategori Statistik  |                            |
       | (Pengguna/Soal/Kuis)      |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Jika Pilih Statistik       |
       |                           | Pengguna                   |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Ambil Data Pengguna        |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Data Statistik Pengguna |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Statistik      |                            |
       |  Pengguna                 |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Pilih Statistik       |
       |                           | Soal                       |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Ambil Data Soal            |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Data Statistik Soal     |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Statistik      |                            |
       |  Soal                     |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Pilih Statistik       |
       |                           | Kuis                       |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Ambil Data Kuis            |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Data Statistik Kuis     |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Statistik      |                            |
       |  Kuis                     |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Filter Waktu        |                            |
       | (Hari/Minggu/Bulan/Tahun) |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Data dengan Filter   |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Data Terfilter          |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Data Terfilter |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Opsi Ekspor         |                            |
       | (PDF/CSV/Excel)           |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Generate File Ekspor       |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Download File Statistik  |                            |
       |<--------------------------|                            |
       |                           |                            |
       v                           v                            v
```

## Penjelasan Alur Aktivitas

### 1. Akses Dashboard Statistik
1. **Admin** login ke sistem dengan kredensial admin.
2. **Admin** mengakses dashboard admin.
3. **Sistem** mengambil data statistik umum dari database.
4. **Sistem** melakukan perhitungan statistik (seperti jumlah total pengguna, kuis, soal, dll).
5. **Sistem** menampilkan dashboard dengan statistik umum.

### 2. Melihat Statistik Pengguna
1. **Admin** memilih kategori statistik pengguna.
2. **Sistem** mengambil data statistik pengguna dari database.
3. **Sistem** menampilkan statistik pengguna, termasuk:
   - Jumlah pengguna per role (admin, guru, siswa)
   - Tingkat pertumbuhan pengguna
   - Pengguna aktif vs tidak aktif
   - Pendaftaran guru yang menunggu persetujuan

### 3. Melihat Statistik Soal
1. **Admin** memilih kategori statistik soal.
2. **Sistem** mengambil data statistik soal dari database.
3. **Sistem** menampilkan statistik soal, termasuk:
   - Jumlah soal per jenis (pilihan ganda, benar/salah, esai)
   - Jumlah soal per tingkat kesulitan
   - Jumlah soal yang dihasilkan AI vs dibuat manual
   - Topik soal terpopuler

### 4. Melihat Statistik Kuis
1. **Admin** memilih kategori statistik kuis.
2. **Sistem** mengambil data statistik kuis dari database.
3. **Sistem** menampilkan statistik kuis, termasuk:
   - Jumlah kuis aktif vs nonaktif
   - Tingkat partisipasi kuis
   - Distribusi nilai kuis
   - Topik kuis terpopuler

### 5. Filtering dan Ekspor Data
1. **Admin** dapat memilih filter waktu untuk melihat statistik dalam rentang waktu tertentu.
2. **Sistem** mengambil data dengan filter yang ditentukan.
3. **Sistem** menampilkan data yang telah difilter.
4. **Admin** dapat memilih untuk mengekspor statistik dalam format PDF, CSV, atau Excel.
5. **Sistem** menghasilkan file ekspor.
6. **Admin** mengunduh file statistik.
