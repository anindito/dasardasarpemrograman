# Pertemuan 12: Struct, Union, dan Typedef

## 📋 Deskripsi

Materi lengkap untuk Pertemuan 12 tentang **Tipe Data Bentukan (User-Defined Types)** dalam C++. Pertemuan ini membahas struct sebagai cara mengelompokkan data yang berhubungan, union untuk memory efficiency, typedef dan using untuk membuat alias tipe data, serta enum untuk konstanta bernama.

## 🎯 Capaian Pembelajaran

Setelah mempelajari materi ini, mahasiswa diharapkan dapat:

1. Mendefinisikan dan menggunakan struct sebagai tipe data bentukan
2. Mendeklarasikan dan menginisialisasi variabel struct dengan berbagai cara
3. Mengakses dan memodifikasi member struct menggunakan dot operator
4. Mengimplementasikan array of struct untuk mengelola koleksi data terstruktur
5. Memahami perbedaan antara pass by value dan pass by reference untuk struct
6. Membuat dan menggunakan nested struct untuk struktur data hierarkis
7. Memahami konsep union dan perbedaannya dengan struct
8. Menggunakan typedef dan using declaration untuk membuat alias tipe data
9. Mendefinisikan dan menggunakan enum serta enum class
10. Mengaplikasikan konsep-konsep tersebut dalam program nyata

## 📁 Struktur Materi

```
pertemuan-12/
├── Bahan_Ajar_Pertemuan_12.md    # Materi lengkap dalam format Markdown
├── index.html                     # Presentasi HTML (Reveal.js)
├── images/                        # Folder untuk gambar dan diagram
│   ├── struct_visualization.svg   # Visualisasi struct dalam memori
│   └── struct_union_comparison.svg # Perbandingan struct vs union
└── README.md                      # File ini
```

## 📚 Materi yang Dibahas

### 1. **Konsep Dasar Struct** (Bagian 12.2)
- Pengertian struct sebagai tipe data bentukan
- Sintaks definisi struct
- Visualisasi struct dalam memori

### 2. **Deklarasi dan Inisialisasi Struct** (Bagian 12.3)
- Berbagai cara deklarasi variabel struct
- Aggregate initialization
- Designated initializers (C++20)
- Akses member menggunakan dot operator

### 3. **Array of Struct** (Bagian 12.4)
- Deklarasi dan inisialisasi array of struct
- Inisialisasi dengan nilai awal
- Operasi pada array of struct (pencarian, agregasi)

### 4. **Struct sebagai Parameter Fungsi** (Bagian 12.5)
- Pass by value vs pass by reference
- Const reference untuk efisiensi
- Fungsi yang mengembalikan struct

### 5. **Nested Struct** (Bagian 12.6)
- Konsep nested struct
- Inisialisasi nested struct
- Akses member nested struct

### 6. **Union** (Bagian 12.7)
- Pengertian union dan shared memory
- Perbedaan struct dan union
- Tagged union untuk safety

### 7. **Typedef dan Type Aliases** (Bagian 12.8)
- Typedef untuk membuat alias tipe data
- Using declaration (C++11)
- Kegunaan dalam proyek besar

### 8. **Enum dan Enum Class** (Bagian 12.9)
- Enum (enumeration)
- Enum class (scoped enumeration - C++11)
- Enum dalam struct

### 9. **Aplikasi Praktis** (Bagian 12.10)
- Sistem manajemen perpustakaan
- Sistem nilai mahasiswa
- Sistem inventory barang

## 🔑 Konsep Kunci

### Struct
- Mengelompokkan data dengan tipe berbeda menjadi satu kesatuan
- Setiap member memiliki ruang memori sendiri
- Akses menggunakan dot operator (.)
- Dapat berisi member dengan tipe apa saja

### Union
- Member berbagi lokasi memori yang sama
- Hanya satu member valid pada satu waktu
- Ukuran = ukuran member terbesar
- Gunakan tagged union untuk safety

### Typedef vs Using
- Kedua nya membuat alias tipe data
- `using` lebih modern dan readable (C++11+)
- `using` mendukung template aliases

### Enum vs Enum Class
- Enum class lebih type-safe
- Enum class mencegah name pollution
- Enum class tidak auto-convert ke int

## 📖 Cara Menggunakan Materi

### Untuk Dosen:
1. Gunakan **Bahan_Ajar_Pertemuan_12.md** sebagai referensi mengajar
2. Buka **index.html** di browser untuk presentasi di kelas
3. Gunakan **diagram SVG** untuk menjelaskan konsep secara visual
4. Jalankan contoh-contoh kode untuk demonstrasi live coding
5. Berikan **soal latihan** sebagai tugas praktikum
6. Diskusikan **soal diskusi** untuk memancing critical thinking

### Untuk Mahasiswa:
1. Baca **Bahan_Ajar_Pertemuan_12.md** secara berurutan
2. Pahami setiap konsep sebelum lanjut ke bagian berikutnya
3. **KETIK ULANG** semua contoh kode (jangan copy-paste!)
4. Jalankan dan modifikasi kode untuk eksperimen
5. Kerjakan **soal latihan** untuk mengasah kemampuan
6. Diskusikan **soal diskusi** dengan teman atau dosen
7. Review **presentasi HTML** sebagai rangkuman visual

`


## 💡 Highlight Materi

### Perbedaan Struct dan Union

| Aspek | Struct | Union |
|-------|--------|-------|
| Memori | Setiap member terpisah | Shared memory |
| Ukuran | Sum of all members | Size of largest member |
| Akses | Semua member bersamaan | Hanya satu member valid |
| Use Case | Data grouping | Memory efficiency |

### Kapan Menggunakan?

- **Struct**: Merepresentasikan objek dengan banyak atribut (Point, Student, Book)
- **Union**: Data yang mutually exclusive (variant types)
- **Typedef/Using**: Meningkatkan readability kode
- **Enum Class**: Set nilai terbatas dengan type safety (Status, Color, Direction)

## 🎓 Tips Belajar

1. **Pahami konsep, bukan hafal sintaks**
   - Fokus pada "mengapa" dan "kapan" menggunakan
   - Pahami perbedaan fundamental struct vs union

2. **Praktik dengan contoh nyata**
   - Buat struct untuk data yang Anda kenal (mahasiswa, buku, produk)
   - Implementasikan operasi CRUD sederhana

3. **Eksperimen dengan kode**
   - Coba berbagai cara inisialisasi
   - Bandingkan pass by value vs pass by reference
   - Lihat perbedaan ukuran struct vs union

4. **Perhatikan best practices**
   - Gunakan `const reference` untuk struct besar
   - Gunakan `enum class` daripada `enum`
   - Gunakan `using` daripada `typedef` (C++11+)

5. **Hindari common pitfalls**
   - Jangan lupa titik koma setelah definisi struct
   - Hati-hati mengakses union member yang tidak aktif
   - Waspadai name pollution dengan enum biasa

## 🔗 Materi Terkait

- **Pertemuan 11:** Pointer dan Memori Dinamis
- **Pertemuan 13:** C++ di Platform Lain
- **Pertemuan 14:** Pengenalan Pemrograman Berorientasi Objek

## 📚 Referensi Utama

1. Deitel, P. & Deitel, H. (2020). *C++ How to Program* (10th ed.). Chapter 10
2. Savitch, W. (2017). *Problem Solving with C++* (10th ed.). Chapter 10
3. Stroustrup, B. (2014). *Programming: Principles and Practice Using C++* (2nd ed.). Chapter 9
4. Lippman, S. B., et al. (2012). *C++ Primer* (5th ed.). Chapter 7
5. Meyers, S. (2014). *Effective Modern C++*. Item 10
6. cppreference.com. (2024). *Structures*

## 🤝 Kontribusi

Jika menemukan kesalahan atau ingin memberikan saran:
1. Buat issue di repository
2. Atau submit pull request dengan perbaikan

## 📄 Lisensi

Materi ini dibuat untuk keperluan pendidikan dan dapat digunakan secara bebas dengan tetap mencantumkan sumber.

---

**Terakhir diperbarui:** November 2025  
**Versi:** 1.0  
**Mata Kuliah:** Dasar-Dasar Pemrograman  
**Pertemuan:** 12 - Struct, Union, dan Typedef

---

**Catatan Penting:**

Struct adalah **jembatan menuju OOP**! Konsep-konsep yang dipelajari di pertemuan ini (struct, member access, nested structures) akan menjadi fondasi penting untuk memahami class dan object-oriented programming di pertemuan mendatang.

**Selamat Belajar! 🚀**
