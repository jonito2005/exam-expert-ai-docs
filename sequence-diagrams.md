# Sequence Diagram Sistem ExamExpert-AI

## 1. Sequence Diagram - Registrasi Pengguna

```mermaid
sequenceDiagram
    participant Pengguna
    participant Frontend
    participant Backend
    participant Database
    participant EmailService

    Pengguna->>Frontend: Mengisi form registrasi
    Frontend->>Backend: POST /api/auth/register
    Backend->>Database: Cek email sudah terdaftar
    alt Email belum terdaftar
        Database-->>Backend: Email tersedia
        Backend->>Database: Simpan data pengguna
        Database-->>Backend: Data tersimpan
        Backend->>EmailService: Kirim email verifikasi
        EmailService-->>Backend: Email terkirim
        Backend-->>Frontend: Registrasi berhasil
        Frontend-->>Pengguna: Tampilkan pesan sukses
    else Email sudah terdaftar
        Database-->>Backend: Email sudah ada
        Backend-->>Frontend: Error email sudah terdaftar
        Frontend-->>Pengguna: Tampilkan pesan error
    end
```

## 2. Sequence Diagram - Login Pengguna

```mermaid
sequenceDiagram
    participant Pengguna
    participant Frontend
    participant Backend
    participant Database
    participant AuthMiddleware

    Pengguna->>Frontend: Input email dan password
    Frontend->>Backend: POST /api/auth/login
    Backend->>Database: Validasi kredensial
    alt Kredensial valid
        Database-->>Backend: Data pengguna valid
        Backend->>AuthMiddleware: Generate JWT token
        AuthMiddleware-->>Backend: Token dibuat
        Backend-->>Frontend: Login berhasil + token
        Frontend-->>Pengguna: Redirect ke dashboard
    else Kredensial tidak valid
        Database-->>Backend: Kredensial salah
        Backend-->>Frontend: Error login gagal
        Frontend-->>Pengguna: Tampilkan pesan error
    end
```

## 3. Sequence Diagram - Registrasi Pengajar

```mermaid
sequenceDiagram
    participant Pengajar
    participant Frontend
    participant Backend
    participant FileStorage
    participant Database
    participant EmailService
    participant Admin

    Pengajar->>Frontend: Mengisi form registrasi Pengajar
    Pengajar->>Frontend: Upload dokumen verifikasi
    Frontend->>Backend: POST /api/teachers/register
    Backend->>FileStorage: Simpan file dokumen
    FileStorage-->>Backend: File tersimpan
    Backend->>Database: Simpan data Pengajar (status: pending)
    Database-->>Backend: Data tersimpan
    Backend->>EmailService: Kirim notifikasi ke admin
    EmailService->>Admin: Email notifikasi Pengajar baru
    Backend-->>Frontend: Registrasi dikirim untuk review
    Frontend-->>Pengajar: Tampilkan status pending
```

## 4. Sequence Diagram - Persetujuan Pengajar oleh Admin

```mermaid
sequenceDiagram
    participant Admin
    participant Frontend
    participant Backend
    participant Database
    participant EmailService
    participant Pengajar

    Admin->>Frontend: Akses halaman pending teachers
    Frontend->>Backend: GET /api/admin/pending-teachers
    Backend->>Database: Ambil data Pengajar pending
    Database-->>Backend: Data Pengajar pending
    Backend-->>Frontend: List Pengajar pending
    Frontend-->>Admin: Tampilkan list Pengajar
    Admin->>Frontend: Pilih Pengajar untuk disetujui/ditolak
    alt Menyetujui Pengajar
        Frontend->>Backend: PUT /api/admin/approve-teacher/:id
        Backend->>Database: Update status Pengajar menjadi active
        Database-->>Backend: Status diupdate
        Backend->>EmailService: Kirim email approval
        EmailService->>Pengajar: Email pemberitahuan disetujui
        Backend-->>Frontend: Pengajar berhasil disetujui
        Frontend-->>Admin: Tampilkan konfirmasi
    else Menolak Pengajar
        Frontend->>Backend: PUT /api/admin/reject-teacher/:id
        Backend->>Database: Update status Pengajar menjadi rejected
        Backend->>EmailService: Kirim email penolakan
        EmailService->>Pengajar: Email pemberitahuan ditolak
        Backend-->>Frontend: Pengajar berhasil ditolak
        Frontend-->>Admin: Tampilkan konfirmasi
    end
```

## 5. Sequence Diagram - Generate Soal AI

```mermaid
sequenceDiagram
    participant Pengajar
    participant Frontend
    participant Backend
    participant AIService
    participant Database

    Pengajar->>Frontend: Input parameter soal (topik, tipe, jumlah, tingkat kesulitan)
    Frontend->>Backend: POST /api/questions/generate
    Backend->>AIService: Request generate soal
    AIService-->>Backend: Response soal yang digenerate
    Backend->>Database: Simpan soal (status: pending_review)
    Database-->>Backend: Soal tersimpan
    Backend-->>Frontend: Soal berhasil digenerate
    Frontend-->>Pengajar: Tampilkan soal untuk review
    Pengajar->>Frontend: Review dan edit soal jika perlu
    Frontend->>Backend: PUT /api/questions/:id
    Backend->>Database: Update soal
    Database-->>Backend: Soal diupdate
    Backend-->>Frontend: Soal berhasil diupdate
    Frontend-->>Pengajar: Konfirmasi update
```

## 6. Sequence Diagram - Persetujuan Soal oleh Pengajar

```mermaid
sequenceDiagram
    participant Pengajar
    participant Frontend
    participant Backend
    participant Database

    Pengajar->>Frontend: Akses halaman review soal yang digenerate
    Frontend->>Backend: GET /api/questions (soal pending milik pengajar)
    Backend->>Database: Ambil soal pending review milik pengajar
    Database-->>Backend: Data soal pending
    Backend-->>Frontend: List soal pending
    Frontend-->>Pengajar: Tampilkan soal untuk review
    Pengajar->>Frontend: Review soal dan beri keputusan
    alt Menyetujui soal
        Frontend->>Backend: PUT /api/questions/:id/approve
        Backend->>Database: Update status soal menjadi approved
        Database-->>Backend: Status diupdate
        Backend-->>Frontend: Soal berhasil disetujui
        Frontend-->>Pengajar: Konfirmasi soal disetujui
    else Menolak/Edit soal
        Frontend->>Backend: PUT /api/questions/:id
        Backend->>Database: Update soal atau ubah status menjadi rejected
        Database-->>Backend: Soal diupdate/ditolak
        Backend-->>Frontend: Soal berhasil diupdate/ditolak
        Frontend-->>Pengajar: Konfirmasi perubahan
    end
```

## 7. Sequence Diagram - Pembuatan Kuis

```mermaid
sequenceDiagram
    participant Pengajar
    participant Frontend
    participant Backend
    participant Database

    Pengajar->>Frontend: Akses halaman buat kuis
    Frontend->>Backend: GET /api/questions (soal approved)
    Backend->>Database: Ambil soal yang disetujui
    Database-->>Backend: Data soal approved
    Backend-->>Frontend: List soal tersedia
    Frontend-->>Pengajar: Tampilkan soal untuk dipilih
    Pengajar->>Frontend: Pilih soal dan isi detail kuis
    Frontend->>Backend: POST /api/quizzes
    Backend->>Database: Simpan data kuis
    Database-->>Backend: Kuis tersimpan
    Backend->>Backend: Generate kode akses kuis
    Backend->>Database: Simpan kode akses
    Database-->>Backend: Kode akses tersimpan
    Backend-->>Frontend: Kuis berhasil dibuat + kode akses
    Frontend-->>Pengajar: Tampilkan kuis dan kode akses
```

## 8. Sequence Diagram - Pelajar Mengikuti Kuis

```mermaid
sequenceDiagram
    participant Pelajar
    participant Frontend
    participant Backend
    participant Database

    Pelajar->>Frontend: Input kode akses kuis
    Frontend->>Backend: POST /api/students/join-quiz
    Backend->>Database: Validasi kode akses dan waktu kuis
    alt Kode valid dan kuis aktif
        Database-->>Backend: Kuis tersedia
        Backend->>Database: Catat partisipasi Pelajar
        Database-->>Backend: Partisipasi tercatat
        Backend-->>Frontend: Join berhasil + data kuis
        Frontend-->>Pelajar: Tampilkan kuis
        loop Untuk setiap soal
            Pelajar->>Frontend: Pilih jawaban
            Frontend->>Frontend: Simpan jawaban sementara
        end
        Pelajar->>Frontend: Submit kuis
        Frontend->>Backend: POST /api/students/submit-answers
        Backend->>Database: Simpan jawaban dan hitung skor
        Database-->>Backend: Jawaban tersimpan + skor
        Backend-->>Frontend: Hasil kuis
        Frontend-->>Pelajar: Tampilkan hasil
    else Kode tidak valid atau kuis tidak aktif
        Database-->>Backend: Kuis tidak ditemukan/expired
        Backend-->>Frontend: Error kode tidak valid
        Frontend-->>Pelajar: Tampilkan pesan error
    end
```

## 9. Sequence Diagram - Melihat Hasil Kuis (Pengajar)

```mermaid
sequenceDiagram
    participant Pengajar
    participant Frontend
    participant Backend
    participant Database

    Pengajar->>Frontend: Akses halaman hasil kuis
    Frontend->>Backend: GET /api/quizzes (kuis milik Pengajar)
    Backend->>Database: Ambil kuis milik Pengajar
    Database-->>Backend: Data kuis Pengajar
    Backend-->>Frontend: List kuis
    Frontend-->>Pengajar: Tampilkan kuis
    Pengajar->>Frontend: Pilih kuis untuk melihat hasil
    Frontend->>Backend: GET /api/quizzes/:id/results
    Backend->>Database: Ambil hasil detail kuis
    Database-->>Backend: Data hasil lengkap
    Backend-->>Frontend: Hasil kuis detail
    Frontend-->>Pengajar: Tampilkan hasil (skor, partisipan, statistik)
    opt Export hasil
        Pengajar->>Frontend: Klik export hasil
        Frontend->>Backend: GET /api/quizzes/:id/export?format=csv
        Backend->>Database: Ambil data untuk export
        Database-->>Backend: Data export
        Backend-->>Frontend: File CSV
        Frontend-->>Pengajar: Download file hasil
    end
```

## 10. Sequence Diagram - Dashboard Admin & Statistik

```mermaid
sequenceDiagram
    participant Admin
    participant Frontend
    participant Backend
    participant Database

    Admin->>Frontend: Akses dashboard admin
    Frontend->>Backend: GET /api/admin/statistics
    Backend->>Database: Hitung statistik pengguna
    Database-->>Backend: Data jumlah pengguna per role
    Backend->>Database: Hitung statistik kuis
    Database-->>Backend: Data jumlah kuis aktif/selesai
    Backend->>Database: Hitung statistik soal
    Database-->>Backend: Data soal pending/approved/rejected
    Backend-->>Frontend: Data statistik lengkap
    Frontend-->>Admin: Tampilkan dashboard dengan grafik
    
    opt Melihat detail pengguna
        Admin->>Frontend: Klik menu kelola pengguna
        Frontend->>Backend: GET /api/admin/users?page=1&limit=10
        Backend->>Database: Ambil data pengguna dengan paginasi
        Database-->>Backend: Data pengguna
        Backend-->>Frontend: List pengguna
        Frontend-->>Admin: Tampilkan tabel pengguna
    end
    
    opt Melihat statistik soal
        Admin->>Frontend: Klik menu statistik soal
        Frontend->>Backend: GET /api/admin/question-statistics
        Backend->>Database: Ambil statistik soal per kategori
        Database-->>Backend: Data statistik soal
        Backend-->>Frontend: Statistik soal detail
        Frontend-->>Admin: Tampilkan grafik statistik soal
    end
```

---

**Keterangan Diagram:**
- Setiap sequence diagram menggambarkan interaksi antar komponen sistem
- Diagram menggunakan notasi standar UML sequence diagram
- Semua diagram dalam bahasa Indonesia sesuai permintaan
- Diagram mencakup flow utama dan alternatif flow (error handling)
- Menunjukkan komunikasi antara Frontend, Backend, Database, dan service eksternal
