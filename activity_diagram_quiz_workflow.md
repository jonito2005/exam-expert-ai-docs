# Diagram Aktivitas Pembuatan dan Pengerjaan Kuis

Diagram aktivitas berikut menggambarkan proses pembuatan kuis oleh guru dan pengerjaan kuis oleh siswa dalam sistem ExamExpert-AI.

```mermaid
flowchart TD
    %% Pembuatan Kuis (Guru)
    Start([Mulai]) --> A1[Guru login ke sistem]
    A1 --> A2[Akses menu Pembuatan Kuis]
    A2 --> A3[Isi informasi kuis:\n- Judul\n- Deskripsi\n- Topik\n- Durasi]
    A3 --> A4[Pilih soal-soal dari bank soal]
    A4 --> A5[Atur pengaturan kuis:\n- Tanggal mulai/selesai\n- Status aktif]
    A5 --> A6[Simpan kuis]
    A6 --> A7[Sistem membuat kode akses unik]
    A7 --> A8[Guru membagikan kode akses kepada siswa]
    
    %% Pengerjaan Kuis (Siswa)
    B1[Siswa login ke sistem] --> B2[Akses menu Gabung Kuis]
    B2 --> B3[Masukkan kode akses kuis]
    B3 --> B4{Kode Valid?}
    B4 -->|Tidak| B5[Tampilkan pesan error]
    B5 --> B3
    B4 -->|Ya| B6[Siswa bergabung ke kuis]
    B6 --> B7{Kuis Aktif?}
    B7 -->|Tidak| B8[Tunggu sampai kuis aktif]
    B8 --> B7
    B7 -->|Ya| B9[Mulai kuis]
    B9 --> B10[Siswa menjawab soal-soal]
    B10 --> B11[Siswa mengirim jawaban]
    
    %% Penilaian dan Hasil
    B11 --> C1[Sistem menilai jawaban secara otomatis]
    C1 --> C2[Menyimpan hasil kuis]
    C2 --> C3[Tampilkan nilai kepada siswa]
    C3 --> C4[Guru melihat hasil kuis]
    C4 --> C5[Guru menganalisis performa siswa]
    C5 --> End([Selesai])
    
    %% Hubungkan alur
    A8 -.-> B1
    
    %% Styles
    classDef start fill:#66ff66,stroke:#009900,stroke-width:2px
    classDef end fill:#ff6666,stroke:#990000,stroke-width:2px
    classDef teacher fill:#ffcc99,stroke:#ff9933,stroke-width:1px
    classDef student fill:#b3e6ff,stroke:#0099cc,stroke-width:1px
    classDef system fill:#f5f5f5,stroke:#333333,stroke-width:1px
    classDef decision fill:#ffff99,stroke:#999900,stroke-width:1px
    
    %% Apply styles
    class Start,End start
    class A1,A2,A3,A4,A5,A8,C4,C5 teacher
    class B1,B2,B3,B5,B6,B8,B9,B10,B11,C3 student
    class A6,A7,C1,C2 system
    class B4,B7 decision
```

## Penjelasan Diagram Aktivitas Pembuatan dan Pengerjaan Kuis

### Pembuatan Kuis (Oleh Guru)
1. **Persiapan Kuis**:
   - Guru login ke sistem dan mengakses menu pembuatan kuis
   - Guru mengisi informasi dasar kuis seperti judul, deskripsi, topik, dan durasi
   - Guru memilih soal-soal dari bank soal yang telah disetujui sebelumnya

2. **Konfigurasi Kuis**:
   - Guru mengatur pengaturan kuis seperti tanggal mulai/selesai dan status aktif
   - Sistem menyimpan kuis dan membuat kode akses unik
   - Guru membagikan kode akses kepada siswa yang akan mengikuti kuis

### Pengerjaan Kuis (Oleh Siswa)
1. **Bergabung dengan Kuis**:
   - Siswa login ke sistem dan mengakses menu gabung kuis
   - Siswa memasukkan kode akses yang diberikan oleh guru
   - Sistem memvalidasi kode akses dan memeriksa status kuis

2. **Mengerjakan Kuis**:
   - Jika kuis aktif, siswa dapat langsung mulai mengerjakan
   - Jika belum aktif, siswa harus menunggu sampai kuis aktif
   - Siswa menjawab soal-soal dalam batas waktu yang ditentukan
   - Siswa mengirimkan jawaban setelah selesai

### Penilaian dan Analisis Hasil
1. **Penilaian Otomatis**:
   - Sistem menilai jawaban siswa secara otomatis untuk soal objektif
   - Sistem menyimpan hasil kuis di database
   - Sistem menampilkan nilai kepada siswa setelah kuis selesai

2. **Analisis oleh Guru**:
   - Guru dapat melihat hasil kuis dari semua siswa
   - Guru menganalisis performa siswa secara individu dan keseluruhan
   - Guru mendapatkan wawasan tentang pemahaman siswa terhadap materi
