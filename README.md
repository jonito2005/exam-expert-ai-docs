# Diagram Sistem ExamExpert-AI

Dokumentasi ini berisi diagram-diagram sistem untuk aplikasi ExamExpert-AI yang dibuat berdasarkan Postman Collection API documentation.

## 📊 Daftar Diagram

### 1. [Diagram Sequence](./sequence-diagrams.md)
Menunjukkan interaksi antar komponen sistem dalam urutan waktu:
- **Alur Autentikasi Pengguna** - Proses login dan registrasi
- **Proses Persetujuan Pengajar** - Alur persetujuan Pengajar oleh admin
- **Proses Pembuatan dan Tinjauan Soal** - Proses pembuatan dan review soal AI
- **Pembuatan dan Pengelolaan Kuis** - Pembuatan dan pengelolaan kuis
- **Proses Pelajar Mengerjakan Kuis** - Proses Pelajar mengerjakan kuis
- **Dashboard Admin dan Statistik** - Dashboard admin dan statistik sistem

### 2. [Diagram Aktivitas](./activity-diagrams.md)
Menggambarkan alur aktivitas dan decision points dalam sistem:
- **Proses Pendaftaran dan Persetujuan Pengajar** - Alur registrasi dan persetujuan Pengajar
- **Proses Pembuatan dan Tinjauan Soal AI** - Proses generate dan review soal AI
- **Proses Pembuatan dan Eksekusi Kuis** - Pembuatan dan eksekusi kuis
- **Alur Autentikasi Pengguna** - Alur autentikasi dengan decision points
- **Proses Pengelolaan Pengguna Admin** - Pengelolaan user oleh admin
- **Proses Statistik dan Analitik Soal** - Statistik dan analitik soal

### 3. [Diagram Use Case](./use-case-diagrams.md)
Menunjukkan fungsionalitas sistem dari perspektif pengguna:
- **Use Case Sistem Keseluruhan** - Use case keseluruhan sistem
- **Use Case Pengelolaan Pengajar** - Pengelolaan Pengajar
- **Use Case Pengelolaan Soal** - Pengelolaan soal
- **Use Case Pengelolaan Kuis** - Pengelolaan kuis
- **Use Case Administratif** - Use case administratif

### 4. [Arsitektur Sistem](./system-architecture.md)
Menggambarkan arsitektur teknis sistem:
- **Diagram Arsitektur Sistem** - Arsitektur keseluruhan sistem
- **Relasi Skema Database** - Relasi skema database
- **Arsitektur Alur API** - Alur arsitektur API

## 🎯 Fitur Utama yang Dicakup

### Autentikasi dan Otorisasi
- Registrasi pengguna (Pelajar, Pengajar, Admin)
- Login dengan JWT token
- Kontrol akses berbasis peran
- Alur persetujuan Pengajar

### Pengelolaan Soal
- Generate soal otomatis menggunakan AI (Perplexity)
- Pengajar meninjau dan approve/reject soal buatannya sendiri
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
- Dashboard Pengajar untuk mengelola kuis, soal, dan tinjauan soal sendiri
- Dashboard Pelajar untuk riwayat kuis
- Ekspor hasil kuis (CSV/PDF)
- Analitik dan pelaporan

### Pengelolaan File
- Upload dokumen untuk registrasi Pengajar
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
- `GET /pending-teachers` - Daftar Pengajar menunggu
- `PUT /approve-teacher/:id` - Setujui Pengajar
- `PUT /reject-teacher/:id` - Tolak Pengajar
- `GET /statistics` - Statistik sistem
- `GET /users` - Pengelolaan pengguna
- `DELETE /users/:id` - Hapus pengguna

### Soal (`/api/questions`)
- `POST /generate` - Buat soal AI
- `GET /my-questions` - Soal milik Pengajar
- `PUT /:id/approve` - Setujui soal sendiri
- `PUT /:id/reject` - Tolak soal sendiri
- `PUT /:id` - Edit soal sebelum disetujui

### Kuis (`/api/quizzes`)
- `POST /` - Buat kuis baru
- `POST /join` - Bergabung kuis dengan kode akses
- `POST /:id/submit` - Kirim jawaban kuis
- `GET /:id/results` - Hasil kuis
- `POST /:id/generate-code` - Buat kode akses

### Pelajar (`/api/students`)
- `POST /join-quiz` - Bergabung kuis
- `POST /submit-answers` - Kirim jawaban
- `GET /history` - Riwayat kuis
- `GET /available-quizzes` - Kuis yang tersedia

### Pengajar (`/api/teachers`)
- `POST /register` - Registrasi Pengajar dengan dokumen
- `GET /status` - Status registrasi
- `GET /pending` - Daftar Pengajar menunggu (admin)

## 🚀 Cara Menggunakan Diagram

1. **Untuk Developer**: Gunakan diagram sequence dan aktivitas untuk memahami alur aplikasi
2. **Untuk Project Manager**: Gunakan diagram use case untuk overview fungsionalitas
3. **Untuk System Architect**: Gunakan arsitektur sistem untuk memahami technical stack
4. **Untuk Testing**: Gunakan diagram aktivitas untuk skenario test case

## 📝 Catatan

Diagram-diagram ini dibuat berdasarkan Postman Collection yang disediakan dan merepresentasikan fitur-fitur utama sistem ExamExpert-AI. Setiap diagram menggunakan format Mermaid yang dapat di-render di GitHub, GitLab, atau platform dokumentasi lainnya.

Untuk detail implementasi lebih lanjut, silakan merujuk ke source code dan dokumentasi API yang tersedia.
