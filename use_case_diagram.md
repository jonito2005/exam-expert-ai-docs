# Use Case Diagram - ExamExpert-AI

Use Case Diagram berikut menggambarkan fungsionalitas sistem ExamExpert-AI dan interaksi antara berbagai aktor dengan sistem.

```
                           +---------------------------------------------+
                           |                ExamExpert-AI                 |
                           +---------------------------------------------+
                           |                                             |
  +----------+             | +-------------+    +-------------------+    |
  |          |             | |             |    |                   |    |
  |  Admin   |-------------+-| Kelola User |    | Lihat Statistik   |    |
  |          |             | |             |    | Sistem            |    |
  +----------+             | +-------------+    +-------------------+    |
       |                   |         |                                   |
       |                   | +----------------+                          |
       |                   | |                |                          |
       +-------------------+-| Setujui Guru   |                          |
                           | |                |                          |
                           | +----------------+                          |
                           |                                             |
  +----------+             | +-------------+    +-------------------+    |
  |          |             | |             |    |                   |    |
  |   Guru   |-------------+-| Buat Soal AI|----| Tinjau & Setujui  |    |
  |          |             | |             |    | Soal              |    |
  +----------+             | +-------------+    +-------------------+    |
       |                   |       |                      |              |
       |                   |       |                      |              |
       |                   | +-----v------+    +----------v--------+    |
       |                   | |            |    |                   |    |
       +-------------------+-| Buat Kuis  |----| Kelola Kuis       |    |
       |                   | |            |    |                   |    |
       |                   | +------------+    +-------------------+    |
       |                   |                             |              |
       |                   | +---------------------+     |              |
       |                   | |                     |     |              |
       +-------------------+-| Lihat Hasil Kuis    |<----+              |
                           | |                     |                    |
                           | +---------------------+                    |
                           |                                             |
  +----------+             | +-------------+    +-------------------+    |
  |          |             | |             |    |                   |    |
  |  Siswa   |-------------+-| Gabung Kuis |----| Kerjakan Kuis     |    |
  |          |             | |             |    |                   |    |
  +----------+             | +-------------+    +-------------------+    |
                           |                             |              |
                           | +---------------------+     |              |
                           | |                     |     |              |
                           | | Lihat Nilai         |<----+              |
                           | |                     |                    |
                           | +---------------------+                    |
                           |                                             |
                           +---------------------------------------------+
```

## Deskripsi Use Case

### Aktor
1. **Admin**: Pengelola sistem dengan akses penuh
2. **Guru**: Pengajar yang membuat soal dan kuis
3. **Siswa**: Peserta yang mengerjakan kuis

### Use Case untuk Admin
1. **Kelola User**: Admin dapat membuat, mengedit, dan menghapus akun pengguna
2. **Lihat Statistik Sistem**: Admin dapat melihat statistik penggunaan sistem
3. **Setujui Guru**: Admin menyetujui atau menolak pendaftaran sebagai guru

### Use Case untuk Guru
1. **Buat Soal AI**: Guru dapat membuat soal menggunakan bantuan AI (Perplexity API)
2. **Tinjau & Setujui Soal**: Guru dapat meninjau, mengedit, dan menyetujui soal yang dihasilkan AI
3. **Buat Kuis**: Guru dapat membuat kuis baru dengan soal-soal yang disetujui
4. **Kelola Kuis**: Guru dapat mengedit, mengaktifkan, atau menonaktifkan kuis
5. **Lihat Hasil Kuis**: Guru dapat melihat hasil dan statistik kuis yang telah dikerjakan siswa

### Use Case untuk Siswa
1. **Gabung Kuis**: Siswa dapat bergabung ke kuis menggunakan kode akses unik
2. **Kerjakan Kuis**: Siswa dapat mengerjakan kuis yang telah mereka ikuti
3. **Lihat Nilai**: Siswa dapat melihat nilai dan hasil kuis mereka

### Use Case Umum
1. **Login/Autentikasi**: Semua pengguna harus login ke sistem dengan kredensial mereka (tidak ditampilkan dalam diagram)
2. **Kelola Profil**: Semua pengguna dapat mengelola profil mereka sendiri (tidak ditampilkan dalam diagram)
