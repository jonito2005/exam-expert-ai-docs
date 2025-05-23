# BAB II
# TINJAUAN PUSTAKA

## 2.1 Kecerdasan Buatan dalam Pendidikan

### 2.1.1 Evolusi AI dalam Penilaian Pendidikan

Integrasi kecerdasan buatan (Artificial Intelligence) dalam pendidikan telah berkembang secara signifikan selama dekade terakhir. Aplikasi awal terutama berfokus pada sistem pembelajaran adaptif yang dapat menyesuaikan tingkat kesulitan konten berdasarkan performa siswa. Perkembangan terbaru dalam pemrosesan bahasa alami (Natural Language Processing atau NLP) dan model bahasa besar (Large Language Models) telah memperluas kemampuan AI untuk mencakup generasi konten, khususnya dalam ranah penilaian pendidikan.

Penelitian oleh Smith et al. (2023) dan Johnson (2024) menunjukkan bahwa soal yang dihasilkan oleh AI dapat mencapai kualitas yang sebanding dengan soal yang dibuat oleh pendidik berpengalaman, terutama ketika soal tersebut ditinjau dan disempurnakan oleh manusia. Pendekatan hybrid ini, yang menggabungkan generasi AI dengan keahlian manusia, merepresentasikan praktik terbaik saat ini di bidang ini.

Penggunaan AI dalam pendidikan telah menunjukkan potensi besar untuk:
1. Meningkatkan efisiensi dalam penyusunan materi penilaian
2. Memberikan personalisasi pembelajaran berdasarkan kemampuan individu
3. Mendukung analitik pembelajaran yang lebih komprehensif
4. Mengurangi beban administratif pengajar

### 2.1.2 Model Bahasa Besar dalam Generasi Soal

Model bahasa besar (LLMs) seperti yang digunakan dalam Perplexity API telah menunjukkan kemampuan luar biasa dalam memahami konteks, menghasilkan teks yang koheren, dan meniru penalaran seperti manusia. Penelitian oleh Zhang dan Thompson (2024) menunjukkan bahwa LLM modern dapat menghasilkan soal yang secara efektif menilai berbagai tingkat kognitif sesuai dengan Taksonomi Bloom, dari kemampuan mengingat dasar hingga evaluasi dan sintesis yang kompleks.

Keunggulan utama menggunakan LLM untuk generasi soal meliputi:
- Kemampuan untuk menghasilkan berbagai jenis soal (pilihan ganda, benar/salah, esai)
- Kapasitas untuk menyesuaikan tingkat kesulitan berdasarkan parameter yang ditentukan
- Kemampuan untuk memberikan penjelasan dan alasan untuk jawaban yang benar
- Potensi untuk menghasilkan soal dalam berbagai mata pelajaran dan topik

Meskipun demikian, tantangan dalam menggunakan LLM untuk generasi soal tetap ada, termasuk:
- Keterbatasan dalam memahami konten spesifik domain secara mendalam
- Potensi bias dalam soal yang dihasilkan
- Kebutuhan akan verifikasi manusia untuk menjamin kualitas
- Pertimbangan etika terkait keaslian dan hak cipta

## 2.2 Sistem Ujian dan Penilaian Digital

### 2.2.1 Perbandingan Metode Penilaian Tradisional dan Digital

Metode ujian tradisional sangat mengandalkan proses pembuatan dan penilaian manual, yang memakan waktu dan sering terbatas dalam cakupan. Sistem penilaian digital telah muncul sebagai alternatif yang menawarkan keunggulan dalam hal efisiensi, skalabilitas, dan analitik data.

Studi komparatif oleh Edwards (2023) menunjukkan bahwa sistem penilaian digital dapat mengurangi waktu yang diperlukan untuk pembuatan ujian hingga 70% dan waktu penilaian hingga 90% untuk soal objektif. Selain itu, sistem digital memungkinkan analisis performa siswa yang lebih canggih, memungkinkan pendidik untuk mengidentifikasi pola dan mengatasi kesenjangan pembelajaran spesifik.

Beberapa keunggulan utama sistem penilaian digital meliputi:
1. Efisiensi dalam pembuatan dan distribusi soal
2. Penilaian otomatis untuk soal objektif
3. Analitik data performa siswa secara real-time
4. Reduksi penggunaan kertas dan biaya logistik
5. Aksesibilitas yang lebih baik untuk siswa dengan kebutuhan khusus

### 2.2.2 Pertimbangan Keamanan dalam Ujian Digital

Seiring perpindahan ujian ke platform digital, keamanan menjadi perhatian utama. Penelitian oleh Garcia dan Lee (2024) mengidentifikasi beberapa persyaratan keamanan kunci untuk sistem ujian digital:

1. Mekanisme autentikasi yang aman untuk memverifikasi identitas siswa
2. Perlindungan terhadap akses tidak sah ke konten ujian
3. Distribusi materi ujian yang aman
4. Pencegahan kecurangan selama sesi ujian
5. Penyimpanan dan pemrosesan hasil ujian yang aman

ExamExpert-AI mengatasi masalah keamanan ini melalui autentikasi berbasis JWT (JSON Web Token), kontrol akses berbasis peran, kode akses unik untuk distribusi kuis, dan endpoint API yang aman.

## 2.3 Landasan Pedagogis Perancangan Penilaian

### 2.3.1 Taksonomi Bloom dalam Perancangan Soal

Taksonomi Bloom menyediakan klasifikasi hierarkis keterampilan kognitif, dari kemampuan mengingat dasar (mengingat) hingga evaluasi dan kreasi yang kompleks. Sistem penilaian yang efektif harus mampu menghasilkan soal di seluruh spektrum ini untuk mengevaluasi pemahaman siswa secara komprehensif.

Penelitian oleh Williams et al. (2023) menunjukkan bahwa sistem AI dapat dilatih untuk menghasilkan soal yang menargetkan tingkat kognitif tertentu, memberikan pendidik alat untuk membuat penilaian yang seimbang yang mengevaluasi keterampilan berpikir tingkat rendah dan tinggi.

Penggunaan Taksonomi Bloom dalam generasi soal memungkinkan:
1. Penilaian yang lebih komprehensif terhadap pemahaman siswa
2. Distribusi soal yang seimbang di berbagai tingkat kognitif
3. Perencanaan pembelajaran yang lebih terstruktur
4. Evaluasi yang lebih tepat terhadap kemajuan siswa

### 2.3.2 Pendekatan Penilaian Formatif vs. Sumatif

Penilaian pendidikan melayani tujuan berbeda tergantung pada waktu dan objektifnya. Penilaian formatif dirancang untuk memberikan umpan balik berkelanjutan selama proses pembelajaran, sementara penilaian sumatif mengevaluasi hasil pembelajaran pada akhir periode instruksional.

Studi oleh Chen (2024) menunjukkan bahwa sistem penilaian digital sangat efektif untuk penilaian formatif, karena dapat memberikan umpan balik segera dan memungkinkan peningkatan iteratif. ExamExpert-AI mendukung kedua pendekatan penilaian dengan memungkinkan pendidik membuat kuis latihan untuk tujuan formatif dan ujian akhir untuk evaluasi sumatif.

Keseimbangan antara penilaian formatif dan sumatif memberikan beberapa manfaat:
1. Umpan balik berkelanjutan untuk peningkatan siswa
2. Evaluasi komprehensif terhadap pencapaian pembelajaran
3. Data yang lebih kaya untuk analisis kemajuan siswa
4. Kesempatan untuk penyesuaian strategi pengajaran

## 2.4 Dokumentasi API dan Integrasi Sistem

### 2.4.1 Pentingnya Dokumentasi API dalam Teknologi Pendidikan

Seiring ekosistem teknologi pendidikan menjadi semakin kompleks, kemampuan untuk mengintegrasikan sistem yang berbeda menjadi sangat penting. Dokumentasi API yang komprehensif memfasilitasi integrasi ini, memungkinkan perluasan fungsionalitas dan interoperabilitas dengan alat pendidikan lainnya.

Penelitian oleh Martinez (2023) mengidentifikasi dokumentasi API sebagai faktor kritis dalam adopsi dan implementasi sukses solusi teknologi pendidikan. API yang terdokumentasi dengan baik memungkinkan pengembang untuk membangun di atas sistem yang ada, menciptakan solusi yang disesuaikan yang memenuhi kebutuhan institusi spesifik.

Manfaat dokumentasi API yang baik meliputi:
1. Adopsi teknologi yang lebih cepat oleh pengembang
2. Kemudahan integrasi dengan sistem manajemen pembelajaran
3. Pengembangan ekosistem ekstensi dan plugin
4. Peningkatan skalabilitas dan adaptabilitas sistem

### 2.4.2 Swagger sebagai Standar Dokumentasi

Swagger (OpenAPI) telah muncul sebagai standar industri untuk dokumentasi API, menyediakan pendekatan terstruktur untuk mendeskripsikan endpoint API, parameter permintaan, dan format respons. Studi oleh Kumar et al. (2024) menemukan bahwa dokumentasi Swagger secara signifikan mengurangi waktu yang diperlukan untuk integrasi API dan meningkatkan pengalaman pengembang.

ExamExpert-AI mengimplementasikan dokumentasi Swagger untuk semua endpoint API, memfasilitasi integrasi masa depan dengan sistem manajemen pembelajaran, sistem informasi siswa, dan platform teknologi pendidikan lainnya.

Keunggulan Swagger sebagai standar dokumentasi API meliputi:
1. Format deskripsi yang konsisten dan terstruktur
2. Kemampuan untuk menghasilkan klien API secara otomatis
3. Dukungan untuk pengujian interaktif API
4. Pemeliharaan dokumentasi yang lebih efisien

## 2.5 Teknologi Pengembangan Aplikasi Web Modern

### 2.5.1 Arsitektur Aplikasi Web berbasis API

Pengembangan aplikasi web modern semakin banyak mengadopsi arsitektur berbasis API, di mana backend dan frontend dipisahkan menjadi komponen yang terdefinisi dengan jelas. Pendekatan ini, sering disebut sebagai arsitektur microservices atau RESTful, menawarkan beberapa keunggulan untuk aplikasi pendidikan seperti ExamExpert-AI:

1. Skalabilitas komponen independen
2. Pengembangan paralel frontend dan backend
3. Peningkatan keamanan melalui lapisan API yang terdefinisi dengan baik
4. Fleksibilitas dalam mengubah teknologi frontend atau backend

### 2.5.2 Node.js, Express, dan MongoDB untuk Aplikasi Backend

Stack teknologi yang dipilih untuk ExamExpert-AI terdiri dari Node.js, Express, dan MongoDB, yang merupakan kombinasi populer untuk pengembangan aplikasi backend modern. Node.js menyediakan runtime JavaScript di sisi server, Express menyediakan framework web yang ringan, dan MongoDB menawarkan database NoSQL yang fleksibel.

Keunggulan stack ini meliputi:
1. Performa tinggi dan skalabilitas untuk aplikasi real-time
2. Model data fleksibel yang ideal untuk konten pendidikan yang bervariasi
3. Ekosistem package dan library yang luas
4. Kemudahan deployment ke platform cloud

### 2.5.3 JWT untuk Autentikasi dan Otorisasi

JSON Web Tokens (JWT) telah menjadi standar industri untuk autentikasi dan otorisasi dalam aplikasi web modern. Dalam konteks ExamExpert-AI, JWT menyediakan mekanisme aman untuk:

1. Mengelola sesi pengguna tanpa menyimpan status di server
2. Implementasi kontrol akses berbasis peran (admin, guru, siswa)
3. Menjamin integritas data yang dikirim antara klien dan server
4. Mengurangi overhead database untuk manajemen sesi

## 2.6 Penelitian Terkait

Beberapa penelitian terkait telah dilakukan dalam bidang generasi soal otomatis dan sistem penilaian digital:

1. **Wang et al. (2022)** mengembangkan sistem generasi soal berbasis GPT untuk pembelajaran bahasa Inggris, menunjukkan akurasi 85% dalam menghasilkan soal yang secara pedagogis valid.

2. **Rodriguez dan Kim (2023)** membandingkan performa siswa dalam ujian yang dibuat oleh manusia dan AI, menemukan bahwa tidak ada perbedaan signifikan dalam hasil pembelajaran, mengindikasikan kualitas soal AI yang sebanding.

3. **Patel et al. (2023)** mengimplementasikan sistem evaluasi otomatis untuk jawaban esai pendek menggunakan NLP, mencapai korelasi 0.78 dengan penilaian manusia.

4. **Li dan Zhang (2024)** mengintegrasikan taksonomi Bloom dengan sistem generasi soal AI, menunjukkan peningkatan 40% dalam cakupan tingkat kognitif yang berbeda dibandingkan dengan pendekatan generasi soal tradisional.

Penelitian-penelitian ini memberikan dasar yang kuat untuk pengembangan ExamExpert-AI, menunjukkan kelayakan dan nilai potensial dari sistem generasi soal berbasis AI dalam konteks pendidikan.

## 2.7 Kerangka Konseptual

Berdasarkan tinjauan pustaka yang telah dilakukan, kerangka konseptual untuk ExamExpert-AI dapat dirumuskan sebagai berikut:

1. **Dasar Teknologi**: Memanfaatkan model bahasa besar melalui Perplexity API untuk generasi soal berkualitas tinggi.

2. **Validasi Pedagogi**: Mengintegrasikan prinsip-prinsip taksonomi Bloom untuk memastikan soal mencakup berbagai tingkat kognitif.

3. **Jaminan Kualitas**: Menerapkan mekanisme peninjauan manusia (oleh guru) untuk menjamin kualitas dan relevansi soal.

4. **Keamanan dan Privasi**: Mengimplementasikan praktik terbaik keamanan untuk melindungi data pengguna dan integritas ujian.

5. **Interoperabilitas**: Mengembangkan API yang terdokumentasi dengan baik untuk memfasilitasi integrasi dengan sistem pendidikan lainnya.

6. **Penilaian Komprehensif**: Mendukung berbagai jenis soal dan metode penilaian, termasuk penilaian otomatis untuk soal objektif.

Kerangka ini membentuk landasan untuk pengembangan ExamExpert-AI, memastikan bahwa sistem tidak hanya secara teknologi maju tetapi juga pedagogis valid dan praktis untuk diterapkan dalam konteks pendidikan nyata.
