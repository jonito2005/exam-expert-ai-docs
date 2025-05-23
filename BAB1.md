# BAB I
# PENDAHULUAN

## 1.1 Latar Belakang

Sektor pendidikan telah mengalami transformasi signifikan dengan integrasi teknologi dalam proses pembelajaran dan evaluasi. Metode tradisional dalam membuat soal ujian memerlukan waktu dan usaha yang besar dari para pendidik, seringkali menghasilkan soal yang repetitif dan cakupan penilaian yang terbatas. Dengan kemajuan kecerdasan buatan (Artificial Intelligence), khususnya model bahasa besar (Large Language Models atau LLMs), terbuka kesempatan untuk merevolusi cara pembuatan dan administrasi ujian pendidikan.

Dalam era digital saat ini, efisiensi dan efektivitas dalam proses belajar mengajar menjadi sangat penting. Guru dan dosen menghadapi tantangan dalam menyusun soal ujian yang berkualitas, bervariasi, dan sesuai dengan tingkat kemampuan siswa dalam waktu yang terbatas. Sementara itu, proses penilaian manual yang dilakukan oleh pengajar juga memakan waktu yang signifikan, terutama untuk kelas dengan jumlah siswa yang banyak.

ExamExpert-AI hadir untuk mengatasi tantangan tersebut dengan menyediakan sistem cerdas yang dapat secara otomatis menghasilkan soal ujian berkualitas tinggi dalam berbagai mata pelajaran dan tingkat kesulitan. Dengan memanfaatkan kemampuan Perplexity API, sistem ini dapat membuat berbagai jenis soal termasuk pilihan ganda, benar/salah, dan esai, sehingga mengurangi beban kerja pengajar sekaligus meningkatkan kualitas dan variasi soal ujian.

Implementasi sistem seperti ExamExpert-AI diharapkan dapat meningkatkan produktivitas pengajar, memberikan pengalaman belajar yang lebih baik bagi siswa, dan pada akhirnya meningkatkan kualitas pendidikan secara keseluruhan. Proyek ini merupakan langkah inovatif dalam mengintegrasikan teknologi AI ke dalam proses pendidikan, sejalan dengan tren pendidikan global yang mengarah pada personalisasi, efisiensi, dan pemanfaatan data untuk pengambilan keputusan yang lebih baik.

## 1.2 Rumusan Masalah

Berdasarkan latar belakang yang telah diuraikan, terdapat beberapa permasalahan yang dihadapi oleh pengajar dalam proses pembuatan dan pengelolaan ujian:

1. **Keterbatasan Waktu**: Pembuatan soal ujian yang komprehensif membutuhkan waktu yang banyak, mengurangi waktu yang seharusnya bisa digunakan untuk mengajar dan berinteraksi dengan siswa.

2. **Keberagaman Soal**: Menjaga keberagaman soal yang menguji berbagai tingkat kognitif merupakan tantangan tersendiri.

3. **Kualitas Penilaian**: Memastikan konsistensi kualitas dan tingkat kesulitan yang sesuai pada seluruh soal memerlukan keahlian dan pertimbangan yang cermat.

4. **Personalisasi**: Menyesuaikan ujian dengan tujuan pembelajaran tertentu dan kemampuan siswa seringkali sulit dilakukan dalam skala besar.

5. **Efisiensi Penilaian**: Penilaian manual, terutama untuk soal objektif, memakan waktu dan rentan terhadap kesalahan manusia.

## 1.3 Tujuan Penelitian

Tujuan utama dari pengembangan ExamExpert-AI adalah:

1. Mengembangkan sistem berbasis AI yang dapat menghasilkan soal ujian berkualitas tinggi dalam berbagai mata pelajaran dan tingkat kesulitan.

2. Menyediakan antarmuka yang user-friendly bagi pengajar untuk membuat, menyesuaikan, dan mengelola ujian.

3. Mengimplementasikan mekanisme penyaringan soal yang efisien sehingga pengajar dapat meninjau dan menyetujui soal yang dihasilkan oleh AI.

4. Membangun sistem distribusi ujian yang aman dengan kode akses unik untuk partisipasi siswa.

5. Mengintegrasikan kemampuan penilaian otomatis untuk soal objektif, mengurangi beban kerja penilaian bagi pengajar.

6. Menciptakan dokumentasi API yang komprehensif menggunakan Swagger untuk kemungkinan integrasi dan pengembangan di masa depan.

## 1.4 Batasan Masalah

Untuk memastikan proyek ExamExpert-AI tetap fokus dan dapat diselesaikan dalam waktu yang ditentukan, beberapa batasan masalah ditetapkan sebagai berikut:

1. Sistem hanya akan mendukung tiga jenis soal: pilihan ganda, benar/salah, dan esai.

2. Penilaian otomatis hanya tersedia untuk soal objektif (pilihan ganda dan benar/salah).

3. Soal esai akan dinilai secara manual oleh pengajar.

4. Sistem tidak menyediakan fitur untuk deteksi kecurangan selama ujian berlangsung.

5. Integrasi hanya dilakukan dengan Perplexity API, tidak dengan sistem AI lainnya.

6. Implementasi dilakukan sebagai aplikasi web dan tidak termasuk pengembangan aplikasi mobile.

7. Sistem dirancang untuk skala institusi pendidikan menengah dan tinggi, tidak dioptimalkan untuk penggunaan skala nasional.

## 1.5 Manfaat Penelitian

Pengembangan ExamExpert-AI diharapkan memberikan berbagai manfaat sebagai berikut:

### 1.5.1 Bagi Pengajar
- Mengurangi waktu dan usaha dalam pembuatan soal ujian berkualitas.
- Menyediakan akses ke berbagai jenis soal dengan tingkat kesulitan yang bervariasi.
- Memudahkan proses penilaian dengan fitur penilaian otomatis untuk soal objektif.
- Memberikan insight tentang performa siswa melalui analisis hasil ujian.

### 1.5.2 Bagi Siswa
- Mendapatkan pengalaman ujian yang lebih terstruktur dan adil.
- Menerima feedback yang lebih cepat melalui penilaian otomatis.
- Mengakses ujian secara fleksibel melalui platform digital.

### 1.5.3 Bagi Institusi Pendidikan
- Meningkatkan efisiensi dan standardisasi dalam proses ujian.
- Mengurangi biaya administratif terkait pencetakan dan distribusi ujian fisik.
- Meningkatkan kualitas pendidikan melalui penilaian yang lebih objektif dan komprehensif.
- Mendukung inisiatif digital transformation dalam institusi pendidikan.

## 1.6 Metodologi Penelitian

Penelitian dan pengembangan ExamExpert-AI menggunakan pendekatan metodologi Design Science Research, yang berfokus pada pembuatan dan evaluasi artefak IT untuk menyelesaikan masalah organisasi yang teridentifikasi. Pendekatan ini melibatkan beberapa fase iteratif:

1. **Identifikasi Masalah**: Memahami tantangan yang dihadapi pengajar dalam membuat dan mengelola ujian.

2. **Perancangan Solusi**: Mengembangkan arsitektur sistem yang mengatasi tantangan tersebut melalui generasi soal berbasis AI dan distribusi ujian yang aman.

3. **Implementasi**: Membangun sistem ExamExpert-AI sesuai dengan arsitektur yang dirancang.

4. **Evaluasi**: Menguji efektivitas sistem dalam konteks pendidikan nyata.

5. **Iterasi**: Menyempurnakan sistem berdasarkan hasil evaluasi dan umpan balik pengguna.

## 1.7 Sistematika Penulisan

Penulisan proposal ini disusun dengan sistematika sebagai berikut:

**BAB I PENDAHULUAN**  
Bab ini menjelaskan latar belakang masalah, rumusan masalah, tujuan penelitian, batasan masalah, manfaat penelitian, metodologi penelitian, dan sistematika penulisan.

**BAB II TINJAUAN PUSTAKA**  
Bab ini menguraikan landasan teori yang relevan dengan penelitian, termasuk konsep kecerdasan buatan dalam pendidikan, sistem ujian digital, model bahasa besar, dan kerangka kerja untuk pengembangan aplikasi web.

**BAB III METODOLOGI PENELITIAN**  
Bab ini menjelaskan metode penelitian yang digunakan, perancangan sistem, arsitektur sistem, model data, dan implementasi teknologi dalam pengembangan ExamExpert-AI.

**BAB IV IMPLEMENTASI DAN PENGUJIAN**  
Bab ini akan menjelaskan tentang implementasi sistem, hasil pengujian, dan analisis terhadap hasil yang diperoleh.

**BAB V PENUTUP**  
Bab ini berisi kesimpulan dari penelitian dan saran untuk pengembangan lebih lanjut.
