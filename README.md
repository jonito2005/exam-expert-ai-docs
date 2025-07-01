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

### 2. [Diagram Aktivitas](./activity-diagrams.md)
Menggambarkan alur aktivitas dan decision points dalam sistem:
- **Proses Pendaftaran dan Persetujuan Guru** - Alur registrasi dan persetujuan guru
- **Proses Pembuatan dan Tinjauan Soal AI** - Proses generate dan review soal AI
- **Proses Pembuatan dan Eksekusi Kuis** - Pembuatan dan eksekusi kuis
- **Alur Autentikasi Pengguna** - Alur autentikasi dengan decision points
- **Proses Pengelolaan Pengguna Admin** - Pengelolaan user oleh admin
- **Proses Statistik dan Analitik Soal** - Statistik dan analitik soal

### 3. [Diagram Use Case](./use-case-diagrams.md)
Menunjukkan fungsionalitas sistem dari perspektif pengguna:
- **Use Case Sistem Keseluruhan** - Use case keseluruhan sistem
- **Use Case Pengelolaan Guru** - Pengelolaan guru
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
- Registrasi pengguna (Siswa, Guru, Admin)
- Login dengan JWT token
- Kontrol akses berbasis peran
- Alur persetujuan guru

### Pengelolaan Soal
- Generate soal otomatis menggunakan AI (Perplexity)
- Review dan persetujuan soal oleh admin
- Operasi CRUD untuk soal
- Kategorisasi berdasarkan topik dan tingkat kesulitan

### Manajemen Kuis
- Pembuatan kuis dari soal yang disetujui
- Access code untuk join kuis
- Timer dan scheduling kuis
- Real-time quiz taking
- Automated scoring

### Dashboard dan Laporan
- Admin dashboard dengan statistik sistem
- Teacher dashboard untuk manage kuis dan soal
- Student dashboard untuk riwayat kuis
- Export hasil kuis (CSV/PDF)
- Analytics dan reporting

### Manajemen File
- Upload dokumen untuk registrasi teacher
- File storage untuk sertifikat dan dokumen
- Secure file access

## 🔧 Teknologi yang Digunakan

### Backend
- **Node.js** dengan Express.js
- **MongoDB** sebagai database
- **JWT** untuk authentication
- **Multer** untuk file upload
- **Perplexity AI** untuk question generation
- **Email service** untuk notifikasi

### Frontend
- **React** dengan TypeScript
- **Vite** sebagai build tool
- **Tailwind CSS** untuk styling
- **Zustand** untuk state management

### Infrastructure
- RESTful API design
- File storage system
- Email notification system
- Security middleware (CORS, rate limiting)

## 📋 Endpoints API Utama

Berdasarkan Postman Collection, sistem memiliki endpoint-endpoint berikut:

### Authentication (`/api/auth`)
- `POST /register` - Registrasi user
- `POST /login` - Login user
- `GET /me` - Profile user saat ini

### Admin (`/api/admin`)
- `GET /pending-teachers` - Daftar guru pending
- `PUT /approve-teacher/:id` - Approve guru
- `PUT /reject-teacher/:id` - Reject guru
- `GET /statistics` - Statistik sistem
- `GET /users` - Manajemen user
- `GET /question-statistics` - Statistik soal

### Questions (`/api/questions`)
- `POST /generate` - Generate soal AI
- `POST /approve` - Approve soal
- `GET /pending-review` - Soal pending review
- `PUT /:id/approve` - Approve soal tunggal
- `PUT /:id/reject` - Reject soal

### Quizzes (`/api/quizzes`)
- `POST /` - Buat kuis baru
- `POST /join` - Join kuis dengan access code
- `POST /:id/submit` - Submit jawaban kuis
- `GET /:id/results` - Hasil kuis
- `POST /:id/generate-code` - Generate access code

### Students (`/api/students`)
- `POST /join-quiz` - Join kuis
- `POST /submit-answers` - Submit jawaban
- `GET /history` - Riwayat kuis
- `GET /available-quizzes` - Kuis yang tersedia

### Teachers (`/api/teachers`)
- `POST /register` - Registrasi guru dengan dokumen
- `GET /status` - Status registrasi
- `GET /pending` - Daftar guru pending (admin)

## 🚀 Cara Menggunakan Diagram

1. **Untuk Developer**: Gunakan sequence dan activity diagrams untuk memahami flow aplikasi
2. **Untuk Project Manager**: Gunakan use case diagrams untuk overview fungsionalitas
3. **Untuk System Architect**: Gunakan system architecture untuk understanding technical stack
4. **Untuk Testing**: Gunakan activity diagrams untuk test case scenarios

## 📝 Catatan

Diagram-diagram ini dibuat berdasarkan Postman Collection yang disediakan dan merepresentasikan fitur-fitur utama sistem ExamExpert-AI. Setiap diagram menggunakan format Mermaid yang dapat di-render di GitHub, GitLab, atau platform dokumentasi lainnya.

Untuk detail implementasi lebih lanjut, silakan merujuk ke source code dan dokumentasi API yang tersedia.
