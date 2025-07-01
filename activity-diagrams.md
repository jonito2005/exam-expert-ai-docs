# Diagram Aktivitas - ExamExpert-AI

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
