# Activity Diagram - Tinjau dan Setujui Soal oleh Guru

Diagram aktivitas berikut menggambarkan proses guru meninjau dan menyetujui soal yang dihasilkan oleh AI atau dibuat oleh guru lain dalam sistem ExamExpert-AI.

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
       | Akses Menu Tinjau Soal    |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Daftar Soal Belum    |
       |                           | Disetujui                  |
       |                           |--------------------------->|
       |                           |                            |
       |                           |  Daftar Soal Belum Disetujui|
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Daftar Soal    |                            |
       |  dengan Filter & Sorting  |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Soal untuk Ditinjau |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Ambil Detail Soal          |
       |                           |--------------------------->|
       |                           |                            |
       |                           |     Detail Soal            |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Detail Soal    |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Tinjau Soal               |                            |
       |------------+              |                            |
       |            |              |                            |
       |<-----------+              |                            |
       |                           |                            |
       | Pilih Aksi                |                            |
       | (Setuju/Edit/Tolak)       |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Jika Aksi = Setuju         |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Update Status Soal         |
       |                           | menjadi Disetujui          |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Update       |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Konfirmasi     |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Aksi = Edit           |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Form Edit Soal |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Edit Konten Soal          |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Validasi Perubahan         |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |                           | Simpan Perubahan Soal      |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Simpan       |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Konfirmasi &   |                            |
       |  Opsi Setujui             |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Setujui Soal yang Diedit  |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Update Status Soal         |
       |                           | menjadi Disetujui          |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Update       |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Konfirmasi     |                            |
       |<--------------------------|                            |
       |                           |                            |
       |                           | Jika Aksi = Tolak          |
       |                           |------------+               |
       |                           |            |               |
       |                           |<-----------+               |
       |                           |                            |
       |  Tampilkan Form Alasan    |                            |
       |  Penolakan                |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Masukkan Alasan Penolakan |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Update Status Soal         |
       |                           | menjadi Ditolak            |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Update       |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Konfirmasi     |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Lanjut Tinjau Soal Lain   |                            |
       |-------------------------->|                            |
       |                           |                            |
       | Pilih Tinjau Masal        |                            |
       | (opsional)                |                            |
       |-------------------------->|                            |
       |                           |                            |
       |  Tampilkan Opsi Tinjau    |                            |
       |  Masal                    |                            |
       |<--------------------------|                            |
       |                           |                            |
       | Pilih Beberapa Soal dan   |                            |
       | Aksi Masal                |                            |
       |-------------------------->|                            |
       |                           |                            |
       |                           | Proses Aksi Masal          |
       |                           |--------------------------->|
       |                           |                            |
       |                           |    Konfirmasi Proses       |
       |                           |<---------------------------|
       |                           |                            |
       |  Tampilkan Konfirmasi     |                            |
       |<--------------------------|                            |
       |                           |                            |
       v                           v                            v
```

## Penjelasan Alur Aktivitas

### 1. Akses Menu Tinjau Soal
1. **Guru** login ke sistem dan mengakses menu tinjau soal.
2. **Sistem** mengambil daftar soal yang belum disetujui dari database.
3. **Sistem** menampilkan daftar soal dengan opsi filter (berdasarkan jenis, topik, dll) dan sorting.

### 2. Peninjauan Detail Soal
1. **Guru** memilih soal tertentu untuk ditinjau.
2. **Sistem** mengambil detail soal dari database.
3. **Sistem** menampilkan detail soal, termasuk:
   - Konten soal
   - Opsi jawaban (untuk pilihan ganda)
   - Jawaban yang benar
   - Penjelasan
   - Metadata (tipe soal, tingkat kesulitan, dll)
4. **Guru** meninjau soal dengan teliti untuk memastikan kualitas dan kesesuaian.

### 3. Aksi Persetujuan
1. **Guru** memilih aksi untuk soal tersebut:
   - Setuju: Menyetujui soal tanpa perubahan
   - Edit: Memperbaiki soal sebelum menyetujui
   - Tolak: Menolak soal karena tidak memenuhi standar

2. Jika aksi = Setuju:
   - **Sistem** memperbarui status soal menjadi "Disetujui" di database
   - **Sistem** menampilkan konfirmasi

3. Jika aksi = Edit:
   - **Sistem** menampilkan form edit soal
   - **Guru** mengubah konten soal, opsi jawaban, atau penjelasan
   - **Sistem** memvalidasi perubahan
   - **Sistem** menyimpan perubahan soal di database
   - **Sistem** menampilkan konfirmasi dan opsi untuk menyetujui
   - **Guru** menyetujui soal yang telah diedit
   - **Sistem** memperbarui status soal menjadi "Disetujui"

4. Jika aksi = Tolak:
   - **Sistem** menampilkan form untuk memasukkan alasan penolakan
   - **Guru** memberikan alasan mengapa soal ditolak
   - **Sistem** memperbarui status soal menjadi "Ditolak" dan menyimpan alasan
   - **Sistem** menampilkan konfirmasi

### 4. Tinjau Masal (Opsional)
1. **Guru** dapat memilih opsi tinjau masal untuk menangani banyak soal sekaligus.
2. **Sistem** menampilkan opsi untuk tinjau masal.
3. **Guru** memilih beberapa soal dan menentukan aksi masal (setujui/tolak).
4. **Sistem** memproses aksi masal pada soal-soal yang dipilih.
5. **Sistem** menampilkan konfirmasi keberhasilan.
