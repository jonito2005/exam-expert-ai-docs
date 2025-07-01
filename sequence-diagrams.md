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
    
    alt Pendaftaran Pengajar
        API->>Email: Kirim email verifikasi
        Email-->>U: Email verifikasi
        API-->>F: Pendaftaran menunggu persetujuan
    else Pendaftaran Pelajar
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

## 2. Proses Persetujuan Pengajar

```mermaid
sequenceDiagram
    participant T as Pengajar
    participant F as Frontend
    participant API as Backend API
    participant DB as Database
    participant A as Admin
    participant Email as Layanan Email

    T->>F: Daftar sebagai Pengajar dengan dokumen
    F->>API: POST /api/teachers/register (multipart/form-data)
    API->>DB: Simpan data Pengajar + dokumen
    DB-->>API: Record Pengajar dibuat (menunggu)
    API->>Email: Beritahu admin pendaftaran baru
    API-->>F: Pendaftaran dikirim
    F-->>T: Pesan menunggu persetujuan

    Note over A,Email: Proses Tinjauan Admin
    A->>F: Akses dashboard admin
    F->>API: GET /api/admin/pending-teachers
    API->>DB: Ambil Pengajar yang menunggu
    DB-->>API: Daftar Pengajar menunggu
    API-->>F: Data Pengajar
    F-->>A: Tampilkan Pengajar menunggu

    A->>F: Tinjau detail Pengajar
    F->>API: GET /api/teachers/:id
    API->>DB: Ambil detail Pengajar
    DB-->>API: Detail Pengajar + dokumen
    API-->>F: Data Pengajar
    F-->>A: Tampilkan profil Pengajar

    alt Setujui Pengajar
        A->>F: Setujui Pengajar
        F->>API: PUT /api/admin/approve-teacher/:id
        API->>DB: Perbarui status Pengajar menjadi 'aktif'
        API->>Email: Kirim notifikasi persetujuan
        Email-->>T: Email persetujuan
    else Tolak Pengajar
        A->>F: Tolak dengan alasan
        F->>API: PUT /api/admin/reject-teacher/:id
        API->>DB: Perbarui status Pengajar menjadi 'ditolak'
        API->>Email: Kirim notifikasi penolakan
        Email-->>T: Email penolakan dengan alasan
    end
```

## 3. Proses Pembuatan dan Tinjauan Soal

```mermaid
sequenceDiagram
    participant T as Pengajar
    participant F as Frontend
    participant API as Backend API
    participant AI as Layanan AI (Perplexity)
    participant DB as Database

    T->>F: Minta pembuatan soal AI
    F->>API: POST /api/questions/generate
    API->>AI: Buat soal dengan topik/kesulitan
    AI-->>API: Soal yang dibuat AI
    API->>DB: Simpan soal (status: draft)
    DB-->>API: Soal disimpan
    API-->>F: Soal yang dibuat AI
    F-->>T: Tampilkan soal untuk ditinjau

    Note over T,F: Pengajar meninjau soal buatannya sendiri
    T->>F: Tinjau kualitas soal AI
    T->>F: Edit soal jika diperlukan
    
    alt Setujui Soal
        T->>F: Setujui soal
        F->>API: PUT /api/questions/:id/approve
        API->>DB: Perbarui status soal menjadi 'disetujui'
        DB-->>API: Soal disetujui
        API-->>F: Respons berhasil
        F-->>T: Soal tersedia untuk kuis
    else Tolak Soal
        T->>F: Tolak soal
        F->>API: PUT /api/questions/:id/reject
        API->>DB: Hapus atau tandai soal ditolak
        DB-->>API: Soal ditolak
        API-->>F: Respons berhasil
        F-->>T: Soal tidak tersedia, perlu generate ulang
    end
```

## 4. Pembuatan dan Pengelolaan Kuis

```mermaid
sequenceDiagram
    participant T as Pengajar
    participant F as Frontend
    participant API as Backend API
    participant DB as Database

    T->>F: Buat kuis baru
    F->>API: GET /api/questions (soal yang disetujui)
    API->>DB: Ambil soal Pengajar yang disetujui
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
    F-->>T: Tampilkan kode akses untuk Pelajar
```

## 5. Proses Pelajar Mengerjakan Kuis

```mermaid
sequenceDiagram
    participant S as Pelajar
    participant F as Frontend
    participant API as Backend API
    participant DB as Database
    participant T as Pengajar

    S->>F: Masukkan kode akses kuis
    F->>API: POST /api/students/join-quiz
    API->>DB: Validasi kode akses & ketersediaan kuis
    DB-->>API: Detail kuis
    API-->>F: Data kuis (tanpa jawaban)
    F-->>S: Tampilkan soal kuis

    S->>F: Jawab soal
    F->>API: POST /api/students/submit-answers
    API->>DB: Simpan jawaban Pelajar
    API->>DB: Hitung skor
    DB-->>API: Hasil dihitung
    API-->>F: Hasil kuis
    F-->>S: Tampilkan hasil kuis

    Note over T,DB: Pengajar dapat melihat hasil
    T->>F: Periksa hasil kuis
    F->>API: GET /api/quizzes/:id/results
    API->>DB: Ambil semua hasil Pelajar
    DB-->>API: Data hasil
    API-->>F: Hasil agregat
    F-->>T: Tampilkan performa Pelajar
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

    A->>F: Lihat Pengajar menunggu persetujuan
    F->>API: GET /api/admin/pending-teachers
    API->>DB: Ambil Pengajar menunggu
    DB-->>API: Data Pengajar menunggu
    API-->>F: Data Pengajar
    F-->>A: Tampilkan daftar Pengajar menunggu
```
