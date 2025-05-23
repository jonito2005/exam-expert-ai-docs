# Activity Diagram - Pembuatan Soal AI

Diagram aktivitas berikut menggambarkan proses pembuatan soal menggunakan AI melalui Perplexity API dalam sistem ExamExpert-AI.

```
+-------------+          +-------------------+          +-------------------+
|             |          |                   |          |                   |
|    Guru     |          |       Sistem      |          |   Perplexity API  |
|             |          |                   |          |                   |
+-------------+          +-------------------+          +-------------------+
       |                           |                            |
       | Login ke Sistem           |                            |
       |-------------------------->|                            |
       |                           |                            |
       | Akses Menu Pembuatan Soal |                            |
       |-------------------------->|                            |
       |                           |                            |
       |    Tampilkan Form         |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Isi Form (Topik, Jenis,   |                            |
       | Tingkat Kesulitan, Jumlah)|                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Validasi Input             |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Jika Input Valid           |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Siapkan Prompt untuk API   |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Kirim Permintaan ke API    |
       |                           |---------------------------->|
       |                           |                            |
       |                           |                            | Proses Permintaan
       |                           |                            |-------------+
       |                           |                            |             |
       |                           |                            |<------------+
       |                           |                            |
       |                           |       Kirim Respons        |
       |                           |<----------------------------|
       |                           |                            |
       |                           | Jika Respons Berhasil      |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Parsing JSON Hasil Soal    |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Simpan Soal ke Database    |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |    Tampilkan Soal         |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Tinjau Soal               |                            |
       |------------+              |                            |
       |            |              |                            |
       |<-----------+              |                            |
       |                           |                            |
       | Edit Soal (jika perlu)    |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Update Soal di Database    |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       | Setujui Soal              |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Tandai Soal sebagai        |
       |                           | Disetujui                  |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |      Konfirmasi           |                            |
       |<--------------------------|                            |
       |                           |                            |
       v                           v                            v
```

## Penjelasan Alur Aktivitas

### 1. Persiapan Pembuatan Soal
1. **Guru** login ke sistem dan mengakses menu pembuatan soal.
2. **Sistem** menampilkan formulir pembuatan soal.
3. **Guru** mengisi formulir dengan informasi yang diperlukan:
   - Topik soal (misalnya: matematika, fisika, sejarah)
   - Jenis soal (pilihan ganda, benar/salah, esai)
   - Tingkat kesulitan (mudah, sedang, sulit)
   - Jumlah soal yang diinginkan

### 2. Validasi dan Persiapan
1. **Sistem** memvalidasi input yang diberikan oleh guru.
2. **Sistem** menyiapkan prompt yang terstruktur untuk dikirimkan ke Perplexity API.
3. **Sistem** mengirimkan permintaan ke API dengan parameter yang sesuai.

### 3. Proses Generasi Soal
1. **Perplexity API** memproses permintaan dan menghasilkan soal-soal sesuai parameter.
2. **Perplexity API** mengirimkan respons dalam format JSON.
3. **Sistem** memproses respons JSON menjadi struktur soal yang dapat disimpan.
4. **Sistem** menyimpan soal-soal yang dihasilkan ke dalam database.

### 4. Peninjauan dan Persetujuan
1. **Sistem** menampilkan soal-soal yang dihasilkan kepada guru.
2. **Guru** meninjau setiap soal untuk memastikan kualitas dan kesesuaian.
3. **Guru** dapat mengedit soal jika diperlukan, seperti memperbaiki redaksi atau mengubah pilihan jawaban.
4. **Sistem** memperbarui soal yang diedit dalam database.
5. **Guru** menyetujui soal-soal yang sudah final.
6. **Sistem** menandai soal yang disetujui dan membuatnya tersedia untuk digunakan dalam kuis.

### 5. Penanganan Kegagalan (Tidak Ditampilkan dalam Diagram)
1. Jika validasi input gagal, sistem akan menampilkan pesan error dan meminta guru untuk memperbaiki input.
2. Jika permintaan ke API gagal, sistem akan menampilkan pesan error dan menawarkan opsi untuk mencoba kembali.
3. Jika parsing respons gagal, sistem akan mencatat error dan memberikan opsi untuk mencoba kembali dengan parameter berbeda.
