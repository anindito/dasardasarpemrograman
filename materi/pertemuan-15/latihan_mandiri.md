# LATIHAN DRILL: FILE HANDLING DAN EXCEPTION HANDLING

## Petunjuk Pengerjaan
- Kerjakan latihan secara berurutan dari yang mudah ke yang lebih kompleks
- Jawaban singkat untuk soal konseptual dapat ditulis langsung
- Untuk soal pemrograman, tulis kode lengkap yang bisa dikompilasi

---

## BAGIAN 1: FILE HANDLING DASAR (15 Soal)

### Soal 1-5: Konsep Dasar

**1. Header File**
Header file apa yang harus di-include untuk menggunakan file handling di C++?
```cpp
// Jawaban:

```

**2. Stream Classes**
Lengkapi tabel berikut:

| Class | Fungsi |
|-------|--------|
| ifstream | ? |
| ? | Menulis ke file |
| fstream | ? |

**3. Membuka File**
Tuliskan dua cara untuk membuka file dalam C++.
```cpp
// Cara 1:


// Cara 2:


```

**4. File Modes**
Apa perbedaan antara `ios::out` dan `ios::app`?
```
Jawaban:



```

**5. Menutup File**
Mengapa kita harus menutup file setelah selesai menggunakannya? Sebutkan minimal 3 alasan.
```
1. 

2. 

3. 

```

### Soal 6-10: Operasi File Sederhana

**6. Menulis String ke File**
Buatlah program yang menulis "Hello World!" ke file bernama output.txt.
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    // Tulis kode di sini
    
    
    
    
    
    return 0;
}
```

**7. Membaca Isi File**
Buatlah program yang membaca dan menampilkan isi file input.txt baris per baris.
```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    // Tulis kode di sini
    
    
    
    
    
    return 0;
}
```

**8. Cek File Ada atau Tidak**
Buatlah fungsi yang memeriksa apakah sebuah file ada atau tidak.
```cpp
bool fileExists(string namaFile) {
    // Tulis kode di sini
    
    
    
}
```

**9. Append ke File**
Buatlah program yang menambahkan teks baru di akhir file tanpa menghapus isi yang sudah ada.
```cpp
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    // Tulis kode di sini
    
    
    
    
    
    return 0;
}
```

**10. Hitung Baris dalam File**
Buatlah fungsi yang menghitung jumlah baris dalam sebuah file.
```cpp
int hitungBaris(string namaFile) {
    // Tulis kode di sini
    
    
    
    
    
}
```

### Soal 11-15: File Operations Lanjutan

**11. Copy File**
Buatlah program yang meng-copy isi dari satu file ke file lain.
```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

void copyFile(string sumber, string tujuan) {
    // Tulis kode di sini
    
    
    
    
    
}

int main() {
    copyFile("source.txt", "destination.txt");
    cout << "File berhasil di-copy!" << endl;
    return 0;
}
```

**12. Hitung Kata dalam File**
Buatlah fungsi yang menghitung jumlah kata dalam sebuah file.
```cpp
int hitungKata(string namaFile) {
    // Tulis kode di sini
    
    
    
    
    
}
```

**13. Cari Kata dalam File**
Buatlah program yang mencari apakah kata tertentu ada dalam file.
```cpp
bool cariKata(string namaFile, string kataDicari) {
    // Tulis kode di sini
    
    
    
    
    
}
```

**14. File Position Pointers**
Jelaskan perbedaan antara:
- seekg() dan seekp()
- tellg() dan tellp()

```
seekg vs seekp:


tellg vs tellp:


```

**15. Binary vs Text File**
Buatlah program yang menyimpan dan membaca struct ke/dari file binary.
```cpp
#include <iostream>
#include <fstream>
#include <cstring>
using namespace std;

struct Mahasiswa {
    char nama[50];
    int nim;
    float ipk;
};

void simpanBinary(string namaFile, Mahasiswa mhs) {
    // Tulis kode di sini
    
    
    
}

Mahasiswa bacaBinary(string namaFile) {
    // Tulis kode di sini
    
    
    
}

int main() {
    Mahasiswa mhs;
    strcpy(mhs.nama, "Andi");
    mhs.nim = 12345;
    mhs.ipk = 3.75;
    
    simpanBinary("mhs.dat", mhs);
    Mahasiswa hasil = bacaBinary("mhs.dat");
    
    cout << hasil.nama << endl;
    cout << hasil.nim << endl;
    cout << hasil.ipk << endl;
    
    return 0;
}
```

---

## BAGIAN 2: EXCEPTION HANDLING DASAR (15 Soal)

### Soal 16-20: Konsep Exception

**16. Apa itu Exception?**
Jelaskan dengan kata-kata Anda sendiri apa yang dimaksud dengan exception.
```
Jawaban:



```

**17. Try-Catch Syntax**
Lengkapi template try-catch berikut:
```cpp
try {
    // Kode yang mungkin error
    _______________
}
catch (______ e) {
    // Handle exception
    _______________
}
```

**18. Throw Statement**
Bagaimana cara melempar (throw) exception? Berikan 3 contoh dengan tipe data berbeda.
```cpp
// Contoh 1: Throw string


// Contoh 2: Throw integer


// Contoh 3: Throw object


```

**19. Keuntungan Exception Handling**
Sebutkan minimal 4 keuntungan menggunakan exception handling dibandingkan error code tradisional.
```
1. 

2. 

3. 

4. 

```

**20. Catch Order**
Mengapa urutan catch block itu penting? Apa yang terjadi jika kita menaruh catch yang paling umum di awal?
```
Jawaban:



```

### Soal 21-25: Implementasi Exception

**21. Division by Zero**
Buatlah fungsi pembagian dengan exception handling untuk division by zero.
```cpp
double bagi(double a, double b) {
    // Tulis kode di sini
    
    
    
}

int main() {
    try {
        cout << bagi(10, 2) << endl;   // OK
        cout << bagi(10, 0) << endl;   // Exception
    }
    catch (const char* e) {
        cout << "Error: " << e << endl;
    }
    return 0;
}
```

**22. Array Out of Bounds**
Buatlah fungsi akses array dengan exception handling untuk index out of bounds.
```cpp
int akses(int arr[], int size, int index) {
    // Tulis kode di sini
    
    
    
}

int main() {
    int data[] = {10, 20, 30, 40, 50};
    
    try {
        cout << akses(data, 5, 2) << endl;  // OK
        cout << akses(data, 5, 10) << endl; // Exception
    }
    catch (int badIndex) {
        cout << "Index " << badIndex << " out of bounds!" << endl;
    }
    
    return 0;
}
```

**23. Multiple Catch Blocks**
Buatlah program dengan multiple catch blocks untuk menangani berbagai tipe exception.
```cpp
#include <iostream>
using namespace std;

void proses(int pilihan) {
    // Tulis kode di sini
    // Throw berbagai tipe exception berdasarkan pilihan
    
    
    
}

int main() {
    try {
        proses(1);
    }
    catch (int e) {
        cout << "Caught int: " << e << endl;
    }
    catch (double e) {
        cout << "Caught double: " << e << endl;
    }
    catch (const char* e) {
        cout << "Caught string: " << e << endl;
    }
    catch (...) {
        cout << "Caught unknown exception!" << endl;
    }
    
    return 0;
}
```

**24. Standard Exception Classes**
Sebutkan hierarki standard exception classes di C++. Gambarkan dalam bentuk tree.
```




```

**25. Invalid Argument Exception**
Buatlah fungsi yang menggunakan `invalid_argument` exception.
```cpp
#include <stdexcept>
using namespace std;

int hitungFaktorial(int n) {
    // Tulis kode di sini
    // Throw invalid_argument jika n < 0
    
    
    
    
}

int main() {
    try {
        cout << hitungFaktorial(5) << endl;   // OK
        cout << hitungFaktorial(-1) << endl;  // Exception
    }
    catch (invalid_argument& e) {
        cout << "Error: " << e.what() << endl;
    }
    return 0;
}
```

### Soal 26-30: Exception Lanjutan

**26. Out of Range Exception**
Buatlah fungsi yang menggunakan `out_of_range` exception.
```cpp
#include <stdexcept>
#include <vector>
using namespace std;

int getElement(vector<int>& v, int index) {
    // Tulis kode di sini
    
    
    
}

int main() {
    vector<int> data = {1, 2, 3, 4, 5};
    
    try {
        cout << getElement(data, 2) << endl;   // OK
        cout << getElement(data, 10) << endl;  // Exception
    }
    catch (out_of_range& e) {
        cout << "Error: " << e.what() << endl;
    }
    
    return 0;
}
```

**27. Runtime Error Exception**
Buatlah program yang menggunakan `runtime_error` untuk operasi file.
```cpp
#include <fstream>
#include <stdexcept>
using namespace std;

void bacaFile(string namaFile) {
    // Tulis kode di sini
    // Throw runtime_error jika file tidak bisa dibuka
    
    
    
    
}

int main() {
    try {
        bacaFile("nonexistent.txt");
    }
    catch (runtime_error& e) {
        cout << "Error: " << e.what() << endl;
    }
    return 0;
}
```

**28. Best Practices**
Identifikasi masalah dalam kode berikut dan perbaiki sesuai best practices:
```cpp
// Kode BURUK:
void proses() {
    ifstream* file = new ifstream("data.txt");
    
    // Operasi file...
    
    delete file;
}

// Perbaikan:



```

**29. RAII Pattern**
Jelaskan apa itu RAII dan berikan contoh implementasinya.
```cpp
// Penjelasan RAII:



// Contoh implementasi:



```

**30. Catch by Reference vs Value**
Jelaskan mengapa kita harus catch by reference, bukan by value. Berikan contoh.
```cpp
// Alasan:



// Contoh BURUK (by value):


// Contoh BAIK (by reference):


```

---

## BAGIAN 3: INTEGRASI FILE HANDLING & EXCEPTION (10 Soal)

### Soal 31-35: File Operations dengan Exception

**31. Safe File Open**
Buatlah fungsi yang membuka file dengan exception handling.
```cpp
#include <fstream>
#include <stdexcept>
using namespace std;

ifstream openFileForRead(string namaFile) {
    // Tulis kode di sini
    
    
    
}

int main() {
    try {
        ifstream file = openFileForRead("data.txt");
        // Baca file...
        file.close();
    }
    catch (runtime_error& e) {
        cout << "Error: " << e.what() << endl;
    }
    return 0;
}
```

**32. Safe File Write**
Buatlah fungsi yang menulis ke file dengan exception handling.
```cpp
void writeToFile(string namaFile, string konten) {
    // Tulis kode di sini
    // Throw exception jika gagal menulis
    
    
    
    
}

int main() {
    try {
        writeToFile("output.txt", "Hello World!");
        cout << "File written successfully!" << endl;
    }
    catch (exception& e) {
        cout << "Error: " << e.what() << endl;
    }
    return 0;
}
```

**33. File Copy dengan Exception**
Buatlah fungsi copy file yang comprehensive dengan exception handling.
```cpp
void safeCopyFile(string sumber, string tujuan) {
    // Tulis kode di sini
    // Handle semua kemungkinan error
    
    
    
    
    
}

int main() {
    try {
        safeCopyFile("input.txt", "output.txt");
        cout << "Copy successful!" << endl;
    }
    catch (runtime_error& e) {
        cout << "Copy failed: " << e.what() << endl;
    }
    catch (...) {
        cout << "Unknown error occurred!" << endl;
    }
    return 0;
}
```

**34. Binary File dengan Exception**
Buatlah fungsi untuk menyimpan dan membaca binary file dengan exception handling.
```cpp
struct Data {
    char nama[50];
    int nilai;
};

void saveBinary(string namaFile, Data d) {
    // Tulis kode di sini
    
    
    
}

Data loadBinary(string namaFile) {
    // Tulis kode di sini
    
    
    
}

int main() {
    try {
        Data d;
        strcpy(d.nama, "Test");
        d.nilai = 100;
        
        saveBinary("data.bin", d);
        Data loaded = loadBinary("data.bin");
        
        cout << loaded.nama << ": " << loaded.nilai << endl;
    }
    catch (exception& e) {
        cout << "Error: " << e.what() << endl;
    }
    return 0;
}
```

**35. Log System dengan Exception**
Buatlah sistem log sederhana dengan exception handling.
```cpp
class Logger {
private:
    string logFile;
    
public:
    Logger(string file) : logFile(file) {}
    
    void log(string pesan) {
        // Tulis kode di sini
        // Append message dengan timestamp
        // Handle exception jika file error
        
        
        
    }
};

int main() {
    try {
        Logger logger("app.log");
        logger.log("Application started");
        logger.log("Processing data");
        logger.log("Application ended");
    }
    catch (exception& e) {
        cout << "Logging error: " << e.what() << endl;
    }
    return 0;
}
```

### Soal 36-40: Custom Exceptions untuk File Operations

**36. Custom File Exception**
Buatlah custom exception class untuk file operations.
```cpp
class FileException : public exception {
private:
    string pesan;
    string namaFile;
    
public:
    FileException(string file, string msg) 
        : namaFile(file), pesan(msg) {}
    
    // Implementasi di sini
    
    
};

// Penggunaan:
void bacaFile(string nama) {
    ifstream file(nama);
    if (!file) {
        throw FileException(nama, "Cannot open file");
    }
}
```

**37. File Not Found Exception**
Buatlah specific exception untuk file not found.
```cpp
class FileNotFoundException : public FileException {
public:
    // Tulis kode di sini
    
    
};
```

**38. File Access Denied Exception**
Buatlah exception untuk file access denied.
```cpp
class FileAccessDeniedException : public FileException {
public:
    // Tulis kode di sini
    
    
};
```

**39. Disk Full Exception**
Buatlah exception untuk disk full scenario.
```cpp
class DiskFullException : public exception {
public:
    // Tulis kode di sini
    
    
};

void tulisFile(string nama, string data) {
    ofstream file(nama);
    file << data;
    
    if (file.fail()) {
        throw DiskFullException();
    }
}
```

**40. Integrated File Manager**
Buatlah class FileManager yang mengintegrasikan semua custom exceptions.
```cpp
class FileManager {
public:
    void open(string nama) {
        // Handle berbagai exception
        
    }
    
    void write(string data) {
        // Handle berbagai exception
        
    }
    
    void close() {
        // Handle berbagai exception
        
    }
};

int main() {
    try {
        FileManager fm;
        fm.open("data.txt");
        fm.write("Hello");
        fm.close();
    }
    catch (FileNotFoundException& e) {
        // Handle
    }
    catch (FileAccessDeniedException& e) {
        // Handle
    }
    catch (DiskFullException& e) {
        // Handle
    }
    catch (exception& e) {
        // Handle umum
    }
    return 0;
}
```

---

## BAGIAN 4: APLIKASI TERINTEGRASI (15 Soal)

### Soal 41-45: Database Sederhana

**41. Struct Design**
Desain struct untuk sistem database mahasiswa yang akan disimpan ke binary file.
```cpp
struct Mahasiswa {
    // Tulis kode di sini
    
    
    
};
```

**42. Add Record**
Buatlah fungsi untuk menambah record ke database dengan exception handling.
```cpp
void tambahMahasiswa(string dbFile, Mahasiswa mhs) {
    // Tulis kode di sini
    
    
    
}
```

**43. Read All Records**
Buatlah fungsi untuk membaca semua records dari database.
```cpp
vector<Mahasiswa> bacaSemuaMahasiswa(string dbFile) {
    // Tulis kode di sini
    
    
    
}
```

**44. Search Record**
Buatlah fungsi untuk mencari record berdasarkan NIM.
```cpp
Mahasiswa cariMahasiswa(string dbFile, int nim) {
    // Tulis kode di sini
    // Throw exception jika tidak ditemukan
    
    
    
}
```

**45. Delete Record**
Buatlah fungsi untuk menghapus record dari database.
```cpp
void hapusMahasiswa(string dbFile, int nim) {
    // Tulis kode di sini
    // Load all, remove one, save back
    
    
    
}
```

### Soal 46-50: Config File Manager

**46. Read Config**
Buatlah fungsi untuk membaca config file format key=value.
```cpp
map<string, string> readConfig(string configFile) {
    // Tulis kode di sini
    // Format: DATABASE_PATH=/path/to/db
    //         MAX_CONNECTIONS=100
    
    
    
}
```

**47. Write Config**
Buatlah fungsi untuk menulis config file.
```cpp
void writeConfig(string configFile, map<string, string> config) {
    // Tulis kode di sini
    
    
    
}
```

**48. Get Config Value**
Buatlah fungsi untuk mendapatkan nilai config dengan default value.
```cpp
string getConfigValue(string configFile, string key, string defaultValue) {
    // Tulis kode di sini
    
    
    
}
```

**49. Update Config**
Buatlah fungsi untuk update satu config value.
```cpp
void updateConfig(string configFile, string key, string newValue) {
    // Tulis kode di sini
    
    
    
}
```

**50. Validate Config**
Buatlah fungsi untuk memvalidasi config file.
```cpp
bool validateConfig(string configFile, vector<string> requiredKeys) {
    // Tulis kode di sini
    // Return true jika semua required keys ada
    
    
    
}
```

### Soal 51-55: CSV File Handler

**51. Write CSV**
Buatlah fungsi untuk menulis data ke CSV file.
```cpp
void writeCSV(string csvFile, vector<vector<string>> data) {
    // Tulis kode di sini
    // Format: value1,value2,value3
    
    
    
}
```

**52. Read CSV**
Buatlah fungsi untuk membaca CSV file.
```cpp
vector<vector<string>> readCSV(string csvFile) {
    // Tulis kode di sini
    
    
    
}
```

**53. Add CSV Row**
Buatlah fungsi untuk menambah baris ke CSV file.
```cpp
void addCSVRow(string csvFile, vector<string> row) {
    // Tulis kode di sini
    
    
    
}
```

**54. CSV to Struct**
Buatlah fungsi untuk convert CSV ke vector of struct.
```cpp
struct Person {
    string nama;
    int umur;
    string kota;
};

vector<Person> csvToPerson(string csvFile) {
    // Tulis kode di sini
    
    
    
}
```

**55. Struct to CSV**
Buatlah fungsi untuk convert vector of struct ke CSV.
```cpp
void personToCSV(string csvFile, vector<Person> people) {
    // Tulis kode di sini
    
    
    
}
```

---

## KUNCI JAWABAN

Kunci jawaban tersedia di file terpisah: `Kunci_Jawaban_Latihan_Drill_Pertemuan_15.md`

---

## EVALUASI DIRI

Setelah menyelesaikan latihan ini, Anda seharusnya bisa:

- [ ] Membuka dan menutup file dengan benar
- [ ] Menulis dan membaca file teks
- [ ] Bekerja dengan file binary
- [ ] Menggunakan file position pointers
- [ ] Memahami konsep exception handling
- [ ] Menggunakan try-catch block
- [ ] Throw exception dengan berbagai tipe
- [ ] Menggunakan standard exception classes
- [ ] Membuat custom exception classes
- [ ] Mengintegrasikan file handling dengan exception handling
- [ ] Menerapkan best practices RAII
- [ ] Membuat aplikasi dengan robust error handling

**Skor Anda:** _____ / 55 soal selesai

**Catatan:**
- 45-55: Excellent! Anda menguasai materi dengan baik
- 35-44: Good! Perlu review beberapa konsep
- 25-34: Average. Pelajari lagi materi yang belum dikuasai
- < 25: Perlu belajar lebih intensif

---

**Selamat berlatih! 🚀**
