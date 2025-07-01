# Diagram Aktivitas - ExamExpert-AI

## Daftar Isi
1. [Proses Pendaftaran dan Persetujuan Guru](#1-proses-pendaftaran-dan-persetujuan-guru)
2. [Proses Pembuatan dan Tinjauan Soal AI](#2-proses-pembuatan-dan-tinjauan-soal-ai)
3. [Proses Pembuatan dan Eksekusi Kuis](#3-proses-pembuatan-dan-eksekusi-kuis)
4. [Alur Autentikasi Pengguna](#4-alur-autentikasi-pengguna)
5. [Proses Pengelolaan Pengguna Admin](#5-proses-pengelolaan-pengguna-admin)
6. [Proses Statistik dan Analitik Soal](#6-proses-statistik-dan-analitik-soal)
7. [Proses Registrasi Pengguna (Perbandingan Siswa vs Guru)](#7-proses-registrasi-pengguna-perbandingan-siswa-vs-guru)
8. [Detail Aktivitas Upload dan Verifikasi Dokumen Guru](#8-detail-aktivitas-upload-dan-verifikasi-dokumen-guru)

---

## 1. Proses Pendaftaran dan Persetujuan Guru

```mermaid
flowchart TD
    A[Guru mengunjungi halaman pendaftaran] --> B[Isi formulir pendaftaran]
    B --> C[Unggah dokumen yang diperlukan]
    C --> D[Kirim pendaftaran]
    D --> E[Sistem validasi data]
    E --> F{Data valid?}
    
    F -->|Tidak| G[Tampilkan error validasi] --> B
    F -->|Ya| H[Buat record guru dengan status 'menunggu']
    H --> I[Kirim notifikasi ke admin]
    I --> J[Kirim email konfirmasi ke guru]
    J --> K[Guru menunggu persetujuan]
    
    K --> L[Admin meninjau aplikasi]
    L --> M[Admin melihat dokumen guru]
    M --> N{Keputusan admin}
    
    N -->|Setujui| O[Perbarui status menjadi 'aktif']
    N -->|Tolak| P[Perbarui status menjadi 'ditolak']
    
    O --> Q[Kirim email persetujuan ke guru]
    P --> R[Kirim email penolakan dengan alasan]
    
    Q --> S[Guru sekarang dapat mengakses fitur guru]
    R --> T[Guru dapat mendaftar ulang setelah memperbaiki masalah]
    
    style A fill:#e1f5fe
    style S fill:#c8e6c9
    style T fill:#ffcdd2
```

## 2. Proses Pembuatan dan Tinjauan Soal AI

```mermaid
flowchart TD
    A[Guru meminta pembuatan soal] --> B[Pilih topik dan kesulitan]
    B --> C[Atur jumlah dan jenis soal]
    C --> D[Kirim permintaan pembuatan]
    D --> E[Sistem panggil layanan AI]
    E --> F[AI membuat soal]
    F --> G[Simpan soal dengan status 'draft']
    G --> H[Tampilkan soal AI ke guru]
    H --> I[Guru meninjau soal yang dibuat AI]
    
    I --> J[Guru evaluasi kualitas soal]
    J --> K{Soal dapat diterima?}
    
    K -->|Ya| L[Guru setujui soal]
    K -->|Tidak| M[Guru tolak soal]
    K -->|Perlu Edit| N[Guru edit soal terlebih dahulu]
    
    L --> O[Tandai soal sebagai 'disetujui']
    M --> P[Hapus atau tandai soal ditolak]
    N --> Q[Simpan perubahan soal]
    
    O --> R[Soal tersedia untuk pembuatan kuis]
    P --> S[Guru perlu generate soal baru]
    Q --> T[Kembali ke evaluasi soal]
    
    T --> J
    R --> U[Guru dapat menggunakan dalam kuis]
    S --> A
    
    style A fill:#e1f5fe
    style U fill:#c8e6c9
    style S fill:#fff3e0
```

## 3. Proses Pembuatan dan Eksekusi Kuis

```mermaid
flowchart TD
    A[Guru membuat kuis baru] --> B[Atur detail kuis]
    B --> C[Pilih soal yang disetujui]
    C --> D[Konfigurasi pengaturan kuis]
    D --> E[Atur durasi waktu]
    E --> F[Atur tanggal mulai/selesai]
    F --> G[Buat kuis]
    G --> H[Buat kode akses]
    H --> I[Bagikan kode akses dengan siswa]
    
    I --> J[Siswa masukkan kode akses]
    J --> K{Kode valid & kuis aktif?}
    
    K -->|Tidak| L[Tampilkan pesan error]
    K -->|Ya| M[Muat soal kuis]
    
    M --> N[Siswa menjawab soal]
    N --> O[Siswa kirim jawaban]
    O --> P[Sistem hitung skor]
    P --> Q[Simpan hasil]
    Q --> R[Tampilkan hasil ke siswa]
    R --> S[Perbarui statistik kuis]
    
    S --> T[Guru dapat melihat semua hasil]
    T --> U[Buat laporan dan analitik]
    
    L --> V[Siswa coba lagi dengan kode yang benar]
    V --> J
    
    style A fill:#e1f5fe
    style R fill:#c8e6c9
    style L fill:#ffcdd2
```

## 4. Alur Autentikasi Pengguna

```mermaid
flowchart TD
    A[Pengguna mengunjungi halaman login] --> B[Masukkan kredensial]
    B --> C[Kirim formulir login]
    C --> D[Sistem validasi kredensial]
    D --> E{Kredensial valid?}
    
    E -->|Tidak| F[Tampilkan pesan error] --> B
    E -->|Ya| G{Cek status pengguna}
    
    G -->|Aktif| H[Buat JWT token]
    G -->|Menunggu| I[Tampilkan pesan menunggu persetujuan]
    G -->|Ditolak| J[Tampilkan pesan penolakan]
    G -->|Dihapus| K[Tampilkan pesan akun dinonaktifkan]
    
    H --> L[Atur sesi]
    L --> M{Peran pengguna?}
    
    M -->|Admin| N[Arahkan ke dashboard admin]
    M -->|Guru| O[Arahkan ke dashboard guru]
    M -->|Siswa| P[Arahkan ke dashboard siswa]
    
    I --> Q[Hubungi admin untuk status]
    J --> R[Daftar ulang atau hubungi support]
    K --> S[Hubungi admin untuk reaktivasi]
    
    style A fill:#e1f5fe
    style N fill:#c8e6c9
    style O fill:#c8e6c9
    style P fill:#c8e6c9
    style F fill:#ffcdd2
    style I fill:#fff3e0
    style J fill:#ffcdd2
    style K fill:#ffcdd2
```

## 5. Proses Pengelolaan Pengguna Admin

```mermaid
flowchart TD
    A[Admin akses pengelolaan pengguna] --> B[Lihat daftar pengguna]
    B --> C[Terapkan filter jika diperlukan]
    C --> D[Pilih aksi pengguna]
    D --> E{Jenis aksi?}
    
    E -->|Lihat Detail| F[Tampilkan profil pengguna]
    E -->|Edit Pengguna| G[Buka formulir edit]
    E -->|Hapus Pengguna| H[Konfirmasi penghapusan]
    E -->|Ubah Status| I[Pilih status baru]
    
    F --> J[Lihat statistik pengguna]
    G --> K[Perbarui informasi pengguna]
    H --> L{Konfirmasi hapus?}
    I --> M[Perbarui status pengguna]
    
    K --> N[Validasi perubahan]
    N --> O{Data valid?}
    O -->|Ya| P[Simpan perubahan]
    O -->|Tidak| Q[Tampilkan error validasi] --> G
    
    L -->|Ya| R[Hapus pengguna secara soft]
    L -->|Tidak| S[Batalkan penghapusan]
    
    M --> T[Kirim notifikasi perubahan status]
    P --> U[Kirim notifikasi perbaruan]
    R --> V[Kirim notifikasi penghapusan]
    
    T --> W[Perbaruan selesai]
    U --> W
    V --> W
    S --> W
    J --> W
    
    W --> X[Kembali ke daftar pengguna]
    
    style A fill:#e1f5fe
    style W fill:#c8e6c9
    style Q fill:#ffcdd2
```

## 6. Proses Statistik dan Analitik Soal

```mermaid
flowchart TD
    A[Guru/Admin meminta statistik] --> B[Pilih jenis laporan]
    B --> C{Ruang lingkup laporan?}
    
    C -->|Statistik Soal| D[Agregat data soal]
    C -->|Performa Kuis| E[Agregat hasil kuis]
    C -->|Analitik Pengguna| F[Agregat aktivitas pengguna]
    
    D --> G[Hitung metrik soal]
    E --> H[Hitung metrik performa]
    F --> I[Hitung engagement pengguna]
    
    G --> J[Soal berdasarkan topik/kesulitan]
    G --> K[Tingkat persetujuan soal oleh guru]
    G --> L[Frekuensi penggunaan soal]
    
    H --> M[Skor rata-rata per kuis]
    H --> N[Tingkat partisipasi siswa]
    H --> O[Analisis waktu]
    
    I --> P[Jumlah pengguna aktif]
    I --> Q[Tren pendaftaran]
    I --> R[Distribusi peran]
    
    J --> S[Buat visualisasi]
    K --> S
    L --> S
    M --> S
    N --> S
    O --> S
    P --> S
    Q --> S
    R --> S
    
    S --> T[Opsi ekspor]
    T --> U{Format ekspor?}
    
    U -->|CSV| V[Buat file CSV]
    U -->|PDF| W[Buat laporan PDF]
    U -->|Lihat Online| X[Tampilkan dashboard]
    
    V --> Y[Unduh file]
    W --> Y
    X --> Z[Grafik dan tabel interaktif]
    
    style A fill:#e1f5fe
    style Y fill:#c8e6c9
    style Z fill:#c8e6c9
```

## 7. Proses Registrasi Pengguna (Perbandingan Siswa vs Guru)

```mermaid
flowchart TD
    Start([Pengguna Baru Datang]) --> Choice{Pilih Jenis Akun}
    
    %% Alur Registrasi Siswa
    Choice -->|Siswa| S1[Klik 'Daftar sebagai Siswa']
    S1 --> S2[Isi Form Sederhana]
    S2 --> S3[Input: Nama Lengkap]
    S3 --> S4[Input: Email]
    S4 --> S5[Input: Password]
    S5 --> S6[Konfirmasi Password]
    S6 --> S7[Klik Submit]
    S7 --> S8[Validasi Format Email]
    S8 --> S9{Email Valid?}
    S9 -->|Tidak| S10[Tampilkan Error] --> S4
    S9 -->|Ya| S11[Validasi Password]
    S11 --> S12{Password Kuat?}
    S12 -->|Tidak| S13[Tampilkan Peringatan] --> S5
    S12 -->|Ya| S14[Simpan Data ke Database]
    S14 --> S15[Akun Langsung Aktif]
    S15 --> S16[Kirim Email Selamat Datang]
    S16 --> S17[Redirect ke Dashboard Siswa]
    S17 --> S18[✅ Mulai Ikut Kuis]
    
    %% Alur Registrasi Guru
    Choice -->|Guru| T1[Klik 'Daftar sebagai Guru']
    T1 --> T2[Isi Form Lengkap]
    T2 --> T3[Input: Data Pribadi]
    T3 --> T4[Input: Data Institusi]
    T4 --> T5[Upload Ijazah S1/S2]
    T5 --> T6[Upload Sertifikat Pendidik]
    T6 --> T7[Upload Surat Rekomendasi]
    T7 --> T8[Upload KTP/Identitas]
    T8 --> T9[Validasi Semua File]
    T9 --> T10{File Lengkap & Valid?}
    T10 -->|Tidak| T11[Tampilkan Error Upload] --> T5
    T10 -->|Ya| T12[Konfirmasi Semua Data]
    T12 --> T13[Klik Submit Pendaftaran]
    T13 --> T14[Simpan Data + File ke Server]
    T14 --> T15[Status: 'Menunggu Review']
    T15 --> T16[Kirim Notifikasi ke Admin]
    T16 --> T17[Kirim Email Konfirmasi ke Guru]
    T17 --> T18[⏳ Menunggu Review Admin]
    
    %% Proses Review Admin
    T18 --> A1[Admin Mendapat Notifikasi]
    A1 --> A2[Admin Buka Dashboard Review]
    A2 --> A3[Admin Lihat Data Guru]
    A3 --> A4[Admin Download/Cek Dokumen]
    A4 --> A5[Admin Verifikasi Kredensial]
    A5 --> A6{Keputusan Admin}
    
    A6 -->|Setujui| A7[Update Status: 'Disetujui']
    A6 -->|Tolak| A8[Update Status: 'Ditolak']
    A6 -->|Perlu Info Tambahan| A9[Minta Dokumen Tambahan]
    
    A7 --> A10[Kirim Email Persetujuan]
    A8 --> A11[Kirim Email Penolakan + Alasan]
    A9 --> A12[Kirim Email Permintaan] --> T5
    
    A10 --> A13[✅ Akun Guru Aktif]
    A11 --> A14[❌ Registrasi Gagal]
    A13 --> A15[Guru Dapat Akses Fitur Lengkap]
    A14 --> A16[Guru Dapat Daftar Ulang]
    
    %% Styling
    style Start fill:#e3f2fd
    style Choice fill:#fff3e0
    style S18 fill:#c8e6c9
    style A15 fill:#c8e6c9
    style A14 fill:#ffcdd2
    style A16 fill:#fff9c4
    
    %% Zona Siswa
    style S1 fill:#e8f5e8
    style S17 fill:#e8f5e8
    
    %% Zona Guru
    style T1 fill:#fff3e0
    style T18 fill:#fff3e0
    
    %% Zona Admin
    style A1 fill:#f3e5f5
    style A13 fill:#f3e5f5
```

## 8. Detail Aktivitas Upload dan Verifikasi Dokumen Guru

```mermaid
flowchart TD
    Start[Guru Mulai Upload Dokumen] --> Choose{Pilih Jenis Dokumen}
    
    %% Upload Ijazah
    Choose -->|Ijazah| I1[Pilih File Ijazah]
    I1 --> I2[Cek Format File]
    I2 --> I3{Format Valid?}
    I3 -->|Tidak| I4[Error: Format Tidak Didukung] --> I1
    I3 -->|Ya| I5[Cek Ukuran File]
    I5 --> I6{Ukuran < 5MB?}
    I6 -->|Tidak| I7[Error: File Terlalu Besar] --> I1
    I6 -->|Ya| I8[Upload ke Server]
    I8 --> I9[Generate Thumbnail]
    I9 --> I10[Simpan Path File]
    I10 --> I11[✅ Ijazah Terupload]
    
    %% Upload Sertifikat
    Choose -->|Sertifikat| C1[Pilih File Sertifikat]
    C1 --> C2[Validasi File] --> C3{Valid?}
    C3 -->|Tidak| C4[Tampilkan Error] --> C1
    C3 -->|Ya| C5[Upload & Simpan] --> C6[✅ Sertifikat Terupload]
    
    %% Upload Rekomendasi
    Choose -->|Surat Rekomendasi| R1[Pilih File Rekomendasi]
    R1 --> R2[Validasi File] --> R3{Valid?}
    R3 -->|Tidak| R4[Tampilkan Error] --> R1
    R3 -->|Ya| R5[Upload & Simpan] --> R6[✅ Rekomendasi Terupload]
    
    %% Upload KTP
    Choose -->|KTP/Identitas| K1[Pilih File KTP]
    K1 --> K2[Validasi File] --> K3{Valid?}
    K3 -->|Tidak| K4[Tampilkan Error] --> K1
    K3 -->|Ya| K5[Upload & Simpan] --> K6[✅ KTP Terupload]
    
    %% Cek Kelengkapan
    I11 --> Check[Cek Kelengkapan Dokumen]
    C6 --> Check
    R6 --> Check
    K6 --> Check
    
    Check --> Complete{Semua Dokumen Lengkap?}
    Complete -->|Tidak| Missing[Tampilkan Dokumen yang Kurang] --> Choose
    Complete -->|Ya| Submit[Enable Tombol Submit]
    Submit --> Final[Kirim Semua Data untuk Review]
    
    %% Proses Verifikasi Admin
    Final --> AdminNotif[Notifikasi ke Admin]
    AdminNotif --> AdminReview[Admin Mulai Review]
    AdminReview --> DownloadDocs[Admin Download Dokumen]
    DownloadDocs --> CheckAuth[Cek Keaslian Dokumen]
    CheckAuth --> CheckInstitute[Verifikasi Institusi]
    CheckInstitute --> AdminDecision{Keputusan Admin}
    
    AdminDecision -->|Approve| Approved[Status: Disetujui]
    AdminDecision -->|Reject| Rejected[Status: Ditolak]
    AdminDecision -->|Need More| NeedMore[Minta Dokumen Tambahan]
    
    Approved --> EmailApproval[Email Persetujuan]
    Rejected --> EmailRejection[Email Penolakan]
    NeedMore --> EmailRequest[Email Permintaan] --> Choose
    
    EmailApproval --> ActiveAccount[✅ Akun Aktif]
    EmailRejection --> InactiveAccount[❌ Akun Tidak Aktif]
    
    %% Styling
    style Start fill:#e3f2fd
    style ActiveAccount fill:#c8e6c9
    style InactiveAccount fill:#ffcdd2
    style I11 fill:#e8f5e8
    style C6 fill:#e8f5e8
    style R6 fill:#e8f5e8
    style K6 fill:#e8f5e8
```
