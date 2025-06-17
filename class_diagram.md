# Class Diagram - ExamExpert-AI

Diagram kelas berikut menggambarkan struktur database dan model data dalam sistem ExamExpert-AI.

```mermaid
classDiagram
    class User {
        +ObjectId _id
        +String name
        +String email
        +String password
        +String role [admin, teacher, student]
        +String status [pending, active, rejected, deleted]
        +Boolean isVerified
        +String verificationToken
        +Date createdAt
        +Date updatedAt
        +Object teacherInfo
        +Array participatedQuizzes
        +Array createdQuizzes
        +String profileImage
        +Date lastLogin
        +Date approvedAt
        +ObjectId approvedBy
        +String rejectionReason
        
        +validatePassword() Boolean
        +generateVerificationToken() String
        +toJSON() Object
    }

    class Question {
        +ObjectId _id
        +String content
        +String type [multiple_choice, true_false, essay]
        +String topic
        +String difficulty [easy, medium, hard]
        +Array options
        +String correctAnswer
        +String explanation
        +String status [pending_review, approved, rejected]
        +ObjectId createdBy
        +ObjectId reviewedBy
        +Date reviewedAt
        +String rejectionReason
        +Boolean aiGenerated
        +Array tags
        +Date createdAt
        +Date updatedAt
        
        +validateOptions() Boolean
        +calculateDifficulty() String
    }

    class Quiz {
        +ObjectId _id
        +String title
        +String description
        +String topic
        +Array questions
        +ObjectId createdBy
        +String accessCode
        +Number duration
        +Boolean isActive
        +Date startDate
        +Date endDate
        +Array participants
        +Date createdAt
        +Date updatedAt
        
        +generateAccessCode() String
        +calculateAverageScore() Number
        +getParticipationStats() Object
    }

    class Participant {
        +ObjectId student
        +Date joinedAt
        +Date completedAt
        +String status [joined, in_progress, completed]
        +Number score
        +Number correctAnswers
        +Number totalQuestions
        +Array answers
        +Array detailedResults
        +Number timeSpent
    }

    class Answer {
        +ObjectId questionId
        +String selectedAnswer
        +Boolean isCorrect
        +Date answeredAt
        +Number timeSpent
    }

    class DetailedResult {
        +ObjectId questionId
        +String questionContent
        +String studentAnswer
        +String correctAnswer
        +Boolean isCorrect
        +String explanation
    }

    class TeacherInfo {
        +String institution
        +String expertise
        +Number experience
        +String qualification
        +String phone
        +String address
        +Array documents
    }

    class Option {
        +String text
        +Boolean isCorrect
        +ObjectId _id
    }

    %% Relationships
    User ||--o{ Question : creates
    User ||--o{ Quiz : creates
    User ||--o{ Participant : participates
    Quiz ||--o{ Participant : has
    Quiz }o--o{ Question : contains
    Question ||--o{ Option : has
    Participant ||--o{ Answer : submits
    Participant ||--o{ DetailedResult : generates
    User ||--|| TeacherInfo : has
    Question ||--|| User : reviewedBy
    Quiz ||--|| User : createdBy
    Participant ||--|| User : student

    %% Notes
    note for User "Model utama untuk semua pengguna sistem\n- Admin: mengelola sistem\n- Teacher: membuat soal dan kuis\n- Student: mengikuti kuis"
    note for Question "Model untuk soal yang dibuat AI atau manual\nMemiliki sistem approval/rejection"
    note for Quiz "Model untuk kuis dengan access code\nMenyimpan hasil partisipasi siswa"
```

## Penjelasan Class Diagram

### 1. **User Class**
Kelas utama yang mewakili semua pengguna sistem dengan berbagai peran:
- **Admin**: Mengelola approval teacher, melihat statistik sistem
- **Teacher**: Membuat soal, kuis, dan mengelola pembelajaran
- **Student**: Mengikuti kuis dan melihat hasil

**Atribut Khusus:**
- `teacherInfo`: Informasi tambahan untuk teacher (institusi, keahlian, dokumen)
- `participatedQuizzes`: Riwayat kuis yang diikuti student
- `createdQuizzes`: Kuis yang dibuat oleh teacher

### 2. **Question Class**
Mewakili soal yang dapat dibuat secara manual atau menggunakan AI.

**Fitur Utama:**
- Support berbagai tipe soal (pilihan ganda, benar/salah, essay)
- Sistem approval/rejection untuk quality control
- Tag dan kategori untuk organisasi soal

### 3. **Quiz Class**
Mewakili kuis yang dibuat teacher dengan sistem access code untuk student.

**Fitur Utama:**
- Access code unik untuk setiap kuis
- Durasi dan periode aktif kuis
- Tracking partisipasi dan hasil student

### 4. **Participant Class**
Embedded document dalam Quiz yang menyimpan data partisipasi student.

**Tracking Data:**
- Status pengerjaan (joined, in_progress, completed)
- Skor dan jawaban detail
- Waktu pengerjaan

### 5. **Supporting Classes**
- **Answer**: Jawaban individual student untuk setiap soal
- **DetailedResult**: Hasil detail dengan penjelasan untuk feedback
- **TeacherInfo**: Informasi tambahan untuk registrasi teacher
- **Option**: Pilihan jawaban untuk soal multiple choice

## Relationships

### One-to-Many Relationships:
- **User → Question**: Satu user dapat membuat banyak soal
- **User → Quiz**: Satu teacher dapat membuat banyak kuis  
- **Quiz → Participant**: Satu kuis dapat memiliki banyak partisipan

### Many-to-Many Relationships:
- **Quiz ↔ Question**: Satu kuis dapat berisi banyak soal, satu soal dapat digunakan di banyak kuis

### One-to-One Relationships:
- **User ↔ TeacherInfo**: Satu teacher memiliki satu info tambahan

## Security Features

### 1. **Authentication & Authorization**
- JWT token-based authentication
- Role-based access control (RBAC)
- Password hashing dengan bcrypt

### 2. **Data Validation**
- Input validation di middleware level
- Schema validation di database level
- File upload validation untuk teacher documents

### 3. **Business Logic Protection**
- Teacher approval workflow
- Question review system
- Quiz access control dengan code

## Database Indexes

```javascript
// User indexes
{ email: 1 } // unique
{ role: 1, status: 1 }

// Question indexes  
{ createdBy: 1 }
{ status: 1 }
{ topic: 1, difficulty: 1 }

// Quiz indexes
{ accessCode: 1 } // unique
{ createdBy: 1 }
{ isActive: 1 }
```

Diagram kelas ini mencerminkan implementasi lengkap sistem ExamExpert-AI dengan fokus pada:
- **Skalabilitas**: Struktur yang dapat menangani banyak user dan data
- **Fleksibilitas**: Support berbagai tipe soal dan metode penilaian
- **Keamanan**: Sistem approval dan access control yang ketat
- **Tracking**: Monitoring lengkap aktivitas user dan performa sistem
