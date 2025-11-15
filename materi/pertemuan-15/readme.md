# Pertemuan 15: File Handling dan Exception Handling

## 📋 Overview

Pertemuan terakhir sebelum UAS ini membahas dua topik penting dalam pengembangan aplikasi C++ yang robust dan profesional: **File Handling** dan **Exception Handling**. Kedua topik ini sering digunakan bersamaan karena operasi file adalah salah satu sumber error yang paling umum dalam programming.

## 🎯 Capaian Pembelajaran

Setelah mempelajari materi pertemuan ini, mahasiswa diharapkan mampu:

1. **File Handling:**
   - Memahami konsep file handling dan stream classes (ifstream, ofstream, fstream)
   - Melakukan operasi membaca dan menulis file teks
   - Bekerja dengan file binary untuk efisiensi storage
   - Menggunakan file modes (in, out, app, binary) dengan tepat
   - Memanfaatkan file position pointers (seekg, seekp, tellg, tellp)
   - Memeriksa status file dengan eof(), fail(), bad(), good()

2. **Exception Handling:**
   - Memahami konsep exception dan pentingnya error handling
   - Mengimplementasikan try-catch block
   - Menggunakan throw statement untuk melempar exception
   - Menangani berbagai tipe exception dengan multiple catch blocks
   - Menggunakan standard exception classes dari C++ library
   - Membuat custom exception classes untuk kebutuhan spesifik
   - Menerapkan best practices dalam exception handling

3. **Integrasi:**
   - Mengintegrasikan file handling dengan exception handling
   - Menerapkan RAII pattern untuk resource management
   - Membuat aplikasi yang robust dengan comprehensive error handling

## 📚 Materi Pembelajaran

### 1. Bahan Ajar (62 KB)
[📖 Baca Bahan Ajar](Bahan_Ajar_Pertemuan_15.md)

Dokumen komprehensif berisi:
- **15.1 Pendahuluan** - Motivasi dan overview
- **15.2 File Handling di C++**
  - 15.2.1 Konsep Dasar File Handling
  - 15.2.2 Membuka dan Menutup File
  - 15.2.3 File Modes
  - 15.2.4 Menulis ke File Teks
  - 15.2.5 Membaca dari File Teks
  - 15.2.6 Memeriksa Status File
  - 15.2.7 File Position Pointers
  - 15.2.8 Binary File Operations
- **15.3 Exception Handling di C++**
  - 15.3.1 Konsep Exception dan Error Handling
  - 15.3.2 Try-Catch Block
  - 15.3.3 Throw Statement
  - 15.3.4 Multiple Catch Blocks
  - 15.3.5 Standard Exception Classes
  - 15.3.6 Exception dalam File Operations
  - 15.3.7 Custom Exception Classes
  - 15.3.8 Best Practices Exception Handling
- **15.4 Studi Kasus Terintegrasi** - Sistem perpustakaan lengkap
- **15.5 Rangkuman**
- **15.6 Soal Latihan**
- **15.7 Pertanyaan Diskusi**
- Referensi akademik

### 2. Slide Presentasi (HTML)
[🎬 Buka Slide](Slide_Pertemuan_15.html)

Presentasi interaktif dengan Reveal.js mencakup:
- Tujuan pembelajaran
- File Handling: konsep, syntax, dan contoh
- Exception Handling: mekanisme dan best practices
- Diagram alur dan ilustrasi
- Studi kasus aplikasi perpustakaan
- Rangkuman dan tips

**Cara menggunakan:**
- Buka file HTML di browser
- Gunakan arrow keys untuk navigasi
- Press 'F' untuk fullscreen
- Press 'S' untuk speaker notes
- Press 'O' untuk overview mode

### 3. Diagram SVG
Visualisasi konsep-konsep penting:

#### [file-handling-flow.svg](images/file-handling-flow.svg)
Diagram alur kerja file handling dari membuka file hingga menutup file, termasuk error handling.

#### [file-modes.svg](images/file-modes.svg)
Perbandingan visual antara mode `ios::out` (truncate) dan `ios::app` (append), menunjukkan apa yang terjadi dengan isi file lama.

#### [file-pointers.svg](images/file-pointers.svg)
Ilustrasi file position pointers dengan contoh penggunaan `seekg()`, `seekp()`, `tellg()`, dan `tellp()`.

#### [exception-flow.svg](images/exception-flow.svg)
Alur kerja exception handling dengan try-catch block, menunjukkan perbedaan program dengan dan tanpa exception handling.

### 4. Latihan Drill (55 Soal)
[✍️ Kerjakan Latihan](Latihan_Drill_Pertemuan_15.md)

Latihan terstruktur dalam 4 bagian:

**Bagian 1: File Handling Dasar (15 soal)**
- Konsep dasar (header, stream classes, file modes)
- Operasi file sederhana (write, read, append)
- File operations lanjutan (copy, search, binary)

**Bagian 2: Exception Handling Dasar (15 soal)**
- Konsep exception
- Try-catch implementation
- Standard exception classes

**Bagian 3: Integrasi File & Exception (10 soal)**
- File operations dengan exception
- Custom exceptions untuk file operations

**Bagian 4: Aplikasi Terintegrasi (15 soal)**
- Database sederhana
- Config file manager
- CSV file handler

### 5. Worksheet Lab (Praktikum)
[🔬 Worksheet Lab](Worksheet_Lab_Pertemuan_15.md)

Hands-on exercises terstruktur:

**Bagian 1: File Handling Dasar**
- Lab 1.1: Menulis dan Membaca File Teks
- Lab 1.2: Append Mode dan File Logging
- Lab 1.3: Membaca dan Memproses Data dari File

**Bagian 2: Exception Handling Dasar**
- Lab 2.1: Try-Catch Sederhana
- Lab 2.2: Multiple Catch Blocks
- Lab 2.3: Standard Exception Classes

**Bagian 3: Integrasi**
- Lab 3.1: Safe File Operations
- Lab 3.2: Binary File dengan Exception

**Bagian 4: Custom Exception Classes**
- Lab 4.1: Membuat Custom Exception

**Bagian 5: Proyek Akhir**
- Aplikasi Perpustakaan Sederhana (complete project)

## 🔑 Konsep Kunci

### File Handling

**Stream Classes:**
```cpp
ifstream  // Input - membaca file
ofstream  // Output - menulis file
fstream   // Both - baca & tulis
```

**File Modes:**
```cpp
ios::in      // Membaca
ios::out     // Menulis (hapus isi lama)
ios::app     // Append (jaga isi lama)
ios::binary  // Mode binary
```

**Basic Operations:**
```cpp
// Menulis
ofstream file("data.txt");
file << "Hello World!" << endl;
file.close();

// Membaca
ifstream file("data.txt");
string line;
while (getline(file, line)) {
    cout << line << endl;
}
file.close();

// Binary
ofstream file("data.bin", ios::binary);
file.write(reinterpret_cast<char*>(&data), sizeof(data));
file.close();
```

### Exception Handling

**Try-Catch Pattern:**
```cpp
try {
    // Kode yang mungkin error
    if (error_condition) {
        throw "Error message";
    }
}
catch (const char* e) {
    // Handle error
    cout << "Error: " << e << endl;
}
```

**Standard Exceptions:**
```cpp
#include <stdexcept>

throw invalid_argument("Invalid input");
throw out_of_range("Index out of bounds");
throw runtime_error("Runtime error occurred");
```

**Custom Exception:**
```cpp
class MyException : public exception {
public:
    const char* what() const noexcept override {
        return "My custom error";
    }
};

throw MyException();
```

### Best Practices

1. **File Handling:**
   - Selalu tutup file setelah selesai
   - Cek apakah file berhasil dibuka
   - Gunakan RAII pattern
   - Handle error dengan exception

2. **Exception Handling:**
   - Catch by reference: `catch (exception& e)`
   - Throw by value: `throw MyException()`
   - Catch specific exceptions first
   - Don't throw in destructor
   - Provide informative error messages

3. **Integrasi:**
   - Combine file ops dengan exception handling
   - Use RAII for automatic cleanup
   - Handle all possible errors
   - Make code robust and maintainable

## 🎓 Topik yang Dibahas vs Tidak Dibahas

### ✅ Dibahas dalam Pertemuan Ini

**File Handling:**
- Stream classes (ifstream, ofstream, fstream)
- File modes (in, out, app, ate, trunc, binary)
- Text file operations (read, write, append)
- Binary file operations
- File position pointers (seekg/seekp, tellg/tellp)
- File status checking (eof, fail, bad, good)

**Exception Handling:**
- Try-catch block
- Throw statement
- Multiple catch blocks
- Standard exception classes (invalid_argument, out_of_range, runtime_error, dll)
- Custom exception classes
- Exception dalam file operations
- RAII pattern
- Best practices

### ❌ Tidak Dibahas (Untuk Mata Kuliah Lanjutan)

- Advanced file I/O (memory-mapped files, async I/O)
- File system operations (create directory, delete file, dll)
- Stream manipulators yang advanced
- Wide character streams (wifstream, wofstream)
- Exception specifications (noexcept, throw())
- Exception safety guarantees (basic, strong, no-throw)
- Stack unwinding details
- Nested exceptions
- Exception performance optimization

## 🔧 Setup dan Tools

### Compiler Requirements
- C++11 atau lebih baru
- Support untuk `<fstream>`, `<exception>`, `<stdexcept>`

### Recommended IDEs
- Code::Blocks
- Visual Studio
- VSCode dengan C++ extension
- CLion

### Testing Files
Buat file-file berikut untuk testing:

**test.txt:**
```
Baris pertama
Baris kedua
Baris ketiga
```

**data.txt:**
```
Andi 85 90 78
Budi 92 88 95
Citra 78 85 82
```

## 📝 Evaluasi

Materi pertemuan ini akan dievaluasi melalui:

1. **Latihan Drill (55 soal)** - Self-assessment
2. **Worksheet Lab** - Hands-on praktikum
3. **Proyek Akhir** - Aplikasi perpustakaan
4. **UAS** - Mencakup file handling dan exception handling

## 🔗 Hubungan dengan Materi Lain

**Prerequisites:**
- Pertemuan 9-10: Array (untuk membaca data terstruktur)
- Pertemuan 11: Pointer (untuk binary operations)
- Pertemuan 12: Struct (untuk data structures)
- Pertemuan 14: OOP (untuk custom exceptions)

**Aplikasi ke Depan:**
- Proyek akhir semester
- Aplikasi database sederhana
- Log system
- Configuration manager
- Data persistence

## 💡 Tips Belajar

1. **Praktik Langsung:**
   - Buat file sendiri dan coba berbagai operasi
   - Eksperimen dengan berbagai file modes
   - Test exception handling dengan berbagai skenario

2. **Debugging:**
   - Gunakan debugger untuk melihat alur exception
   - Check file status dengan berbagai method
   - Verify file contents setelah operasi

3. **Best Practices:**
   - Selalu handle exceptions
   - Jangan lupa tutup file
   - Use RAII pattern
   - Make error messages clear

4. **Common Mistakes:**
   - Lupa menutup file
   - Tidak cek file status
   - Catch by value instead of reference
   - Throw in destructor
   - Empty catch blocks

## 📖 Referensi Tambahan

1. **Deitel & Deitel** - C++ How to Program
   - Chapter 14: File Processing
   - Chapter 16: Exception Handling

2. **Walter Savitch** - Problem Solving with C++
   - Chapter 12: Streams and File I/O
   - Chapter 16: Exception Handling

3. **Bjarne Stroustrup** - Programming: Principles and Practice
   - Chapter 10: Input and Output Streams
   - Chapter 11: Customizing I/O

4. **Online Resources:**
   - cppreference.com - File I/O
   - cppreference.com - Exceptions
   - learncpp.com - File handling
   - learncpp.com - Exception handling

## 🚀 Next Steps

Setelah menguasai materi ini:

1. ✅ Selesaikan semua latihan drill
2. ✅ Kerjakan worksheet lab
3. ✅ Selesaikan proyek perpustakaan
4. ✅ Review semua materi Pertemuan 1-15
5. ✅ Persiapkan UAS
6. 🎯 Terapkan pada proyek akhir semester

## 📧 Support

Jika ada pertanyaan atau kesulitan:
- Diskusi di forum kelas
- Office hours dosen
- Study group dengan teman

---

**Good luck dengan pembelajaran file handling dan exception handling!** 🎉

Ini adalah pertemuan terakhir sebelum UAS. Pastikan Anda menguasai semua konsep dengan baik karena ini adalah fondasi penting untuk menjadi programmer yang profesional!

**Remember:** 
- Files need to be closed
- Exceptions need to be caught
- Code needs to be robust
- Practice makes perfect! 💪
