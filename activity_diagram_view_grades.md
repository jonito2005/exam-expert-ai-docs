# Activity Diagram - Lihat Nilai oleh Siswa

Diagram aktivitas berikut menggambarkan proses siswa melihat nilai dan hasil kuis dalam sistem ExamExpert-AI.

```
+-------------+          +-------------------+          +-------------------+
|             |          |                   |          |                   |
|    Siswa    |          |       Sistem      |          |   Database        |
|             |          |                   |          |                   |
+-------------+          +-------------------+          +-------------------+
       |                           |                            |
       | Login sebagai Siswa       |                            |
       |-------------------------->|                            |
       |                           |                            |
       | Akses Dashboard Siswa     |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Data Ringkasan       |
       |                           | Kuis Siswa                 |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Data Ringkasan         |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Dashboard      |                            |
       |  dengan Ringkasan Kuis    |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Menu "Nilai Saya"   |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Daftar Kuis yang     |
       |                           | Telah Dikerjakan           |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Daftar Kuis            |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Daftar Kuis    |                            |
       |  dengan Nilai             |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Filter atau Sorting |                            |
       | (opsional)                |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Terapkan Filter/Sorting    |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Hasil          |                            |
       |  Terfilter/Terurut        |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Kuis Tertentu       |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Detail Hasil Kuis    |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Detail Hasil Kuis      |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Detail Hasil   |                            |
       |  Kuis                     |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Lihat Detail Jawaban|                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Detail Jawaban       |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Detail Jawaban         |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Detail Jawaban |                            |
       |  dengan Pembahasan        |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Lihat Soal Berikut/ |                            |
       | Sebelumnya                |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Data Soal            |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Data Soal              |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Soal dan       |                            |
       |  Jawaban                  |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Kembali ke Daftar   |                            |
       | Nilai                     |                            |
       |-------------------------->|                            |
       |                           |                            |
       |  Tampilkan Daftar Nilai   |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Ekspor Hasil        |                            |
       | (opsional)                |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Generate File Ekspor       |
       |                           | (PDF)                      |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Download File Hasil      |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Lihat Statistik     |                            |
       | Performa                  |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Data Statistik       |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Data Statistik         |
       |                           |<---------------------------|
       |                           |                            |
       |                           | Hitung Tren & Perbandingan |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Visualisasi    |                            |
       |  Performa                 |                            |
       |<--------------------------|                            |
       |                           |                            |
       v                           v                            v
```

## Penjelasan Alur Aktivitas

### 1. Akses Nilai
1. **Siswa** login ke sistem dan mengakses dashboard siswa.
2. **Sistem** mengambil data ringkasan kuis yang telah dikerjakan oleh siswa dari database.
3. **Sistem** menampilkan dashboard dengan ringkasan kuis (jumlah kuis, nilai rata-rata, dll).
4. **Siswa** memilih menu "Nilai Saya" untuk melihat daftar lengkap nilai.
5. **Sistem** mengambil daftar kuis yang telah dikerjakan oleh siswa dari database.
6. **Sistem** menampilkan daftar kuis beserta nilai yang diperoleh.

### 2. Melihat Daftar Nilai
1. **Siswa** dapat memilih filter atau pengurutan untuk daftar nilai (opsional), seperti:
   - Filter berdasarkan periode waktu
   - Filter berdasarkan subjek/kategori
   - Pengurutan berdasarkan nilai (tinggi ke rendah atau sebaliknya)
   - Pengurutan berdasarkan tanggal
2. **Sistem** menerapkan filter/pengurutan yang dipilih.
3. **Sistem** menampilkan hasil yang terfilter/terurut.

### 3. Melihat Detail Hasil Kuis
1. **Siswa** memilih kuis tertentu untuk melihat detail hasil.
2. **Sistem** mengambil detail hasil kuis dari database.
3. **Sistem** menampilkan detail hasil kuis, termasuk:
   - Nilai keseluruhan
   - Jumlah jawaban benar dan salah
   - Waktu pengerjaan
   - Persentase keberhasilan
   - Peringkat (jika ada)

### 4. Melihat Detail Jawaban
1. **Siswa** memilih untuk melihat detail jawaban.
2. **Sistem** mengambil detail jawaban dari database.
3. **Sistem** menampilkan detail jawaban beserta:
   - Soal yang dijawab
   - Jawaban siswa
   - Jawaban yang benar
   - Pembahasan atau penjelasan
   - Status jawaban (benar/salah)
4. **Siswa** dapat memilih untuk melihat soal berikutnya atau sebelumnya.
5. **Sistem** mengambil data soal yang dipilih.
6. **Sistem** menampilkan soal dan jawaban.

### 5. Fitur Tambahan
1. **Siswa** dapat memilih untuk kembali ke daftar nilai.
2. **Siswa** dapat memilih untuk mengekspor hasil kuis dalam format PDF (opsional).
3. **Sistem** menghasilkan file ekspor.
4. **Siswa** mengunduh file hasil.
5. **Siswa** dapat memilih untuk melihat statistik performa (opsional).
6. **Sistem** mengambil data statistik dan menghitung tren serta perbandingan.
7. **Sistem** menampilkan visualisasi performa, seperti:
   - Grafik perkembangan nilai dari waktu ke waktu
   - Perbandingan dengan nilai rata-rata kelas
   - Area kekuatan dan kelemahan berdasarkan kategori soal
