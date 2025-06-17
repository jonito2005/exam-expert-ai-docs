# Activity Diagram - Sistem ExamExpert-AI

Dokumen ini berisi activity diagram lengkap untuk semua proses utama dalam sistem ExamExpert-AI.

## Daftar Isi

1. [Activity Diagram Registrasi dan Login](#1-activity-diagram-registrasi-dan-login)
2. [Activity Diagram Approval Teacher oleh Admin](#2-activity-diagram-approval-teacher-oleh-admin)
3. [Activity Diagram Pembuatan Soal dengan AI](#3-activity-diagram-pembuatan-soal-dengan-ai)
4. [Activity Diagram Review dan Approval Soal](#4-activity-diagram-review-dan-approval-soal)
5. [Activity Diagram Pembuatan Kuis](#5-activity-diagram-pembuatan-kuis)
6. [Activity Diagram Partisipasi Kuis oleh Student](#6-activity-diagram-partisipasi-kuis-oleh-student)
7. [Activity Diagram Melihat Hasil dan Statistik](#7-activity-diagram-melihat-hasil-dan-statistik)
8. [Activity Diagram Ekspor Hasil Kuis](#8-activity-diagram-ekspor-hasil-kuis)

---

## 1. Activity Diagram Registrasi dan Login

```mermaid
flowchart TD
    A[Pengguna mengakses sistem] --> B{Sudah punya akun?}
    B -->|Ya| C[Klik Login]
    B -->|Tidak| D[Klik Register]
    
    %% Login Flow
    C --> E[Input email dan password]
    E --> F[Sistem validasi credentials]
    F --> G{Credentials valid?}
    G -->|Ya| H{Role pengguna?}
    G -->|Tidak| I[Tampilkan error login]
    I --> E
    
    H -->|Admin| J[Dashboard Admin]
    H -->|Teacher| K{Status teacher?}
    H -->|Student| L[Dashboard Student]
    
    K -->|Active| M[Dashboard Teacher]
    K -->|Pending| N[Halaman status pending]
    K -->|Rejected| O[Halaman ditolak dengan alasan]
    
    %% Registration Flow
    D --> P{Role yang dipilih?}
    P -->|Student| Q[Form registrasi student]
    P -->|Teacher| R[Form registrasi teacher + dokumen]
    
    Q --> S[Input data basic]
    R --> T[Input data teacher + upload dokumen]
    
    S --> U[Sistem validasi data]
    T --> V[Sistem validasi data dan dokumen]
    
    U --> W{Data valid?}
    V --> X{Data dan dokumen valid?}
    
    W -->|Ya| Y[Buat akun student aktif]
    W -->|Tidak| Z[Tampilkan error validasi]
    X -->|Ya| AA[Buat akun teacher pending]
    X -->|Tidak| BB[Tampilkan error validasi]
    
    Z --> S
    BB --> T
    
    Y --> CC[Kirim email verifikasi]
    AA --> DD[Kirim email konfirmasi + notif admin]
    
    CC --> L
    DD --> EE[Halaman menunggu approval]
    
    J --> FF[End]
    L --> FF
    M --> FF
    N --> FF
    O --> FF
    EE --> FF
```

### Detail Aktivitas Registrasi dan Login

#### A. Proses Login
1. **Input Credentials**: Pengguna memasukkan email dan password
2. **Validasi**: Sistem memverifikasi credentials dengan database
3. **Role Check**: Sistem mengecek role dan status pengguna
4. **Redirect**: Pengguna diarahkan ke dashboard sesuai role dan status

#### B. Proses Registrasi Student
1. **Form Input**: Mengisi nama, email, password
2. **Validasi**: Sistem mengecek format email, kekuatan password
3. **Akun Aktif**: Student langsung dapat menggunakan sistem
4. **Email Verifikasi**: Opsional untuk verifikasi email

#### C. Proses Registrasi Teacher
1. **Form Lengkap**: Data personal + informasi institusi
2. **Upload Dokumen**: Sertifikat, CV, dokumen pendukung
3. **Status Pending**: Akun menunggu approval admin
4. **Notifikasi**: Email ke teacher dan notifikasi ke admin

---

## 2. Activity Diagram Approval Teacher oleh Admin

```mermaid
flowchart TD
    A[Admin login ke sistem] --> B[Akses menu Teacher Management]
    B --> C[Sistem tampilkan daftar pending teachers]
    C --> D[Admin pilih teacher untuk review]
    D --> E[Sistem tampilkan detail teacher]
    E --> F[Admin review dokumen dan info]
    
    F --> G{Keputusan admin?}
    G -->|Approve| H[Admin klik approve]
    G -->|Reject| I[Admin klik reject + input alasan]
    G -->|Perlu info tambahan| J[Admin request info tambahan]
    
    H --> K[Sistem update status teacher ke 'active']
    I --> L[Sistem update status teacher ke 'rejected']
    J --> M[Sistem kirim email request info]
    
    K --> N[Sistem kirim email approval ke teacher]
    L --> O[Sistem kirim email rejection ke teacher]
    M --> P[Teacher terima notifikasi]
    
    N --> Q[Teacher dapat akses dashboard]
    O --> R[Teacher lihat alasan penolakan]
    P --> S[Teacher lengkapi info tambahan]
    
    S --> T[Teacher submit info baru]
    T --> U[Sistem update status ke pending review]
    U --> C
    
    Q --> V[End]
    R --> W[Teacher dapat mendaftar ulang]
    W --> V
```

### Detail Aktivitas Approval Teacher

#### A. Review Process
1. **Akses Dashboard**: Admin melihat daftar teacher pending
2. **Detail Review**: Memeriksa dokumen, CV, dan informasi institusi
3. **Verifikasi**: Cross-check dengan institusi terkait (opsional)
4. **Keputusan**: Approve, reject, atau minta info tambahan

#### B. Approval Actions
1. **Approve**: Teacher dapat langsung menggunakan sistem
2. **Reject**: Teacher diberi alasan dan dapat mendaftar ulang
3. **Request Info**: Teacher diminta melengkapi data

#### C. Notification System
1. **Email Otomatis**: Dikirim untuk setiap perubahan status
2. **Dashboard Update**: Status realtime di dashboard teacher
3. **Admin Log**: Semua aksi admin tercatat untuk audit

---

## 3. Activity Diagram Pembuatan Soal dengan AI

```mermaid
flowchart TD
    A[Teacher login] --> B[Akses menu Question Generation]
    B --> C[Teacher input parameter soal]
    
    C --> D[Input topik]
    D --> E[Pilih tipe soal]
    E --> F[Set tingkat kesulitan]
    F --> G[Set jumlah soal]
    G --> H[Teacher submit request]
    
    H --> I[Sistem validasi input]
    I --> J{Input valid?}
    J -->|Tidak| K[Tampilkan error validasi]
    K --> C
    
    J -->|Ya| L[Sistem kirim request ke AI]
    L --> M[AI proses generate soal]
    M --> N{AI berhasil generate?}
    
    N -->|Tidak| O[Tampilkan error AI]
    O --> P[Saran gunakan mock data]
    P --> Q[Teacher pilih gunakan mock/retry]
    Q -->|Retry| L
    Q -->|Mock| R[Sistem generate mock questions]
    
    N -->|Ya| S[AI return generated questions]
    R --> T[Format soal ke database]
    S --> T
    
    T --> U[Sistem simpan soal dengan status 'pending_review']
    U --> V[Sistem tampilkan preview soal]
    V --> W[Teacher review soal yang dihasilkan]
    
    W --> X{Teacher puas dengan soal?}
    X -->|Tidak| Y[Teacher edit soal manual]
    X -->|Ya| Z[Teacher submit untuk review]
    
    Y --> AA[Sistem update soal]
    AA --> V
    
    Z --> BB[Sistem update timestamp review]
    BB --> CC[Kirim notifikasi ke reviewer]
    CC --> DD[Soal masuk antrian review]
    DD --> EE[End]
```

### Detail Aktivitas Pembuatan Soal dengan AI

#### A. Parameter Input
1. **Topik**: Mata pelajaran atau sub-topik spesifik
2. **Tipe Soal**: Multiple choice, true/false, atau essay
3. **Tingkat Kesulitan**: Easy, medium, hard
4. **Jumlah Soal**: 1-20 soal per request
5. **Konteks Tambahan**: Opsional untuk customization

#### B. AI Processing
1. **API Call**: Request ke service AI eksternal (Perplexity)
2. **Prompt Engineering**: Template prompt disesuaikan dengan parameter
3. **Response Parsing**: Extract soal dari response AI
4. **Quality Check**: Validasi format dan konten soal
5. **Fallback**: Mock data jika AI gagal

#### C. Quality Control
1. **Preview System**: Teacher dapat review sebelum submit
2. **Edit Capability**: Teacher dapat edit soal hasil AI
3. **Pending Status**: Soal menunggu approval sebelum dapat digunakan
4. **Review Queue**: Masuk antrian untuk review oleh teacher lain/admin

---

## 4. Activity Diagram Review dan Approval Soal

```mermaid
flowchart TD
    A[Teacher/Admin login] --> B[Akses menu Question Review]
    B --> C[Sistem tampilkan daftar pending questions]
    C --> D[Filter soal berdasarkan kriteria]
    D --> E[Teacher pilih soal untuk review]
    
    E --> F[Sistem tampilkan detail soal]
    F --> G[Reviewer analisis soal]
    G --> H[Check konten dan kualitas]
    H --> I[Check jawaban dan penjelasan]
    I --> J[Check tingkat kesulitan]
    
    J --> K{Kualitas soal memenuhi standar?}
    K -->|Ya| L[Reviewer klik Approve]
    K -->|Tidak| M[Reviewer klik Reject + input alasan]
    K -->|Perlu revisi| N[Reviewer beri feedback untuk perbaikan]
    
    L --> O[Sistem update status soal ke 'approved']
    M --> P[Sistem update status soal ke 'rejected']
    N --> Q[Sistem kirim feedback ke pembuat soal]
    
    O --> R[Soal dapat digunakan dalam kuis]
    P --> S[Soal tidak dapat digunakan]
    Q --> T[Pembuat soal terima notifikasi]
    
    T --> U[Pembuat soal edit dan resubmit]
    U --> V[Sistem update soal dan reset status ke pending]
    V --> C
    
    R --> W[Update statistik approval]
    S --> X[Update statistik rejection]
    W --> Y[End]
    X --> Y
    
    %% Bulk Actions
    C --> Z[Teacher pilih multiple soal]
    Z --> AA[Bulk approve/reject]
    AA --> BB[Sistem proses batch update]
    BB --> CC[Update status semua soal selected]
    CC --> DD[Kirim notifikasi batch]
    DD --> Y
```

### Detail Aktivitas Review dan Approval Soal

#### A. Review Criteria
1. **Konten Accuracy**: Kebenaran materi dan informasi
2. **Language Quality**: Tata bahasa dan kejelasan bahasa
3. **Difficulty Alignment**: Kesesuaian tingkat kesulitan
4. **Answer Validity**: Kebenaran kunci jawaban
5. **Educational Value**: Nilai edukasi dan pembelajaran

#### B. Review Actions
1. **Approve**: Soal langsung dapat digunakan dalam kuis
2. **Reject**: Soal ditolak dengan alasan spesifik
3. **Request Revision**: Feedback untuk perbaikan soal
4. **Bulk Operations**: Approve/reject multiple soal sekaligus

#### C. Feedback System
1. **Detailed Comments**: Reviewer dapat beri komentar spesifik
2. **Improvement Suggestions**: Saran perbaikan untuk pembuat soal
3. **Quality Scoring**: Optional scoring system untuk kualitas soal
4. **Revision Tracking**: History perubahan dan revisi soal

---

## 5. Activity Diagram Pembuatan Kuis

```mermaid
flowchart TD
    A[Teacher login] --> B[Akses menu Quiz Creation]
    B --> C[Teacher klik 'Buat Kuis Baru']
    C --> D[Input informasi dasar kuis]
    
    D --> E[Input judul kuis]
    E --> F[Input deskripsi]
    F --> G[Pilih topik]
    G --> H[Set durasi kuis]
    H --> I[Set tanggal mulai/berakhir]
    
    I --> J[Teacher pilih soal untuk kuis]
    J --> K[Sistem tampilkan daftar approved questions]
    K --> L[Filter soal berdasarkan topik/difficulty]
    L --> M[Teacher select soal yang diinginkan]
    
    M --> N{Jumlah soal mencukupi?}
    N -->|Tidak| O[Teacher tambah soal lagi]
    O --> K
    
    N -->|Ya| P[Teacher review kuis]
    P --> Q[Preview susunan soal]
    Q --> R{Teacher puas dengan kuis?}
    
    R -->|Tidak| S[Teacher edit kuis]
    S --> T{Edit apa?}
    T -->|Info kuis| D
    T -->|Soal| J
    
    R -->|Ya| U[Teacher submit kuis]
    U --> V[Sistem validasi kuis]
    V --> W{Validasi berhasil?}
    
    W -->|Tidak| X[Tampilkan error validasi]
    X --> S
    
    W -->|Ya| Y[Sistem simpan kuis]
    Y --> Z[Sistem generate access code]
    Z --> AA[Sistem set status kuis aktif]
    
    AA --> BB[Sistem tampilkan detail kuis + access code]
    BB --> CC[Teacher dapat share access code]
    CC --> DD[Teacher dapat kelola kuis]
    
    DD --> EE[Monitor partisipasi]
    EE --> FF[Lihat hasil realtime]
    FF --> GG[Export hasil]
    GG --> HH[End]
```

### Detail Aktivitas Pembuatan Kuis

#### A. Setup Kuis
1. **Basic Information**: Judul, deskripsi, topik
2. **Timing**: Durasi pengerjaan, periode aktif kuis
3. **Configuration**: Setting khusus (shuffle questions, show results, dll)
4. **Access Control**: Public atau private dengan access code

#### B. Question Selection
1. **Filtered Browse**: Cari soal berdasarkan topik, difficulty, type
2. **Preview Questions**: Lihat detail soal sebelum menambahkan
3. **Drag & Drop**: Atur urutan soal dalam kuis
4. **Question Pool**: Opsi random selection dari pool soal

#### C. Kuis Management
1. **Access Code**: Generate unique code untuk student access
2. **Status Control**: Aktifkan/non-aktifkan kuis
3. **Real-time Monitoring**: Lihat siapa saja yang sedang mengerjakan
4. **Result Access**: Instant access ke hasil dan statistik

---

## 6. Activity Diagram Partisipasi Kuis oleh Student

```mermaid
flowchart TD
    A[Student login] --> B[Akses menu Quiz]
    B --> C{Cara akses kuis?}
    C -->|Access Code| D[Input access code]
    C -->|Browse Available| E[Lihat daftar kuis tersedia]
    
    D --> F[Sistem validasi access code]
    E --> G[Student pilih kuis dari daftar]
    
    F --> H{Access code valid?}
    G --> I[Sistem check eligibility]
    
    H -->|Tidak| J[Tampilkan error invalid code]
    H -->|Ya| K[Sistem load kuis]
    I --> L{Student eligible?}
    
    J --> D
    L -->|Tidak| M[Tampilkan pesan 'already joined' atau 'not eligible']
    L -->|Ya| K
    
    K --> N[Sistem check status kuis]
    N --> O{Kuis masih aktif?}
    O -->|Tidak| P[Tampilkan pesan kuis tidak aktif]
    O -->|Ya| Q[Student join kuis]
    
    Q --> R[Sistem add student ke participants]
    R --> S[Sistem tampilkan instruksi kuis]
    S --> T[Student baca instruksi]
    T --> U[Student klik 'Mulai Kuis']
    
    U --> V[Sistem start timer]
    V --> W[Sistem tampilkan soal pertama]
    W --> X[Student baca soal]
    X --> Y[Student pilih jawaban]
    
    Y --> Z[Sistem simpan jawaban sementara]
    Z --> AA{Student ingin lanjut?}
    AA -->|Next| BB[Tampilkan soal berikutnya]
    AA -->|Previous| CC[Tampilkan soal sebelumnya]
    AA -->|Submit| DD[Student yakin submit?]
    
    BB --> W
    CC --> W
    
    DD --> EE{Konfirmasi submit?}
    EE -->|Tidak| AA
    EE -->|Ya| FF[Sistem stop timer]
    
    FF --> GG[Sistem hitung skor]
    GG --> HH[Sistem simpan hasil final]
    HH --> II[Sistem tampilkan hasil ke student]
    
    II --> JJ[Student lihat skor dan detail]
    JJ --> KK[Student dapat lihat pembahasan]
    KK --> LL[End]
    
    %% Timer habis
    V --> MM[Timer countdown]
    MM --> NN{Timer habis?}
    NN -->|Ya| OO[Sistem auto-submit]
    NN -->|Tidak| AA
    OO --> FF
    
    M --> LL
    P --> LL
```

### Detail Aktivitas Partisipasi Kuis

#### A. Access Methods
1. **Access Code**: Input 6-digit code yang dibagikan teacher
2. **Public Browse**: Lihat kuis public yang tersedia
3. **Direct Link**: Akses via link langsung dari teacher
4. **Scheduled Quiz**: Kuis yang dijadwalkan otomatis muncul

#### B. Quiz Execution
1. **Pre-Quiz**: Instruksi, rules, dan informasi durasi
2. **Navigation**: Previous/next question, question numbering
3. **Auto-Save**: Jawaban tersimpan otomatis setiap perubahan
4. **Timer Management**: Countdown timer dengan warning alerts
5. **Auto-Submit**: Otomatis submit saat waktu habis

#### C. Result Display
1. **Immediate Scoring**: Skor langsung tampil untuk objective questions
2. **Answer Review**: Lihat jawaban benar/salah dengan penjelasan
3. **Performance Stats**: Statistik waktu pengerjaan dan akurasi
4. **Ranking**: Posisi relatif terhadap participant lain (opsional)

---

## 7. Activity Diagram Melihat Hasil dan Statistik

```mermaid
flowchart TD
    A{User Role?} --> B[Admin]
    A --> C[Teacher]
    A --> D[Student]
    
    %% Admin Flow
    B --> E[Akses Dashboard Admin]
    E --> F[Lihat System Statistics]
    F --> G[Monitor user statistics]
    G --> H[Monitor question statistics]
    H --> I[Monitor quiz statistics]
    I --> J[Generate system reports]
    J --> K[Export system data]
    
    %% Teacher Flow
    C --> L[Akses Dashboard Teacher]
    L --> M[Pilih kuis untuk lihat hasil]
    M --> N[Sistem tampilkan overview hasil]
    N --> O[Lihat statistik partisipasi]
    O --> P[Analisis performa per soal]
    P --> Q[Lihat detail jawaban student]
    Q --> R[Identifikasi soal bermasalah]
    R --> S[Generate laporan hasil]
    S --> T[Export hasil kuis]
    
    %% Student Flow
    D --> U[Akses Dashboard Student]
    U --> V[Lihat quiz history]
    V --> W[Pilih kuis untuk detail]
    W --> X[Lihat skor dan ranking]
    X --> Y[Review jawaban dan pembahasan]
    Y --> Z[Lihat progress learning]
    
    %% Data Analysis
    K --> AA[Admin analisis trend]
    T --> BB[Teacher analisis class performance]
    Z --> CC[Student track progress]
    
    AA --> DD[End]
    BB --> DD
    CC --> DD
    
    %% Detailed Analytics
    F --> EE[Real-time dashboard]
    EE --> FF[User growth metrics]
    FF --> GG[Content quality metrics]
    GG --> HH[System performance metrics]
    
    N --> II[Participation rate]
    II --> JJ[Score distribution]
    JJ --> KK[Time analysis]
    KK --> LL[Question difficulty analysis]
    
    X --> MM[Individual performance]
    MM --> NN[Weak areas identification]
    NN --> OO[Improvement recommendations]
```

### Detail Aktivitas Melihat Hasil dan Statistik

#### A. Admin Analytics
1. **System Overview**: Total users, quizzes, questions
2. **User Growth**: Registration trends, activation rates
3. **Content Analytics**: Question approval rates, quiz creation
4. **Performance Metrics**: System response time, error rates
5. **Usage Patterns**: Peak hours, popular features

#### B. Teacher Analytics
1. **Quiz Performance**: Participation rate, completion rate
2. **Score Analysis**: Average scores, distribution, outliers
3. **Question Analytics**: Most difficult/easy questions
4. **Student Progress**: Individual and class progress tracking
5. **Time Analysis**: Average completion time, time per question

#### C. Student Analytics
1. **Personal Performance**: Scores, accuracy, improvement over time
2. **Subject Analysis**: Strength and weakness per topic
3. **Comparison**: Performance vs class average
4. **Learning Path**: Recommended areas for improvement
5. **Achievement**: Badges, milestones, progress tracking

---

## 8. Activity Diagram Ekspor Hasil Kuis

```mermaid
flowchart TD
    A[Teacher akses hasil kuis] --> B[Teacher klik menu Export]
    B --> C[Sistem tampilkan opsi export]
    C --> D[Teacher pilih format export]
    
    D --> E{Format yang dipilih?}
    E -->|CSV| F[Generate CSV file]
    E -->|PDF| G[Generate PDF report]
    E -->|Excel| H[Generate Excel file]
    
    F --> I[Sistem compile data kuis]
    G --> J[Sistem compile report data]
    H --> K[Sistem compile spreadsheet data]
    
    I --> L[Format data ke CSV]
    J --> M[Generate PDF dengan charts]
    K --> N[Format data ke Excel dengan sheets]
    
    L --> O[Sistem generate download link]
    M --> P[Sistem generate download link]
    N --> Q[Sistem generate download link]
    
    O --> R[Teacher download CSV file]
    P --> S[Teacher download PDF report]
    Q --> T[Teacher download Excel file]
    
    R --> U[Teacher buka file di spreadsheet app]
    S --> V[Teacher buka PDF untuk review]
    T --> W[Teacher buka Excel untuk analysis]
    
    U --> X[Data analysis dan reporting]
    V --> Y[Share report dengan stakeholder]
    W --> Z[Advanced data manipulation]
    
    X --> AA[End]
    Y --> AA
    Z --> AA
    
    %% Customization Options
    C --> BB[Teacher pilih data yang di-export]
    BB --> CC[Select columns/fields]
    CC --> DD[Set date range filter]
    DD --> EE[Choose student groups]
    EE --> D
    
    %% Error Handling
    F --> FF{Export berhasil?}
    G --> GG{Export berhasil?}
    H --> HH{Export berhasil?}
    
    FF -->|Tidak| II[Tampilkan error message]
    GG -->|Tidak| II
    HH -->|Tidak| II
    
    II --> JJ[Suggest alternative format]
    JJ --> D
    
    FF -->|Ya| O
    GG -->|Ya| P
    HH -->|Ya| Q
```

### Detail Aktivitas Ekspor Hasil Kuis

#### A. Export Options
1. **Format Selection**: CSV, PDF, Excel dengan template berbeda
2. **Data Customization**: Pilih kolom/field yang ingin di-export
3. **Filter Options**: Date range, student groups, score range
4. **Template Choice**: Summary report, detailed analysis, raw data

#### B. CSV Export
1. **Student Data**: Name, email, score, completion time
2. **Answer Details**: Per question response dan correctness
3. **Timestamps**: Join time, completion time, time per question
4. **Compatibility**: Format yang compatible dengan Excel, Google Sheets

#### C. PDF Report
1. **Executive Summary**: Overview statistik dan key metrics
2. **Visualizations**: Charts untuk score distribution, time analysis
3. **Detailed Results**: Table hasil per student
4. **Recommendations**: Analysis insights dan action items

#### D. Excel Export
1. **Multiple Sheets**: Summary, detailed results, raw data
2. **Formulas**: Pre-built formulas untuk analysis
3. **Charts**: Embedded charts dan pivot tables
4. **Formatting**: Professional formatting dengan conditional formatting

## Kesimpulan

Activity diagram di atas menggambarkan alur kerja lengkap sistem ExamExpert-AI yang mencakup:

1. **User Management**: Registrasi, login, dan approval workflow
2. **Content Creation**: AI-powered question generation dan review system
3. **Assessment Delivery**: Quiz creation dan student participation
4. **Analytics & Reporting**: Comprehensive analytics dan export capabilities

Setiap diagram dirancang untuk memberikan visibilitas yang jelas terhadap:
- **Decision Points**: Titik-titik keputusan dalam setiap proses
- **Error Handling**: Penanganan error dan alternative flows
- **User Experience**: Smooth user journey untuk semua role
- **Data Flow**: Bagaimana data mengalir antar sistem components

Implementasi yang sudah ada telah mengcover hampir semua activity yang digambarkan, dengan beberapa enhancement yang bisa ditambahkan untuk fitur advanced seperti PDF export dan real-time notifications.
