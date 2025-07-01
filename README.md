# Diagram Sistem ExamExpert-AI

Dokumentasi ini berisi diagram-diagram sistem untuk aplikasi ExamExpert-AI yang dibuat berdasarkan Postman Collection API documentation.

## 📊 Daftar Diagram

### 1. [Diagram Sequence](./sequence-diagrams.md)
Menunjukkan interaksi antar komponen sistem dalam urutan waktu:
- **Alur Autentikasi Pengguna** - Proses login dan registrasi
- **Proses Persetujuan Guru** - Alur persetujuan guru oleh admin
- **Proses Pembuatan dan Tinjauan Soal** - Proses pembuatan dan review soal AI
- **Pembuatan dan Pengelolaan Kuis** - Pembuatan dan pengelolaan kuis
- **Proses Siswa Mengerjakan Kuis** - Proses siswa mengerjakan kuis
- **Dashboard Admin dan Statistik** - Dashboard admin dan statistik sistem
- **Proses Registrasi Siswa vs Guru** - Perbandingan alur registrasi yang berbeda
- **Detail Upload Dokumen Guru** - Proses upload dokumen step-by-step
- **Notifikasi dan Status Update** - Sistem notifikasi real-time

### 2. [Diagram Aktivitas](./activity-diagrams.md)
Menggambarkan alur aktivitas dan decision points dalam sistem:
- **Proses Pendaftaran dan Persetujuan Guru** - Alur registrasi dan persetujuan guru
- **Proses Pembuatan dan Tinjauan Soal AI** - Proses generate dan review soal AI
- **Proses Pembuatan dan Eksekusi Kuis** - Pembuatan dan eksekusi kuis
- **Alur Autentikasi Pengguna** - Alur autentikasi dengan decision points
- **Proses Pengelolaan Pengguna Admin** - Pengelolaan user oleh admin
- **Proses Statistik dan Analitik Soal** - Statistik dan analitik soal
- **Proses Registrasi Pengguna (Perbandingan Siswa vs Guru)** - Flowchart registrasi berbeda
- **Detail Aktivitas Upload dan Verifikasi Dokumen Guru** - Proses upload dokumen detail

### 3. [Diagram Use Case](./use-case-diagrams.md)
Menunjukkan fungsionalitas sistem dari perspektif pengguna:
- **Use Case Sistem Keseluruhan** - Use case keseluruhan sistem dengan semua aktor
- **Use Case Pendaftaran Pengguna** - Alur pendaftaran untuk siswa dan guru
- **Use Case Manajemen Soal dan Kuis** - Pengelolaan soal AI dan kuis
- **Use Case Manajemen Pengguna (Admin)** - Pengelolaan pengguna oleh admin
- **Use Case Sistem dan Pemeliharaan** - Pemeliharaan sistem
- **Use Case Proses Registrasi Pengguna** - Detail proses registrasi berbeda untuk siswa dan guru
- **Use Case Upload dan Verifikasi Dokumen Guru** - Proses upload dan verifikasi dokumen
- **Use Case Perbandingan Alur Registrasi** - Ringkasan perbedaan registrasi siswa vs guru

### 4. [Arsitektur Sistem](./system-architecture.md)
Menggambarkan arsitektur teknis sistem:
- **Diagram Arsitektur Sistem** - Arsitektur keseluruhan sistem
- **Relasi Skema Database** - Relasi skema database
- **Arsitektur Alur API** - Alur arsitektur API

## 🎯 Fitur Utama yang Dicakup

### Autentikasi dan Otorisasi
- **Registrasi Siswa**: Proses sederhana dengan aktivasi langsung
- **Registrasi Guru**: Proses kompleks dengan upload dokumen dan approval admin
- Login dengan JWT token
- Kontrol akses berbasis peran (Admin, Guru, Siswa)
- Alur persetujuan guru dengan verifikasi dokumen
- Sistem notifikasi email untuk status registrasi

### Perbedaan Alur Registrasi
#### 👨‍🎓 **Registrasi Siswa (Sederhana)**
- Input data minimal: Nama, Email, Password
- Tidak perlu upload dokumen
- Akun langsung aktif setelah registrasi
- Waktu aktivasi: Instant

#### 👨‍🏫 **Registrasi Guru (Kompleks)**
- Input data lengkap: Data pribadi + institusi
- Upload 4 dokumen wajib:
  - 📜 Ijazah S1/S2
  - 🏆 Sertifikat Pendidik
  - 📝 Surat Rekomendasi
  - 🆔 KTP/Identitas
- Review manual oleh admin
- Akun aktif setelah disetujui
- Waktu aktivasi: 1-3 hari kerja

### Proses Upload dan Verifikasi Dokumen
- **Validasi File**: Format (PDF, JPG, PNG) dan ukuran (max 5MB)
- **Penyimpanan Aman**: File disimpan dengan nama unik
- **Preview Dokumen**: Admin dapat preview/download dokumen
- **Status Tracking**: Real-time status update untuk guru
- **Notifikasi Email**: Otomatis untuk setiap perubahan status

### Pengelolaan Soal
- Generate soal otomatis menggunakan AI (Perplexity)
- Guru meninjau dan approve/reject soal buatannya sendiri
- Operasi CRUD untuk soal
- Kategorisasi berdasarkan topik dan tingkat kesulitan

### Pengelolaan Kuis
- Pembuatan kuis dari soal yang disetujui
- Kode akses untuk bergabung kuis
- Timer dan penjadwalan kuis
- Mengerjakan kuis real-time
- Penilaian otomatis

### Dashboard dan Laporan
- Dashboard admin dengan statistik sistem dan pengelolaan pengguna
- Dashboard guru untuk mengelola kuis, soal, dan tinjauan soal sendiri
- Dashboard siswa untuk riwayat kuis
- Ekspor hasil kuis (CSV/PDF)
- Analitik dan pelaporan

### Pengelolaan File
- Upload dokumen untuk registrasi guru
- Penyimpanan file untuk sertifikat dan dokumen
- Akses file yang aman

## 🔧 Teknologi yang Digunakan

### Backend
- **Node.js** dengan Express.js
- **MongoDB** sebagai database
- **JWT** untuk autentikasi
- **Multer** untuk upload file
- **Perplexity AI** untuk pembuatan soal
- **Layanan email** untuk notifikasi

### Frontend
- **React** dengan TypeScript
- **Vite** sebagai build tool
- **Tailwind CSS** untuk styling
- **Zustand** untuk manajemen state

### Infrastruktur
- Desain RESTful API
- Sistem penyimpanan file
- Sistem notifikasi email
- Middleware keamanan (CORS, rate limiting)

## 📋 Endpoint API Utama

Berdasarkan Postman Collection, sistem memiliki endpoint-endpoint berikut:

### Autentikasi (`/api/auth`)
- `POST /register` - Registrasi pengguna
- `POST /login` - Login pengguna
- `GET /me` - Profil pengguna saat ini

### Admin (`/api/admin`)
- `GET /pending-teachers` - Daftar guru menunggu
- `PUT /approve-teacher/:id` - Setujui guru
- `PUT /reject-teacher/:id` - Tolak guru
- `GET /statistics` - Statistik sistem
- `GET /users` - Pengelolaan pengguna
- `DELETE /users/:id` - Hapus pengguna

### Soal (`/api/questions`)
- `POST /generate` - Buat soal AI
- `GET /my-questions` - Soal milik guru
- `PUT /:id/approve` - Setujui soal sendiri
- `PUT /:id/reject` - Tolak soal sendiri
- `PUT /:id` - Edit soal sebelum disetujui

### Kuis (`/api/quizzes`)
- `POST /` - Buat kuis baru
- `POST /join` - Bergabung kuis dengan kode akses
- `POST /:id/submit` - Kirim jawaban kuis
- `GET /:id/results` - Hasil kuis
- `POST /:id/generate-code` - Buat kode akses

### Siswa (`/api/students`)
- `POST /join-quiz` - Bergabung kuis
- `POST /submit-answers` - Kirim jawaban
- `GET /history` - Riwayat kuis
- `GET /available-quizzes` - Kuis yang tersedia

### Guru (`/api/teachers`)
- `POST /register` - Registrasi guru dengan dokumen
- `GET /status` - Status registrasi
- `GET /pending` - Daftar guru menunggu (admin)

## 🚀 Cara Menggunakan Diagram

1. **Untuk Developer**: Gunakan diagram sequence dan aktivitas untuk memahami alur aplikasi
2. **Untuk Project Manager**: Gunakan diagram use case untuk overview fungsionalitas
3. **Untuk System Architect**: Gunakan arsitektur sistem untuk memahami technical stack
4. **Untuk Testing**: Gunakan diagram aktivitas untuk skenario test case

## 📝 Catatan

Diagram-diagram ini dibuat berdasarkan Postman Collection yang disediakan dan merepresentasikan fitur-fitur utama sistem ExamExpert-AI. Setiap diagram menggunakan format Mermaid yang dapat di-render di GitHub, GitLab, atau platform dokumentasi lainnya.

Untuk detail implementasi lebih lanjut, silakan merujuk ke source code dan dokumentasi API yang tersedia.
