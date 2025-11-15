# WORKSHEET LAB: FILE HANDLING DAN EXCEPTION HANDLING
**Pertemuan 15 - Dasar-Dasar Pemrograman**

---

## Informasi Mahasiswa

| | |
|---|---|
| **Nama** | : _________________________ |
| **NIM** | : _________________________ |
| **Kelas** | : _________________________ |
| **Tanggal** | : _________________________ |

---

## Tujuan Praktikum

Setelah menyelesaikan praktikum ini, mahasiswa diharapkan mampu:
1. Melakukan operasi file handling (membaca, menulis, append)
2. Bekerja dengan file teks dan binary
3. Mengimplementasikan exception handling dengan try-catch
4. Membuat custom exception classes
5. Mengintegrasikan file handling dengan exception handling
6. Menerapkan best practices dalam error handling

---

## Persiapan

### Software yang Dibutuhkan:
- [ ] Code::Blocks / Visual Studio / VSCode dengan C++ compiler
- [ ] Text editor untuk membuat test files

### File yang Perlu Disiapkan:
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

---

## BAGIAN 1: FILE HANDLING DASAR

### Lab 1.1: Menulis dan Membaca File Teks

**Tujuan:** Memahami operasi dasar file I/O

**Langkah-langkah:**

1. Buat program `lab1_1.cpp`:

```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    // BAGIAN 1: Menulis ke file
    cout << "=== MENULIS KE FILE ===" << endl;
    ofstream fileWrite("output.txt");
    
    if (!fileWrite) {
        cout << "Error: Tidak dapat membuat file!" << endl;
        return 1;
    }
    
    fileWrite << "Nama: [ISI DENGAN NAMA ANDA]" << endl;
    fileWrite << "NIM: [ISI DENGAN NIM ANDA]" << endl;
    fileWrite << "Mata Kuliah: Dasar-Dasar Pemrograman" << endl;
    
    fileWrite.close();
    cout << "Data berhasil ditulis ke output.txt" << endl;
    
    // BAGIAN 2: Membaca dari file
    cout << "\n=== MEMBACA DARI FILE ===" << endl;
    ifstream fileRead("output.txt");
    
    if (!fileRead) {
        cout << "Error: File tidak ditemukan!" << endl;
        return 1;
    }
    
    string baris;
    while (getline(fileRead, baris)) {
        cout << baris << endl;
    }
    
    fileRead.close();
    
    return 0;
}
```

2. Compile dan jalankan program
3. Periksa apakah file `output.txt` terbuat
4. Screenshot hasil output program

**Screenshot Output:**
```
[Tempel screenshot di sini]
```

**Isi file output.txt:**
```
[Salin isi file output.txt di sini]
```

**Pertanyaan:**

a) Apa yang terjadi jika Anda jalankan program dua kali? Apakah isi file output.txt ditimpa atau ditambahkan?
```
Jawaban:


```

b) Bagaimana cara agar isi file tidak ditimpa saat program dijalankan ulang?
```
Jawaban:


```

**Checklist:**
- [ ] Program berhasil dikompilasi
- [ ] File output.txt terbuat
- [ ] Isi file sesuai yang ditulis
- [ ] Screenshot telah diambil

---

### Lab 1.2: Append Mode dan File Logging

**Tujuan:** Memahami perbedaan mode file dan membuat simple logger

**Langkah-langkah:**

1. Buat program `lab1_2.cpp`:

```cpp
#include <iostream>
#include <fstream>
#include <ctime>
using namespace std;

void writeLog(string pesan) {
    // TODO: Buka file "app.log" dengan mode append
    
    
    // TODO: Dapatkan timestamp saat ini
    time_t now = time(0);
    char* dt = ctime(&now);
    
    // TODO: Tulis log dengan format: [timestamp] pesan
    
    
    // TODO: Tutup file
    
}

int main() {
    cout << "Simple Logger Program" << endl;
    
    writeLog("Program dimulai");
    
    cout << "Masukkan nama Anda: ";
    string nama;
    getline(cin, nama);
    
    writeLog("User login: " + nama);
    
    cout << "Melakukan proses..." << endl;
    // Simulasi proses
    
    writeLog("Proses selesai");
    writeLog("Program berakhir");
    
    cout << "Log telah ditulis ke app.log" << endl;
    
    return 0;
}
```

2. Lengkapi bagian TODO
3. Jalankan program beberapa kali
4. Periksa isi file `app.log`

**Isi file app.log setelah 3x menjalankan program:**
```
[Salin isi file app.log di sini]
```

**Pertanyaan:**

a) Mengapa kita menggunakan `ios::app` untuk file log?
```
Jawaban:


```

b) Apa yang terjadi jika kita gunakan `ios::out` saja tanpa `ios::app`?
```
Jawaban:


```

**Checklist:**
- [ ] Fungsi writeLog berhasil diimplementasi
- [ ] Log ditambahkan, tidak ditimpa
- [ ] Timestamp muncul dengan benar
- [ ] Multiple runs menghasilkan log yang bertambah

---

### Lab 1.3: Membaca dan Memproses Data dari File

**Tujuan:** Membaca data terstruktur dan melakukan kalkulasi

**Langkah-langkah:**

1. Pastikan file `data.txt` sudah ada dengan format:
```
Andi 85 90 78
Budi 92 88 95
Citra 78 85 82
```

2. Buat program `lab1_3.cpp`:

```cpp
#include <iostream>
#include <fstream>
#include <string>
#include <iomanip>
using namespace std;

int main() {
    ifstream file("data.txt");
    
    if (!file) {
        cout << "Error: File data.txt tidak ditemukan!" << endl;
        return 1;
    }
    
    cout << "=== LAPORAN NILAI MAHASISWA ===" << endl;
    cout << string(60, '=') << endl;
    cout << left << setw(15) << "Nama" 
         << setw(10) << "UTS" 
         << setw(10) << "UAS" 
         << setw(10) << "Tugas" 
         << setw(15) << "Rata-rata" << endl;
    cout << string(60, '-') << endl;
    
    string nama;
    int uts, uas, tugas;
    
    // TODO: Baca data dari file dan hitung rata-rata
    while (file >> nama >> uts >> uas >> tugas) {
        // TODO: Hitung rata-rata
        
        
        // TODO: Tampilkan data
        
        
    }
    
    cout << string(60, '=') << endl;
    
    file.close();
    
    return 0;
}
```

3. Lengkapi bagian TODO
4. Tambahkan data Anda sendiri ke `data.txt`
5. Jalankan program

**Screenshot Output:**
```
[Tempel screenshot di sini]
```

**Pertanyaan:**

a) Apa yang terjadi jika format data di file tidak sesuai (misal: ada data yang kurang)?
```
Jawaban:


```

b) Bagaimana cara mendeteksi apakah pembacaan file berhasil atau gagal?
```
Jawaban:


```

**Checklist:**
- [ ] Program berhasil membaca data
- [ ] Rata-rata dihitung dengan benar
- [ ] Format output rapi
- [ ] Data tambahan berhasil ditambahkan

---

## BAGIAN 2: EXCEPTION HANDLING DASAR

### Lab 2.1: Try-Catch Sederhana

**Tujuan:** Memahami mekanisme try-catch

**Langkah-langkah:**

1. Buat program `lab2_1.cpp`:

```cpp
#include <iostream>
using namespace std;

double bagi(double a, double b) {
    // TODO: Throw exception jika b == 0
    
    
    return a / b;
}

int main() {
    double angka1, angka2;
    
    cout << "Program Kalkulator Pembagian" << endl;
    cout << "Angka pertama: ";
    cin >> angka1;
    cout << "Angka kedua: ";
    cin >> angka2;
    
    try {
        double hasil = bagi(angka1, angka2);
        cout << "Hasil: " << hasil << endl;
    }
    catch (const char* pesan) {
        cout << "Error: " << pesan << endl;
    }
    
    cout << "Program selesai." << endl;
    
    return 0;
}
```

2. Lengkapi fungsi `bagi()`
3. Test dengan input normal (10, 2)
4. Test dengan division by zero (10, 0)

**Test Case 1 - Input Normal:**
```
Input: 10, 2
Output:


```

**Test Case 2 - Division by Zero:**
```
Input: 10, 0
Output:


```

**Pertanyaan:**

a) Apa yang terjadi tanpa exception handling saat pembagian dengan nol?
```
Jawaban:


```

b) Bagaimana exception handling membuat program lebih robust?
```
Jawaban:


```

**Checklist:**
- [ ] Exception ter-throw dengan benar
- [ ] Catch block menangani exception
- [ ] Program tidak crash
- [ ] Message error informatif

---

### Lab 2.2: Multiple Catch Blocks

**Tujuan:** Menangani berbagai tipe exception

**Langkah-langkah:**

1. Buat program `lab2_2.cpp`:

```cpp
#include <iostream>
using namespace std;

void prosesData(int tipe) {
    if (tipe == 1) {
        throw 404;  // Not found error
    } else if (tipe == 2) {
        throw 3.14159;  // Pi value
    } else if (tipe == 3) {
        throw "Invalid operation";
    } else {
        throw 'X';  // Unknown
    }
}

int main() {
    int pilihan;
    
    cout << "Pilih tipe error (1-4): ";
    cin >> pilihan;
    
    try {
        prosesData(pilihan);
    }
    catch (int errorCode) {
        cout << "Caught integer exception: " << errorCode << endl;
        if (errorCode == 404) {
            cout << "Data not found!" << endl;
        }
    }
    catch (double value) {
        cout << "Caught double exception: " << value << endl;
    }
    catch (const char* msg) {
        cout << "Caught string exception: " << msg << endl;
    }
    catch (...) {
        cout << "Caught unknown exception!" << endl;
    }
    
    return 0;
}
```

2. Test dengan berbagai input (1, 2, 3, 4)

**Test Results:**

| Input | Output yang Diharapkan | Output Aktual |
|-------|------------------------|---------------|
| 1 | | |
| 2 | | |
| 3 | | |
| 4 | | |

**Pertanyaan:**

a) Mengapa urutan catch block itu penting?
```
Jawaban:


```

b) Apa fungsi catch (...)?
```
Jawaban:


```

**Checklist:**
- [ ] Semua catch block berfungsi
- [ ] Exception tertangani sesuai tipe
- [ ] Catch-all berfungsi
- [ ] Semua test case berhasil

---

### Lab 2.3: Standard Exception Classes

**Tujuan:** Menggunakan exception classes dari C++ standard library

**Langkah-langkah:**

1. Buat program `lab2_3.cpp`:

```cpp
#include <iostream>
#include <stdexcept>
#include <vector>
using namespace std;

int akses(vector<int>& data, int index) {
    // TODO: Throw out_of_range jika index invalid
    
    
    return data[index];
}

int faktorial(int n) {
    // TODO: Throw invalid_argument jika n < 0
    
    
    int hasil = 1;
    for (int i = 1; i <= n; i++) {
        hasil *= i;
    }
    return hasil;
}

int main() {
    vector<int> angka = {10, 20, 30, 40, 50};
    
    // Test 1: Access valid index
    try {
        cout << "Test 1: ";
        cout << akses(angka, 2) << endl;
    }
    catch (out_of_range& e) {
        cout << "Error: " << e.what() << endl;
    }
    
    // Test 2: Access invalid index
    try {
        cout << "Test 2: ";
        cout << akses(angka, 10) << endl;
    }
    catch (out_of_range& e) {
        cout << "Error: " << e.what() << endl;
    }
    
    // Test 3: Faktorial valid
    try {
        cout << "Test 3: ";
        cout << faktorial(5) << endl;
    }
    catch (invalid_argument& e) {
        cout << "Error: " << e.what() << endl;
    }
    
    // Test 4: Faktorial invalid
    try {
        cout << "Test 4: ";
        cout << faktorial(-1) << endl;
    }
    catch (invalid_argument& e) {
        cout << "Error: " << e.what() << endl;
    }
    
    return 0;
}
```

2. Lengkapi fungsi `akses()` dan `faktorial()`
3. Jalankan program

**Output Program:**
```
[Salin output lengkap di sini]
```

**Pertanyaan:**

a) Apa keuntungan menggunakan standard exception classes dibanding throw string?
```
Jawaban:


```

b) Method apa yang digunakan untuk mendapatkan pesan error dari exception object?
```
Jawaban:


```

**Checklist:**
- [ ] out_of_range exception berfungsi
- [ ] invalid_argument exception berfungsi
- [ ] Message error dari what() muncul
- [ ] Semua test case berhasil

---

## BAGIAN 3: INTEGRASI FILE HANDLING & EXCEPTION HANDLING

### Lab 3.1: Safe File Operations

**Tujuan:** Mengintegrasikan file handling dengan exception handling

**Langkah-langkah:**

1. Buat program `lab3_1.cpp`:

```cpp
#include <iostream>
#include <fstream>
#include <stdexcept>
#include <string>
using namespace std;

void bacaFile(string namaFile) {
    ifstream file(namaFile);
    
    // TODO: Throw runtime_error jika file tidak bisa dibuka
    
    
    string baris;
    int nomorBaris = 0;
    
    while (getline(file, baris)) {
        nomorBaris++;
        cout << nomorBaris << ". " << baris << endl;
    }
    
    // TODO: Throw runtime_error jika bad()
    
    
    file.close();
}

void tulisFile(string namaFile, string konten) {
    ofstream file(namaFile);
    
    // TODO: Throw runtime_error jika file tidak bisa dibuka
    
    
    file << konten;
    
    // TODO: Throw runtime_error jika fail()
    
    
    file.close();
}

int main() {
    string namaFile, konten;
    int pilihan;
    
    do {
        cout << "\n=== FILE MANAGER ===" << endl;
        cout << "1. Baca File" << endl;
        cout << "2. Tulis File" << endl;
        cout << "3. Keluar" << endl;
        cout << "Pilihan: ";
        cin >> pilihan;
        cin.ignore();
        
        try {
            switch (pilihan) {
                case 1:
                    cout << "Nama file: ";
                    getline(cin, namaFile);
                    bacaFile(namaFile);
                    break;
                    
                case 2:
                    cout << "Nama file: ";
                    getline(cin, namaFile);
                    cout << "Konten: ";
                    getline(cin, konten);
                    tulisFile(namaFile, konten);
                    cout << "File berhasil ditulis!" << endl;
                    break;
                    
                case 3:
                    cout << "Terima kasih!" << endl;
                    break;
                    
                default:
                    cout << "Pilihan tidak valid!" << endl;
            }
        }
        catch (runtime_error& e) {
            cout << "Error: " << e.what() << endl;
        }
        
    } while (pilihan != 3);
    
    return 0;
}
```

2. Lengkapi bagian TODO
3. Test dengan berbagai skenario:
   - Baca file yang ada
   - Baca file yang tidak ada
   - Tulis file baru
   - Tulis file ke folder yang tidak ada akses

**Test Case 1 - Baca file yang ada (test.txt):**
```
Output:


```

**Test Case 2 - Baca file yang tidak ada:**
```
Output:


```

**Test Case 3 - Tulis file baru:**
```
Output:


```

**Pertanyaan:**

a) Mengapa kita perlu exception handling untuk file operations?
```
Jawaban:


```

b) Apa saja kemungkinan error yang bisa terjadi saat operasi file?
```
Jawaban:


```

**Checklist:**
- [ ] Exception ter-throw saat file not found
- [ ] Exception ter-throw saat write fail
- [ ] Program tidak crash
- [ ] Error message informatif

---

### Lab 3.2: Binary File dengan Exception

**Tujuan:** Bekerja dengan binary file dan exception handling

**Langkah-langkah:**

1. Buat program `lab3_2.cpp`:

```cpp
#include <iostream>
#include <fstream>
#include <stdexcept>
#include <cstring>
using namespace std;

struct Mahasiswa {
    char nama[50];
    int nim;
    float ipk;
};

void simpan(string namaFile, Mahasiswa mhs) {
    ofstream file(namaFile, ios::binary | ios::app);
    
    // TODO: Exception handling
    
    
    file.write(reinterpret_cast<char*>(&mhs), sizeof(Mahasiswa));
    
    // TODO: Exception handling
    
    
    file.close();
}

void tampilkanSemua(string namaFile) {
    ifstream file(namaFile, ios::binary);
    
    // TODO: Exception handling
    
    
    Mahasiswa mhs;
    int no = 1;
    
    cout << "\n=== DAFTAR MAHASISWA ===" << endl;
    while (file.read(reinterpret_cast<char*>(&mhs), sizeof(Mahasiswa))) {
        cout << no++ << ". " << mhs.nama 
             << " - " << mhs.nim 
             << " - IPK: " << mhs.ipk << endl;
    }
    
    file.close();
}

int main() {
    string namaFile = "mahasiswa.dat";
    int pilihan;
    
    do {
        cout << "\n=== DATABASE MAHASISWA ===" << endl;
        cout << "1. Tambah Mahasiswa" << endl;
        cout << "2. Tampilkan Semua" << endl;
        cout << "3. Keluar" << endl;
        cout << "Pilihan: ";
        cin >> pilihan;
        cin.ignore();
        
        try {
            switch (pilihan) {
                case 1: {
                    Mahasiswa mhs;
                    cout << "Nama: ";
                    cin.getline(mhs.nama, 50);
                    cout << "NIM: ";
                    cin >> mhs.nim;
                    cout << "IPK: ";
                    cin >> mhs.ipk;
                    cin.ignore();
                    
                    simpan(namaFile, mhs);
                    cout << "Data berhasil disimpan!" << endl;
                    break;
                }
                case 2:
                    tampilkanSemua(namaFile);
                    break;
                    
                case 3:
                    cout << "Terima kasih!" << endl;
                    break;
                    
                default:
                    cout << "Pilihan tidak valid!" << endl;
            }
        }
        catch (runtime_error& e) {
            cout << "Error: " << e.what() << endl;
        }
        catch (exception& e) {
            cout << "Exception: " << e.what() << endl;
        }
        
    } while (pilihan != 3);
    
    return 0;
}
```

2. Lengkapi exception handling
3. Tambahkan minimal 3 data mahasiswa
4. Verifikasi data tersimpan dengan benar

**Data yang Ditambahkan:**

| No | Nama | NIM | IPK |
|----|------|-----|-----|
| 1 | | | |
| 2 | | | |
| 3 | | | |

**Screenshot Output Tampilkan Semua:**
```
[Tempel screenshot di sini]
```

**Pertanyaan:**

a) Apa perbedaan menyimpan data dalam text file vs binary file?
```
Jawaban:


```

b) Mengapa kita menggunakan `reinterpret_cast` saat write/read binary?
```
Jawaban:


```

**Checklist:**
- [ ] Data berhasil disimpan ke binary file
- [ ] Data berhasil dibaca dari binary file
- [ ] Exception handling berfungsi
- [ ] Program tidak corrupt data

---

## BAGIAN 4: CUSTOM EXCEPTION CLASSES

### Lab 4.1: Membuat Custom Exception

**Tujuan:** Membuat exception class sendiri

**Langkah-langkah:**

1. Buat program `lab4_1.cpp`:

```cpp
#include <iostream>
#include <fstream>
#include <exception>
#include <string>
using namespace std;

// TODO: Buat custom exception class
class FileException : public exception {
private:
    string pesan;
    string namaFile;
    
public:
    FileException(string file, string msg) 
        : namaFile(file), pesan(msg) {}
    
    const char* what() const noexcept override {
        return pesan.c_str();
    }
    
    string getFileName() const {
        return namaFile;
    }
};

class FileNotFoundException : public FileException {
public:
    FileNotFoundException(string file) 
        : FileException(file, "File tidak ditemukan") {}
};

class FileWriteException : public FileException {
public:
    // TODO: Implementasi constructor
    
};

void bacaFile(string nama) {
    ifstream file(nama);
    
    if (!file) {
        throw FileNotFoundException(nama);
    }
    
    string baris;
    while (getline(file, baris)) {
        cout << baris << endl;
    }
    
    file.close();
}

void tulisFile(string nama, string data) {
    ofstream file(nama);
    
    if (!file) {
        throw FileWriteException(nama);
    }
    
    file << data;
    
    if (file.fail()) {
        throw FileWriteException(nama);
    }
    
    file.close();
}

int main() {
    try {
        // Test read existing file
        cout << "=== Reading test.txt ===" << endl;
        bacaFile("test.txt");
        
        // Test read non-existing file
        cout << "\n=== Reading nonexistent.txt ===" << endl;
        bacaFile("nonexistent.txt");
    }
    catch (FileNotFoundException& e) {
        cout << "FileNotFoundException: " << e.what() << endl;
        cout << "File: " << e.getFileName() << endl;
    }
    catch (FileWriteException& e) {
        cout << "FileWriteException: " << e.what() << endl;
        cout << "File: " << e.getFileName() << endl;
    }
    catch (FileException& e) {
        cout << "FileException: " << e.what() << endl;
    }
    
    return 0;
}
```

2. Lengkapi class `FileWriteException`
3. Jalankan program

**Output Program:**
```
[Salin output lengkap di sini]
```

**Pertanyaan:**

a) Apa keuntungan membuat custom exception class?
```
Jawaban:


```

b) Mengapa `FileNotFoundException` mewarisi dari `FileException`?
```
Jawaban:


```

**Checklist:**
- [ ] FileException class berfungsi
- [ ] FileNotFoundException berfungsi
- [ ] FileWriteException diimplementasi
- [ ] Inheritance berfungsi dengan benar

---

## BAGIAN 5: PROYEK AKHIR - APLIKASI PERPUSTAKAAN SEDERHANA

### Deskripsi Proyek

Buat aplikasi perpustakaan sederhana dengan fitur:
1. Tambah buku (disimpan ke binary file)
2. Tampilkan semua buku
3. Cari buku berdasarkan ISBN
4. Pinjam buku
5. Kembalikan buku

Dengan requirements:
- Gunakan binary file untuk storage
- Implementasi custom exception classes
- Handle semua kemungkinan error
- RAII pattern untuk file management

### Starter Code

```cpp
#include <iostream>
#include <fstream>
#include <vector>
#include <string>
#include <exception>
using namespace std;

// TODO: Implement custom exceptions
class BukuException : public exception {
    // Your code here
};

class BukuTidakDitemukanException : public BukuException {
    // Your code here
};

class BukuSudahDipinjamException : public BukuException {
    // Your code here
};

struct Buku {
    char isbn[20];
    char judul[100];
    char pengarang[100];
    bool dipinjam;
};

class Perpustakaan {
private:
    string namaFile;
    vector<Buku> daftarBuku;
    
    void muatDariFile() {
        // TODO: Implement
    }
    
    void simpanKeFile() {
        // TODO: Implement
    }
    
public:
    Perpustakaan(string file) : namaFile(file) {
        muatDariFile();
    }
    
    ~Perpustakaan() {
        simpanKeFile();
    }
    
    void tambahBuku(Buku b) {
        // TODO: Implement
    }
    
    void tampilkanSemua() {
        // TODO: Implement
    }
    
    void pinjamBuku(string isbn) {
        // TODO: Implement
        // Throw BukuTidakDitemukanException
        // Throw BukuSudahDipinjamException
    }
    
    void kembalikanBuku(string isbn) {
        // TODO: Implement
    }
};

int main() {
    try {
        Perpustakaan perpus("perpustakaan.dat");
        
        // TODO: Implement menu
        
    }
    catch (exception& e) {
        cout << "Error: " << e.what() << endl;
    }
    
    return 0;
}
```

### Task Checklist

- [ ] Custom exception classes diimplementasi
- [ ] Struct Buku sesuai requirements
- [ ] Method muatDariFile() berfungsi
- [ ] Method simpanKeFile() berfungsi
- [ ] Method tambahBuku() berfungsi
- [ ] Method tampilkanSemua() berfungsi
- [ ] Method pinjamBuku() dengan exception handling
- [ ] Method kembalikanBuku() berfungsi
- [ ] Menu interaktif lengkap
- [ ] All exceptions handled properly
- [ ] RAII pattern implemented (destructor saves file)
- [ ] Program tested dengan berbagai skenario

### Test Scenarios

**Scenario 1: Tambah 3 Buku**
```
[Dokumentasikan hasilnya]
```

**Scenario 2: Pinjam Buku yang Ada**
```
[Dokumentasikan hasilnya]
```

**Scenario 3: Pinjam Buku yang Sudah Dipinjam**
```
[Dokumentasikan hasilnya]
```

**Scenario 4: Pinjam Buku yang Tidak Ada**
```
[Dokumentasikan hasilnya]
```

**Scenario 5: Kembalikan Buku**
```
[Dokumentasikan hasilnya]
```

### Screenshot Aplikasi Berjalan

**Menu Utama:**
```
[Screenshot]
```

**Tambah Buku:**
```
[Screenshot]
```

**Tampilkan Semua:**
```
[Screenshot]
```

**Exception Handling:**
```
[Screenshot saat exception terjadi]
```

---

## REFLEKSI

### Apa yang Anda Pelajari?

Dari praktikum ini, saya telah mempelajari:

1. File Handling:
```
[Tuliskan reflection Anda]
```

2. Exception Handling:
```
[Tuliskan reflection Anda]
```

3. Integrasi keduanya:
```
[Tuliskan reflection Anda]
```

### Kesulitan yang Dihadapi

Tantangan yang saya hadapi:
```
[Tuliskan tantangan dan bagaimana Anda mengatasinya]
```

### Aplikasi di Dunia Nyata

Bagaimana materi ini bisa diterapkan:
```
[Tuliskan ide aplikasi Anda]
```

---

## SUBMISSION CHECKLIST

Sebelum mengumpulkan, pastikan:

- [ ] Semua Lab 1.1 - 1.3 selesai
- [ ] Semua Lab 2.1 - 2.3 selesai
- [ ] Semua Lab 3.1 - 3.2 selesai
- [ ] Lab 4.1 selesai
- [ ] Proyek Akhir selesai dan tested
- [ ] Semua screenshot diambil
- [ ] Semua pertanyaan dijawab
- [ ] Refleksi ditulis
- [ ] Code dikompilasi tanpa error
- [ ] Semua file yang diminta disertakan

**Files to Submit:**
1. Worksheet_Lab_Pertemuan_15.md (file ini)
2. Semua source code (.cpp)
3. Screenshot (dalam folder terpisah)
4. File-file hasil program (output.txt, app.log, dll)

---

**Nama Pengumpul:** _________________________

**Tanggal Pengumpulan:** _________________________

**Nilai:** _____ / 100

**Catatan Dosen:**
```




```

---

**Selamat mengerjakan! 🚀**
