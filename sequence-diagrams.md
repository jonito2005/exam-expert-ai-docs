# Diagram Sequence - ExamExpert-AI

## 1. Alur Autentikasi Pengguna

```mermaid
sequenceDiagram
    participant U as Pengguna
    participant F as Frontend
    participant API as Backend API
    participant DB as Database
    participant Email as Layanan Email

    U->>F: Masukkan detail pendaftaran
    F->>API: POST /api/auth/register
    API->>DB: Buat record pengguna
    DB-->>API: Pengguna dibuat
    
    alt Pendaftaran Guru
        API->>Email: Kirim email verifikasi
        Email-->>U: Email verifikasi
        API-->>F: Pendaftaran menunggu persetujuan
    else Pendaftaran Siswa
        API-->>F: Pendaftaran berhasil
    end
    
    F-->>U: Tampilkan status pendaftaran

    Note over U,Email: Proses Login
    U->>F: Masukkan kredensial login
    F->>API: POST /api/auth/login
    API->>DB: Validasi kredensial
    DB-->>API: Data pengguna
    API-->>F: JWT Token + Info pengguna
    F-->>U: Login berhasil
```

## 2. Proses Persetujuan Guru

```mermaid
sequenceDiagram
    participant T as Guru
    participant F as Frontend
    participant API as Backend API
    participant DB as Database
    participant A as Admin
    participant Email as Layanan Email

    T->>F: Daftar sebagai guru dengan dokumen
    F->>API: POST /api/teachers/register (multipart/form-data)
    API->>DB: Simpan data guru + dokumen
    DB-->>API: Record guru dibuat (menunggu)
    API->>Email: Beritahu admin pendaftaran baru
    API-->>F: Pendaftaran dikirim
    F-->>T: Pesan menunggu persetujuan

    Note over A,Email: Proses Tinjauan Admin
    A->>F: Akses dashboard admin
    F->>API: GET /api/admin/pending-teachers
    API->>DB: Ambil guru yang menunggu
    DB-->>API: Daftar guru menunggu
    API-->>F: Data guru
    F-->>A: Tampilkan guru menunggu

    A->>F: Tinjau detail guru
    F->>API: GET /api/teachers/:id
    API->>DB: Ambil detail guru
    DB-->>API: Detail guru + dokumen
    API-->>F: Data guru
    F-->>A: Tampilkan profil guru

    alt Setujui Guru
        A->>F: Setujui guru
        F->>API: PUT /api/admin/approve-teacher/:id
        API->>DB: Perbarui status guru menjadi 'aktif'
        API->>Email: Kirim notifikasi persetujuan
        Email-->>T: Email persetujuan
    else Tolak Guru
        A->>F: Tolak dengan alasan
        F->>API: PUT /api/admin/reject-teacher/:id
        API->>DB: Perbarui status guru menjadi 'ditolak'
        API->>Email: Kirim notifikasi penolakan
        Email-->>T: Email penolakan dengan alasan
    end
```

## 3. Proses Pembuatan dan Tinjauan Soal

```mermaid
sequenceDiagram
    participant T as Guru
    participant F as Frontend
    participant API as Backend API
    participant AI as Layanan AI (Perplexity)
    participant DB as Database
    participant A as Admin

    T->>F: Minta pembuatan soal AI
    F->>API: POST /api/questions/generate
    API->>AI: Buat soal dengan topik/kesulitan
    AI-->>API: Soal yang dibuat
    API->>DB: Simpan soal (status: menunggu_tinjauan)
    DB-->>API: Soal disimpan
    API-->>F: Soal yang dibuat
    F-->>T: Tampilkan soal yang dibuat

    Note over A,DB: Proses Tinjauan Admin
    A->>F: Akses tinjauan soal
    F->>API: GET /api/questions/pending-review
    API->>DB: Ambil soal menunggu
    DB-->>API: Soal menunggu
    API-->>F: Data soal
    F-->>A: Tampilkan soal untuk ditinjau

    alt Setujui Soal
        A->>F: Setujui soal terpilih
        F->>API: POST /api/questions/approve-multiple
        API->>DB: Perbarui status soal menjadi 'disetujui'
        DB-->>API: Soal disetujui
        API-->>F: Respons berhasil
    else Tolak Soal
        A->>F: Tolak dengan alasan
        F->>API: PUT /api/questions/:id/reject
        API->>DB: Perbarui status soal menjadi 'ditolak'
        DB-->>API: Soal ditolak
        API-->>F: Respons berhasil
    end
```

## 4. Pembuatan dan Pengelolaan Kuis

```mermaid
sequenceDiagram
    participant T as Guru
    participant F as Frontend
    participant API as Backend API
    participant DB as Database

    T->>F: Buat kuis baru
    F->>API: GET /api/questions (soal yang disetujui)
    API->>DB: Ambil soal guru yang disetujui
    DB-->>API: Daftar soal
    API-->>F: Soal tersedia
    F-->>T: Tampilkan pilihan soal

    T->>F: Konfigurasi detail kuis
    F->>API: POST /api/quizzes
    API->>DB: Buat record kuis
    DB-->>API: Kuis dibuat
    API-->>F: Data kuis dengan ID
    F-->>T: Kuis berhasil dibuat

    T->>F: Buat kode akses
    F->>API: POST /api/quizzes/:id/generate-code
    API->>DB: Buat dan simpan kode akses
    DB-->>API: Kode akses
    API-->>F: Kode akses
    F-->>T: Tampilkan kode akses untuk siswa
```

## 5. Proses Siswa Mengerjakan Kuis

```mermaid
sequenceDiagram
    participant S as Siswa
    participant F as Frontend
    participant API as Backend API
    participant DB as Database
    participant T as Guru

    S->>F: Masukkan kode akses kuis
    F->>API: POST /api/students/join-quiz
    API->>DB: Validasi kode akses & ketersediaan kuis
    DB-->>API: Detail kuis
    API-->>F: Data kuis (tanpa jawaban)
    F-->>S: Tampilkan soal kuis

    S->>F: Jawab soal
    F->>API: POST /api/students/submit-answers
    API->>DB: Simpan jawaban siswa
    API->>DB: Hitung skor
    DB-->>API: Hasil dihitung
    API-->>F: Hasil kuis
    F-->>S: Tampilkan hasil kuis

    Note over T,DB: Guru dapat melihat hasil
    T->>F: Periksa hasil kuis
    F->>API: GET /api/quizzes/:id/results
    API->>DB: Ambil semua hasil siswa
    DB-->>API: Data hasil
    API-->>F: Hasil agregat
    F-->>T: Tampilkan performa siswa
```

## 6. Dashboard Admin dan Statistik

```mermaid
sequenceDiagram
    participant A as Admin
    participant F as Frontend
    participant API as Backend API
    participant DB as Database

    A->>F: Akses dashboard admin
    F->>API: GET /api/admin/statistics
    API->>DB: Agregat statistik sistem
    DB-->>API: Data statistik
    API-->>F: Metrik sistem
    F-->>A: Tampilkan dashboard

    A->>F: Lihat pengelolaan pengguna
    F->>API: GET /api/admin/users
    API->>DB: Ambil pengguna dengan filter
    DB-->>API: Daftar pengguna
    API-->>F: Data pengguna
    F-->>A: Tampilkan tabel pengguna

    A->>F: Lihat statistik soal
    F->>API: GET /api/admin/question-statistics
    API->>DB: Agregat metrik soal
    DB-->>API: Statistik soal
    API-->>F: Metrik soal
    F-->>A: Tampilkan analitik soal
```
