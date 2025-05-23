# Diagram Aktivitas Autentikasi

Diagram aktivitas berikut menggambarkan proses autentikasi pengguna dalam sistem ExamExpert-AI, termasuk registrasi, login, dan verifikasi token.

```mermaid
flowchart TD
    Start([Mulai]) --> A{Pengguna Terdaftar?}
    A -->|Tidak| B1[Akses Halaman Registrasi]
    A -->|Ya| C1[Akses Halaman Login]
    
    %% Alur Registrasi
    B1 --> B2[Isi Formulir Registrasi:\n- Nama\n- Email\n- Password\n- Role]
    B2 --> B3[Kirim Formulir]
    B3 --> B4{Validasi Data}
    B4 -->|Tidak Valid| B5[Tampilkan Pesan Error]
    B5 --> B2
    B4 -->|Valid| B6[Enkripsi Password]
    B6 --> B7[Buat Pengguna Baru di Database]
    B7 --> B8[Buat JWT Token]
    B8 --> B9[Kirim Respons Sukses dengan Token]
    B9 --> D1[Simpan Token di Client]
    
    %% Alur Login
    C1 --> C2[Isi Kredensial:\n- Email\n- Password]
    C2 --> C3[Kirim Kredensial]
    C3 --> C4{Validasi Kredensial}
    C4 -->|Tidak Valid| C5[Tampilkan Pesan Error]
    C5 --> C2
    C4 -->|Valid| C6[Buat JWT Token]
    C6 --> C7[Kirim Respons Sukses dengan Token]
    C7 --> D1
    
    %% Alur Akses API
    D1 --> D2[Akses API dengan Token]
    D2 --> D3[Server Menerima Request]
    D3 --> D4[Middleware Auth Memeriksa Token]
    D4 --> D5{Token Valid?}
    D5 -->|Tidak| D6[Kirim Error 401 Unauthorized]
    D6 --> End1([Selesai - Akses Ditolak])
    D5 -->|Ya| D7[Ekstrak Data Pengguna dari Token]
    D7 --> D8[Periksa Role dan Izin]
    D8 --> D9{Izin Cukup?}
    D9 -->|Tidak| D10[Kirim Error 403 Forbidden]
    D10 --> End1
    D9 -->|Ya| D11[Proses Request]
    D11 --> D12[Kirim Respons]
    D12 --> End2([Selesai - Akses Diberikan])
    
    %% Styles
    classDef start fill:#66ff66,stroke:#009900,stroke-width:2px
    classDef end fill:#ff6666,stroke:#990000,stroke-width:2px
    classDef process fill:#f5f5f5,stroke:#333333,stroke-width:1px
    classDef decision fill:#ffff99,stroke:#999900,stroke-width:1px
    classDef auth fill:#b3e6ff,stroke:#0099cc,stroke-width:1px
    
    %% Apply styles
    class Start start
    class End1,End2 end
    class B1,B2,B3,B5,B6,B7,B8,B9,C1,C2,C3,C5,C6,C7,D1,D2,D3,D6,D7,D8,D10,D11,D12 process
    class A,B4,C4,D5,D9 decision
    class D4 auth
```

## Penjelasan Diagram Aktivitas Autentikasi

### 1. Registrasi Pengguna
1. **Mulai Proses**: Pengguna yang belum terdaftar mengakses halaman registrasi.
2. **Pengisian Data**:
   - Pengguna mengisi formulir registrasi dengan nama, email, password, dan pemilihan role.
   - Sistem memvalidasi data yang dimasukkan.
3. **Pemrosesan Registrasi**:
   - Jika data tidak valid, sistem menampilkan pesan error.
   - Jika data valid, sistem mengenkripsi password untuk keamanan.
   - Sistem membuat pengguna baru di database.
4. **Autentikasi Awal**:
   - Sistem membuat JWT token untuk pengguna baru.
   - Sistem mengirimkan respons sukses dengan token.

### 2. Login Pengguna
1. **Akses Login**: Pengguna yang sudah terdaftar mengakses halaman login.
2. **Verifikasi Identitas**:
   - Pengguna memasukkan email dan password.
   - Sistem memvalidasi kredensial yang dimasukkan.
3. **Proses Login**:
   - Jika kredensial tidak valid, sistem menampilkan pesan error.
   - Jika kredensial valid, sistem membuat JWT token.
   - Sistem mengirimkan respons sukses dengan token.

### 3. Akses API dengan Autentikasi
1. **Penggunaan Token**:
   - Client menyimpan token yang diterima.
   - Client menggunakan token saat mengakses API.
2. **Verifikasi Token**:
   - Server menerima request dengan token.
   - Middleware autentikasi memeriksa validitas token.
3. **Otorisasi**:
   - Jika token tidak valid, server mengirim error 401 Unauthorized.
   - Jika token valid, server mengekstrak data pengguna dari token.
   - Server memeriksa role dan izin pengguna untuk endpoint yang diminta.
4. **Respons Final**:
   - Jika izin tidak cukup, server mengirim error 403 Forbidden.
   - Jika izin cukup, server memproses request dan mengirim respons.

Diagram ini menunjukkan bagaimana sistem ExamExpert-AI menangani autentikasi dan otorisasi pengguna dengan aman menggunakan JWT token dan middleware autentikasi.
