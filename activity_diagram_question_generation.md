# Diagram Aktivitas Pembuatan Soal AI

Diagram aktivitas berikut menggambarkan proses pembuatan soal menggunakan AI melalui Perplexity API dalam sistem ExamExpert-AI.

```mermaid
flowchart TD
    Start([Mulai]) --> A[Guru login ke sistem]
    A --> B[Akses menu Pembuatan Soal]
    B --> C[Isi form pembuatan soal:\n- Topik\n- Jenis soal\n- Tingkat kesulitan\n- Jumlah soal]
    C --> D{Validasi Input}
    D -->|Tidak Valid| C
    D -->|Valid| E[Kirim permintaan ke server]
    E --> F[Server menyiapkan prompt untuk Perplexity API]
    F --> G[Kirim permintaan ke Perplexity API]
    G --> H{Respons API Berhasil?}
    H -->|Tidak| I[Tampilkan pesan error]
    I --> J[Catat log error]
    J --> K[Tawarkan opsi mencoba kembali]
    K --> L{Coba Lagi?}
    L -->|Ya| E
    L -->|Tidak| End([Selesai])
    
    H -->|Ya| M[Proses respons API]
    M --> N[Parsing JSON hasil soal]
    N --> O[Simpan soal ke database]
    O --> P[Tampilkan soal ke guru]
    P --> Q[Guru meninjau soal]
    Q --> R{Setujui Soal?}
    R -->|Tidak| S[Edit soal jika diperlukan]
    S --> Q
    R -->|Ya| T[Tandai soal sebagai disetujui]
    T --> U[Soal tersedia untuk digunakan dalam kuis]
    U --> End

    classDef start fill:#66ff66,stroke:#009900,stroke-width:2px
    classDef end fill:#ff6666,stroke:#990000,stroke-width:2px
    classDef process fill:#f5f5f5,stroke:#333333,stroke-width:1px
    classDef decision fill:#ffff99,stroke:#999900,stroke-width:1px
    classDef api fill:#b3e6ff,stroke:#0099cc,stroke-width:1px

    class Start,End start
    class A,B,C,E,I,J,K,M,N,O,P,Q,S,T,U process
    class D,H,L,R decision
    class F,G api
```

## Penjelasan Diagram Aktivitas Pembuatan Soal AI

1. **Mulai Proses**: Guru memulai proses dengan login ke sistem.
2. **Persiapan Pembuatan Soal**:
   - Guru mengakses menu pembuatan soal
   - Guru mengisi form dengan informasi yang diperlukan (topik, jenis soal, tingkat kesulitan, jumlah soal)
   - Sistem memvalidasi input yang diberikan
3. **Proses Pembuatan Soal**:
   - Server menyiapkan prompt untuk Perplexity API
   - Server mengirim permintaan ke API dengan parameter yang sesuai
   - Sistem menangani respons dari API (berhasil atau gagal)
4. **Penanganan Kegagalan**:
   - Jika API gagal, sistem menampilkan pesan error
   - Sistem mencatat log error untuk debugging
   - Guru diberi opsi untuk mencoba kembali
5. **Pengolahan Hasil**:
   - Jika berhasil, sistem memproses respons API
   - Hasil JSON diubah menjadi struktur soal yang dapat disimpan
   - Soal disimpan ke database
6. **Peninjauan dan Persetujuan**:
   - Soal ditampilkan kepada guru untuk ditinjau
   - Guru dapat mengedit soal jika diperlukan
   - Guru menyetujui soal yang sudah final
7. **Finalisasi**:
   - Soal yang disetujui ditandai dan tersedia untuk digunakan dalam kuis
   - Proses pembuatan soal selesai
