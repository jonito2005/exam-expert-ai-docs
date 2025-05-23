# Activity Diagram - Melihat Hasil Kuis oleh Guru

Diagram aktivitas berikut menggambarkan proses guru melihat dan menganalisis hasil kuis siswa dalam sistem ExamExpert-AI.

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
       | Akses Dashboard Guru      |                            |
       |-------------------------->|                            |
       |                           |                            |
       |  Tampilkan Dashboard      |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Menu Hasil Kuis     |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Daftar Kuis Guru     |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Data Kuis Guru         |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Daftar Kuis    |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Kuis Tertentu       |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Data Kuis & Hasil    |
       |                           |--------------------------->|
       |                           |                            |
       |                           |   Detail Kuis & Hasil      |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Ringkasan Hasil|                            |
       |  (Jumlah Peserta, Rata2,  |                            |
       |   Nilai Tertinggi/Terendah)|                           |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Lihat Detail Analisis|                           |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Hitung Statistik Analisis  |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Visualisasi    |                            |
       |  Performa Per Soal        |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Lihat Daftar Siswa  |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Data Siswa Peserta   |
       |                           |--------------------------->|
       |                           |                            |
       |                           |   Data Siswa & Nilai       |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Daftar Siswa   |                            |
       |  dengan Nilai             |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Siswa Tertentu      |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Detail Jawaban Siswa |
       |                           |--------------------------->|
       |                           |                            |
       |                           |  Detail Jawaban Siswa      |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Detail Jawaban |                            |
       |  Siswa Per Soal           |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Opsi Ekspor Hasil   |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Generate File Ekspor       |
       |                           | (CSV/PDF)                  |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Download File Hasil      |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Tandai Soal Bermasalah    |                            |
       | (opsional)                |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Update Status Soal         |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Update       |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Konfirmasi     |                            |
       |<--------------------------|                            |
       |                           |                            |
       v                           v                            v
```

## Penjelasan Alur Aktivitas

### 1. Akses Menu Hasil Kuis
1. **Guru** login ke sistem dan mengakses dashboard guru.
2. **Guru** memilih menu hasil kuis.
3. **Sistem** mengambil daftar kuis yang dibuat oleh guru dari database.
4. **Sistem** menampilkan daftar kuis kepada guru.

### 2. Melihat Ringkasan Hasil
1. **Guru** memilih kuis tertentu untuk dilihat hasilnya.
2. **Sistem** mengambil data kuis dan hasil pengerjaan dari database.
3. **Sistem** menampilkan ringkasan hasil kuis, termasuk:
   - Jumlah peserta
   - Nilai rata-rata
   - Nilai tertinggi dan terendah
   - Persentase kelulusan (jika ada batas kelulusan)

### 3. Analisis Performa Per Soal
1. **Guru** memilih untuk melihat detail analisis.
2. **Sistem** menghitung statistik analisis, seperti:
   - Tingkat kesulitan soal berdasarkan persentase jawaban benar
   - Soal yang paling banyak dijawab salah
   - Distribusi jawaban untuk soal pilihan ganda
3. **Sistem** menampilkan visualisasi performa per soal.

### 4. Melihat Performa Siswa
1. **Guru** memilih untuk melihat daftar siswa yang mengikuti kuis.
2. **Sistem** mengambil data siswa peserta dan nilai mereka dari database.
3. **Sistem** menampilkan daftar siswa beserta nilai mereka, diurutkan berdasarkan nilai.
4. **Guru** dapat memilih siswa tertentu untuk melihat detail jawaban.
5. **Sistem** mengambil detail jawaban siswa per soal dari database.
6. **Sistem** menampilkan detail jawaban siswa, termasuk:
   - Jawaban yang dipilih
   - Status jawaban (benar/salah)
   - Waktu yang digunakan untuk menjawab (jika tersedia)

### 5. Ekspor dan Tindak Lanjut
1. **Guru** memilih opsi untuk mengekspor hasil kuis.
2. **Sistem** menghasilkan file ekspor dalam format CSV atau PDF.
3. **Guru** mengunduh file hasil kuis.
4. **Guru** dapat menandai soal yang bermasalah (terlalu sulit, ambigu, dll).
5. **Sistem** memperbarui status soal di database.
6. **Sistem** menampilkan konfirmasi bahwa soal telah ditandai untuk peninjauan lebih lanjut.
