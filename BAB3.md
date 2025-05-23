# BAB III
# METODOLOGI PENELITIAN DAN PERANCANGAN SISTEM

## 3.1 Pendekatan Penelitian

Penelitian ini menggunakan metodologi Design Science Research, yang berfokus pada pembuatan dan evaluasi artefak IT yang bertujuan untuk menyelesaikan masalah organisasi yang telah diidentifikasi. Pendekatan ini melibatkan beberapa fase iteratif:

1. **Identifikasi Masalah**: Memahami tantangan yang dihadapi oleh pendidik dalam membuat dan mengelola ujian.
2. **Perancangan Solusi**: Mengembangkan arsitektur sistem yang mengatasi tantangan tersebut melalui generasi soal berbasis AI dan distribusi ujian yang aman.
3. **Implementasi**: Membangun sistem ExamExpert-AI sesuai dengan arsitektur yang dirancang.
4. **Evaluasi**: Menguji efektivitas sistem dalam konteks pendidikan nyata.
5. **Iterasi**: Menyempurnakan sistem berdasarkan hasil evaluasi dan umpan balik pengguna.

Metode ini dipilih karena kemampuannya untuk mengatasi masalah dunia nyata melalui solusi inovatif, serta kemampuannya untuk beradaptasi dengan perubahan kebutuhan selama proses pengembangan.

## 3.2 Arsitektur Sistem

### 3.2.1 Arsitektur Keseluruhan

ExamExpert-AI mengikuti arsitektur tiga tingkat (three-tier architecture) modern:

1. **Lapisan Presentasi**: Antarmuka sisi klien untuk peran pengguna yang berbeda (admin, guru, siswa)
2. **Lapisan Aplikasi**: Logika sisi server yang diimplementasikan menggunakan Node.js dan Express
3. **Lapisan Data**: Database MongoDB untuk penyimpanan persisten

Sistem menggunakan desain API RESTful, dengan semua endpoint didokumentasikan menggunakan Swagger. Arsitektur ini memastikan skalabilitas, kemudahan pemeliharaan, dan potensi untuk pengembangan di masa depan.

![Diagram Arsitektur Sistem ExamExpert-AI](../assets/images/architecture_diagram.png)

### 3.2.2 Komponen Utama

Sistem terdiri dari beberapa komponen utama:

1. **Sistem Autentikasi**: Autentikasi berbasis JWT dengan kontrol akses berbasis peran
2. **Modul Generasi Soal**: Integrasi dengan Perplexity API untuk generasi soal berbasis AI
3. **Modul Manajemen Soal**: Alat untuk meninjau, menyetujui, dan mengorganisir soal
4. **Modul Pembuatan Kuis**: Fungsionalitas untuk menyusun soal menjadi penilaian komprehensif
5. **Modul Distribusi Kuis**: Mekanisme aman untuk berbagi kuis dengan siswa
6. **Modul Partisipasi Kuis**: Antarmuka bagi siswa untuk menyelesaikan kuis yang ditugaskan
7. **Modul Penilaian Otomatis**: Sistem untuk mengevaluasi soal objektif dan menghitung skor
8. **Modul Dokumentasi API**: Implementasi Swagger untuk dokumentasi endpoint yang komprehensif

![Diagram Komponen Sistem ExamExpert-AI](../assets/images/component_diagram.png)

## 3.3 Model Data

### 3.3.1 Model Pengguna

Model Pengguna merepresentasikan pengguna sistem dengan peran berbeda:

- **Properti**: nama, email, password (hashed), peran (admin, guru, siswa), informasi profil
- **Hubungan**: Kuis yang dibuat (untuk guru), kuis yang diikuti (untuk siswa)
- **Fitur Keamanan**: Hashing password, perizinan berbasis peran

```json
{
  "_id": "ObjectId",
  "name": "String",
  "email": "String",
  "password": "String (hashed)",
  "role": "String (admin, teacher, student)",
  "status": "String (pending, active, rejected)",
  "teacherInfo": {
    "institution": "String",
    "expertise": "String",
    "experience": "Number",
    "verificationDocuments": [
      {
        "documentType": "String",
        "documentUrl": "String",
        "uploadedAt": "Date",
        "description": "String"
      }
    ]
  },
  "profilePicture": "String",
  "createdQuizzes": ["ObjectId"],
  "participatedQuizzes": [
    {
      "quiz": "ObjectId",
      "score": "Number",
      "completedAt": "Date"
    }
  ],
  "isActive": "Boolean",
  "createdAt": "Date",
  "updatedAt": "Date"
}
```

### 3.3.2 Model Soal

Model Soal merepresentasikan item penilaian individual:

- **Properti**: konten, tipe (pilihan_ganda, benar_salah, esai), topik, kesulitan, opsi, jawaban benar, penjelasan
- **Metadata**: Pembuat, status persetujuan, flag generasi AI, timestamp pembuatan
- **Hubungan**: Terkait dengan kuis, dibuat oleh pengguna

```json
{
  "_id": "ObjectId",
  "content": "String",
  "type": "String (multiple_choice, true_false, essay)",
  "topic": "String",
  "difficulty": "String (easy, medium, hard)",
  "options": [
    {
      "text": "String",
      "isCorrect": "Boolean"
    }
  ],
  "correctAnswer": "String",
  "explanation": "String",
  "createdBy": "ObjectId",
  "isApproved": "Boolean",
  "aiGenerated": "Boolean",
  "tags": ["String"],
  "createdAt": "Date",
  "updatedAt": "Date"
}
```

### 3.3.3 Model Kuis

Model Kuis merepresentasikan kumpulan soal yang disusun menjadi penilaian:

- **Properti**: judul, deskripsi, topik, durasi, kode akses, status aktif, tanggal mulai/selesai
- **Hubungan**: Dibuat oleh guru, berisi soal, dikerjakan oleh siswa
- **Data Partisipasi**: Pengiriman siswa, skor, timestamp penyelesaian

```json
{
  "_id": "ObjectId",
  "title": "String",
  "description": "String",
  "topic": "String",
  "questions": ["ObjectId"],
  "createdBy": "ObjectId",
  "accessCode": "String",
  "duration": "Number",
  "isActive": "Boolean",
  "startDate": "Date",
  "endDate": "Date",
  "participants": [
    {
      "student": "ObjectId",
      "score": "Number",
      "submittedAt": "Date",
      "answers": [
        {
          "question": "ObjectId",
          "answer": "Mixed",
          "isCorrect": "Boolean",
          "score": "Number"
        }
      ]
    }
  ],
  "createdAt": "Date",
  "updatedAt": "Date"
}
```

## 3.4 Desain RESTful API

ExamExpert-AI menggunakan arsitektur RESTful API untuk komunikasi antara klien dan server. Endpoint API utama meliputi:

### 3.4.1 Endpoint Autentikasi

- `POST /api/auth/register`: Mendaftarkan pengguna baru
- `POST /api/auth/login`: Mengautentikasi pengguna dan mengeluarkan token JWT
- `GET /api/auth/me`: Mengambil informasi pengguna yang terautentikasi saat ini
- `POST /api/auth/logout`: Mencabut token JWT saat ini

### 3.4.2 Endpoint Pengguna

- `GET /api/users`: Mengambil daftar pengguna (admin)
- `GET /api/users/:id`: Mengambil pengguna berdasarkan ID
- `PUT /api/users/:id`: Memperbarui informasi pengguna
- `DELETE /api/users/:id`: Menghapus pengguna (admin)

### 3.4.3 Endpoint Guru

- `POST /api/teachers/register`: Mendaftarkan sebagai guru (memerlukan persetujuan admin)
- `GET /api/teachers/status`: Memeriksa status pendaftaran guru
- `GET /api/teachers/pending`: Mengambil semua pendaftaran guru yang tertunda (admin)
- `PUT /api/teachers/:id/approval`: Menyetujui atau menolak pendaftaran guru (admin)

### 3.4.4 Endpoint Soal

- `POST /api/questions/generate`: Menghasilkan soal menggunakan AI
- `POST /api/questions/approve`: Menyetujui soal untuk digunakan dalam kuis
- `GET /api/questions`: Mengambil soal yang dibuat oleh pengguna saat ini
- `PUT /api/questions/:id`: Memperbarui soal
- `DELETE /api/questions/:id`: Menghapus soal

### 3.4.5 Endpoint Kuis

- `POST /api/quizzes`: Membuat kuis baru
- `GET /api/quizzes`: Mengambil kuis yang dibuat oleh pengguna saat ini
- `GET /api/quizzes/:id`: Mengambil kuis berdasarkan ID
- `PUT /api/quizzes/:id`: Memperbarui kuis
- `DELETE /api/quizzes/:id`: Menghapus kuis
- `POST /api/quizzes/join`: Bergabung dengan kuis menggunakan kode akses
- `POST /api/quizzes/:id/submit`: Mengirimkan jawaban untuk kuis
- `GET /api/quizzes/:id/results`: Mengambil hasil kuis

## 3.5 Teknologi Implementasi

Implementasi ExamExpert-AI menggunakan teknologi berikut:

1. **Backend Framework**: Node.js dengan Express
   - Menyediakan runtime JavaScript sisi server yang cepat dan efisien
   - Express menawarkan framework web ringan untuk membangun API

2. **Database**: MongoDB dengan Mongoose ODM
   - Database NoSQL yang fleksibel dengan skema dinamis
   - Mongoose menyediakan layer abstraksi untuk operasi database

3. **Autentikasi**: JSON Web Tokens (JWT)
   - Mekanisme autentikasi stateless
   - Mendukung kontrol akses berbasis peran

4. **Integrasi AI**: Perplexity API
   - API model bahasa besar untuk generasi soal
   - Mendukung generasi teks kontekstual berkualitas tinggi

5. **Dokumentasi API**: Swagger.js
   - Dokumentasi API interaktif menggunakan swagger-jsdoc dan swagger-ui-express
   - Memfasilitasi pengujian dan integrasi endpoint

6. **Alat Pengembangan**:
   - Git untuk kontrol versi
   - Postman untuk pengujian API
   - Jest untuk pengujian unit dan integrasi

![Diagram Stack Teknologi ExamExpert-AI](../assets/images/tech_stack_diagram.png)

## 3.6 Rancangan Antarmuka Pengguna

### 3.6.1 Dashboard Admin

Dashboard Admin menyediakan antarmuka untuk mengelola pengguna, meninjau pendaftaran guru, dan melihat statistik sistem.

Fitur utama:
- Manajemen pengguna (daftar, detail, edit, hapus)
- Persetujuan pendaftaran guru
- Statistik penggunaan sistem
- Konfigurasi sistem

![Mockup Dashboard Admin](../assets/images/admin_dashboard_mockup.png)

### 3.6.2 Dashboard Guru

Dashboard Guru menyediakan antarmuka untuk membuat soal, mengelola kuis, dan melihat hasil siswa.

Fitur utama:
- Generasi soal AI
- Peninjauan dan persetujuan soal
- Pembuatan dan pengelolaan kuis
- Analisis performa siswa

![Mockup Dashboard Guru](../assets/images/teacher_dashboard_mockup.png)

### 3.6.3 Dashboard Siswa

Dashboard Siswa menyediakan antarmuka untuk bergabung dengan kuis, mengerjakan kuis, dan melihat hasil.

Fitur utama:
- Bergabung dengan kuis menggunakan kode akses
- Tampilan kuis yang sedang berlangsung
- Riwayat kuis dan hasil
- Profil dan pengaturan

![Mockup Dashboard Siswa](../assets/images/student_dashboard_mockup.png)

## 3.7 Metodologi Pengujian

Pendekatan pengujian untuk ExamExpert-AI meliputi:

1. **Pengujian Unit**: Menguji komponen dan fungsi individual
   - Pengujian fungsi kontroller
   - Validasi model dan schema
   - Verifikasi utilitas dan helpers

2. **Pengujian Integrasi**: Menguji interaksi antar komponen
   - Pengujian alur data end-to-end
   - Verifikasi komunikasi middleware
   - Validasi integrasi API eksternal

3. **Pengujian API**: Memvalidasi endpoint API menggunakan koleksi Postman
   - Verifikasi permintaan dan respons
   - Pengujian skenario sukses dan gagal
   - Validasi autentikasi dan otorisasi

4. **Pengujian Penerimaan Pengguna**: Evaluasi oleh pendidik dan siswa dalam konteks pendidikan nyata
   - Pengujian usability
   - Validasi alur kerja
   - Umpan balik pengguna akhir

## 3.8 Strategi Deployment

Strategi deployment untuk ExamExpert-AI melibatkan:

1. **Lingkungan Pengembangan**: Setup lokal untuk pengembangan dan pengujian awal
   - Server Node.js lokal
   - Database MongoDB lokal
   - Konfigurasi environment variables

2. **Lingkungan Staging**: Deployment berbasis cloud untuk pengujian integrasi
   - Platform cloud (misalnya Heroku, Vercel)
   - Database MongoDB Atlas
   - Integrasi dengan layanan cloud lainnya

3. **Lingkungan Produksi**: Deployment cloud yang dapat diskalakan dengan langkah-langkah keamanan yang tepat
   - Platform cloud dengan skalabilitas (misalnya AWS, Azure)
   - Konfigurasi load balancing
   - Backup dan pemulihan bencana

4. **Continuous Integration/Continuous Deployment**: Pipeline otomatis untuk pengujian dan deployment
   - GitHub Actions untuk CI/CD
   - Pengujian otomatis sebelum deployment
   - Rollback otomatis jika terjadi kegagalan

## 3.9 Metrik Evaluasi

Keberhasilan ExamExpert-AI akan dievaluasi berdasarkan metrik berikut:

1. **Kualitas Soal**: Penilaian soal yang dihasilkan AI oleh pakar mata pelajaran
   - Akurasi konten
   - Kepatuhan dengan standar pendidikan
   - Distribusi tingkat kesulitan

2. **Usabilitas Sistem**: Umpan balik dari pendidik dan siswa tentang antarmuka pengguna dan alur kerja
   - Skor System Usability Scale (SUS)
   - Tingkat kesuksesan tugas
   - Waktu penyelesaian tugas

3. **Efisiensi Waktu**: Pengukuran waktu yang dihemat dalam pembuatan ujian dan penilaian
   - Perbandingan dengan metode tradisional
   - Analisis ROI (Return on Investment)
   - Produktivitas pendidik

4. **Efektivitas Penilaian**: Analisis hasil ujian dan keselarasan dengan tujuan pembelajaran
   - Distribusi skor
   - Validitas diskriminatif soal
   - Korelasi dengan metrik kinerja lainnya

5. **Performa Sistem**: Metrik teknis seperti waktu respons, tingkat kesalahan, dan skalabilitas
   - Waktu respons API
   - Throughput sistem
   - Resource utilization

## 3.10 Pertimbangan Etis

Implementasi AI dalam penilaian pendidikan menimbulkan beberapa pertimbangan etis:

1. **Privasi Data**: Memastikan penanganan informasi siswa dan hasil ujian yang aman
   - Implementasi GDPR dan regulasi privasi lainnya
   - Enkripsi data sensitif
   - Kebijakan retensi data

2. **Transparansi AI**: Memberikan kejelasan tentang peran AI dalam generasi soal
   - Pengungkapan penggunaan AI kepada semua pemangku kepentingan
   - Dokumentasi metode AI yang digunakan
   - Proses tinjauan manusia

3. **Keadilan Pendidikan**: Memastikan sistem tidak merugikan kelompok siswa tertentu
   - Pengujian bias dalam soal yang dihasilkan
   - Aksesibilitas untuk siswa dengan kebutuhan khusus
   - Keadilan dalam metode penilaian

4. **Otonomi Pengajar**: Mempertahankan peran pendidik dalam desain dan evaluasi penilaian
   - Kontrol akhir oleh pendidik
   - Kemampuan untuk mengedit dan menyesuaikan soal
   - Keseimbangan antara otomatisasi dan penilaian manusia

5. **Integritas Akademik**: Mengimplementasikan langkah-langkah untuk mencegah kecurangan dan memastikan penilaian yang adil
   - Tindakan keamanan untuk konten ujian
   - Diversifikasi bank soal
   - Pelaporan dan analisis anomali

Pertimbangan ini akan diperhatikan sepanjang fase desain, implementasi, dan evaluasi proyek ini.

## 3.11 Jadwal Pelaksanaan

Pengembangan ExamExpert-AI direncanakan dalam jadwal 6 bulan sebagai berikut:

| Bulan | Aktivitas |
|-------|-----------|
| 1     | - Analisis kebutuhan<br>- Perancangan arsitektur<br>- Setup infrastruktur awal |
| 2     | - Pengembangan sistem autentikasi<br>- Implementasi model data<br>- Integrasi Perplexity API |
| 3     | - Pengembangan modul generasi soal<br>- Implementasi manajemen soal<br>- Pengembangan modul pembuatan kuis |
| 4     | - Pengembangan modul partisipasi kuis<br>- Implementasi penilaian otomatis<br>- Pengembangan dashboard admin |
| 5     | - Pengujian dan debugging<br>- Implementasi dokumentasi API<br>- Pengembangan UX/UI |
| 6     | - User acceptance testing<br>- Optimisasi performa<br>- Deployment produksi<br>- Dokumentasi final |

## 3.12 Ringkasan

BAB III telah menguraikan pendekatan metodologis untuk pengembangan ExamExpert-AI, termasuk arsitektur sistem, model data, desain API, teknologi implementasi, dan strategi pengujian. Penekanan diberikan pada penggunaan praktik terbaik dalam pengembangan perangkat lunak dan kepatuhan terhadap prinsip-prinsip pedagogis.

Sistem ini dirancang dengan mempertimbangkan kebutuhan semua pemangku kepentingan - admin, guru, dan siswa - dengan fokus pada usabilitas, skalabilitas, dan keamanan. Implementasi mengadopsi pendekatan berbasis API modern yang memfasilitasi pengembangan dan integrasi masa depan.

Dengan mengikuti metodologi yang diuraikan dalam bab ini, ExamExpert-AI diharapkan dapat memberikan solusi yang efektif dan efisien untuk tantangan pembuatan dan administrasi ujian dalam institusi pendidikan.
