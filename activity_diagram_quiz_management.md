# Activity Diagram - Kelola Kuis oleh Guru

Diagram aktivitas berikut menggambarkan proses pengelolaan kuis oleh guru dalam sistem ExamExpert-AI.

```
+-------------+          +-------------------+          +-------------------+
|             |          |                   |          |                   |
|    Guru     |          |       Sistem      |          |   Database        |
|             |          |                   |          |                   |
+-------------+          +-------------------+          +-------------------+
       |                           |                            |
       | Login sebagai Guru        |                            |
       |-------------------------->|                            |
       |                           |                            |
       | Akses Menu Kelola Kuis    |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Daftar Kuis Guru     |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Data Kuis Guru         |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Daftar Kuis    |                            |
       |  dengan Status & Filter   |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Aksi (Edit/         |                            |
       | Aktif/Nonaktif/Hapus/     |                            |
       | Duplikat)                 |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Jika Aksi = Edit Kuis      |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Ambil Detail Kuis          |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Detail Kuis            |
       |                           |<---------------------------|
       |                           |                            |
       |    Tampilkan Form Edit    |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Edit Kuis (Judul/Deskripsi|                            |
       | /Instruksi/Batas Waktu/   |                            |
       | Soal/dll)                 |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Validasi Perubahan         |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Update Kuis                |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Update       |
       |                           |<---------------------------|
       |                           |                            |
       |    Tampilkan Konfirmasi   |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Aksi = Aktivasi/      |
       |                           | Deaktivasi                 |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |    Tampilkan Konfirmasi   |                            |
       |    Aktivasi/Deaktivasi    |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Konfirmasi Aktivasi/      |                            |
       | Deaktivasi                |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Update Status Kuis         |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Update       |
       |                           |<---------------------------|
       |                           |                            |
       |    Tampilkan Notifikasi   |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Aksi = Hapus Kuis     |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |    Tampilkan Konfirmasi   |                            |
       |    Hapus                  |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Konfirmasi Hapus          |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Cek Apakah Kuis Sudah      |
       |                           | Dikerjakan Siswa           |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Status Pengerjaan       |
       |                           |<---------------------------|
       |                           |                            |
       |                           | Jika Belum Dikerjakan      |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Hapus Kuis                 |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Hapus        |
       |                           |<---------------------------|
       |                           |                            |
       |    Tampilkan Notifikasi   |                            |
       |    Hapus                  |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Sudah Dikerjakan      |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |    Tampilkan Peringatan   |                            |
       |    Arsip vs Hapus Total   |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Arsip atau Hapus    |                            |
       | Total                     |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Proses Sesuai Pilihan      |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Proses       |
       |                           |<---------------------------|
       |                           |                            |
       |    Tampilkan Notifikasi   |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Aksi = Duplikat Kuis  |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Ambil Detail Kuis          |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Detail Kuis            |
       |                           |<---------------------------|
       |                           |                            |
       |    Tampilkan Form         |                            |
       |    Duplikat Kuis          |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Edit Detail Duplikat      |                            |
       | (opsional)                |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Buat Kuis Baru dari        |
       |                           | Template                   |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Pembuatan    |
       |                           |<---------------------------|
       |                           |                            |
       |    Tampilkan Notifikasi   |                            |
       |    & Link ke Kuis Baru    |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Lihat Analitik Kuis |                            |
       | (opsional)                |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Data Analitik        |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Data Analitik          |
       |                           |<---------------------------|
       |                           |                            |
       |    Tampilkan Analitik     |                            |
       |    Kuis                   |                            |
       |<--------------------------|                            |
       |                           |                            |
       v                           v                            v
```

## Penjelasan Alur Aktivitas

### 1. Akses Menu Kelola Kuis
1. **Guru** login ke sistem dan mengakses menu kelola kuis.
2. **Sistem** mengambil daftar kuis yang telah dibuat oleh guru dari database.
3. **Sistem** menampilkan daftar kuis dengan status (aktif/nonaktif) dan opsi filter.

### 2. Edit Kuis
1. **Guru** memilih kuis tertentu dan aksi edit.
2. **Sistem** mengambil detail kuis dari database.
3. **Sistem** menampilkan formulir edit dengan data kuis yang sudah ada.
4. **Guru** mengubah detail kuis yang diperlukan, seperti:
   - Judul kuis
   - Deskripsi
   - Instruksi
   - Batas waktu pengerjaan
   - Soal-soal dalam kuis
   - Urutan soal
   - Pengaturan skor
   - Opsi pengacakan soal
5. **Sistem** memvalidasi perubahan.
6. **Sistem** memperbarui data kuis di database.
7. **Sistem** menampilkan konfirmasi keberhasilan.

### 3. Aktivasi/Deaktivasi Kuis
1. **Guru** memilih kuis tertentu dan aksi aktivasi/deaktivasi.
2. **Sistem** menampilkan konfirmasi.
3. **Guru** mengkonfirmasi perubahan status.
4. **Sistem** memperbarui status kuis di database.
5. **Sistem** menampilkan notifikasi keberhasilan.

### 4. Hapus Kuis
1. **Guru** memilih kuis tertentu dan aksi hapus.
2. **Sistem** menampilkan konfirmasi hapus.
3. **Guru** mengkonfirmasi penghapusan.
4. **Sistem** memeriksa apakah kuis sudah pernah dikerjakan oleh siswa.
5. Jika belum dikerjakan:
   - **Sistem** menghapus kuis dari database
   - **Sistem** menampilkan notifikasi keberhasilan
6. Jika sudah dikerjakan:
   - **Sistem** menampilkan peringatan dengan opsi arsip (soft delete) atau hapus total
   - **Guru** memilih opsi yang diinginkan
   - **Sistem** memproses sesuai pilihan
   - **Sistem** menampilkan notifikasi keberhasilan

### 5. Duplikat Kuis
1. **Guru** memilih kuis tertentu dan aksi duplikat.
2. **Sistem** mengambil detail kuis dari database.
3. **Sistem** menampilkan formulir duplikat kuis dengan data dari kuis asli.
4. **Guru** dapat mengubah detail kuis duplikat (opsional).
5. **Sistem** membuat kuis baru berdasarkan template kuis yang dipilih.
6. **Sistem** menampilkan notifikasi keberhasilan dan link ke kuis baru.

### 6. Lihat Analitik Kuis (Opsional)
1. **Guru** memilih untuk melihat analitik kuis.
2. **Sistem** mengambil data analitik kuis dari database.
3. **Sistem** menampilkan analitik kuis, termasuk:
   - Jumlah pengerjaan
   - Nilai rata-rata
   - Distribusi nilai
   - Soal dengan tingkat kesulitan tertinggi/terendah
   - Waktu pengerjaan rata-rata
