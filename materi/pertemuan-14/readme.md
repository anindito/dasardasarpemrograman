# BAB 14: FILE HANDLING DAN EXCEPTION HANDLING

## 14.1 Pendahuluan

Selamat datang di pertemuan keempat belas mata kuliah Dasar-Dasar Pemrograman. Hingga saat ini, semua program yang kita buat menyimpan data hanya di dalam memori komputer (RAM). Ketika program berakhir, semua data yang tersimpan akan hilang. Pada pertemuan ini, kita akan mempelajari cara menyimpan dan membaca data secara permanen menggunakan file, serta bagaimana menangani kesalahan (error) yang mungkin terjadi selama proses tersebut.

Bayangkan Anda memiliki aplikasi buku alamat. Tentu tidak masuk akal jika setiap kali membuka aplikasi, pengguna harus memasukkan kembali semua kontak dari awal. Dengan file handling, data kontak dapat disimpan ke dalam file di hard disk dan dibaca kembali ketika aplikasi dijalankan lagi. Kemampuan membaca dan menulis file adalah skill fundamental yang dibutuhkan dalam hampir semua aplikasi dunia nyata, mulai dari game yang menyimpan progress, editor teks yang menyimpan dokumen, hingga database yang menyimpan jutaan record.

Selain file handling, kita juga akan mempelajari exception handling, yaitu mekanisme untuk menangani situasi tidak normal (exceptional) yang mungkin terjadi saat program berjalan. Misalnya, apa yang terjadi jika program mencoba membuka file yang tidak ada? Atau bagaimana menangani pembagian dengan nol? Exception handling memungkinkan kita membuat program yang lebih robust dan tidak crash ketika menghadapi situasi yang tidak diharapkan.

## 14.2 Konsep Dasar File dalam C++

### 14.2.1 Pengertian File dan Stream

Dalam pemrograman, file adalah kumpulan data yang disimpan di media penyimpanan permanen seperti hard disk, SSD, atau USB drive. Berbeda dengan data di RAM yang bersifat volatile (hilang saat komputer dimatikan), data di file bersifat persistent dan tetap ada meskipun program berakhir atau komputer dimatikan.

C++ menggunakan konsep stream untuk berkomunikasi dengan file. Stream dapat dibayangkan sebagai aliran data antara program dan file. Sama seperti air yang mengalir melalui pipa, data mengalir dari program ke file (output stream) atau dari file ke program (input stream). Konsep ini sebenarnya sudah familiar bagi kita karena cin dan cout yang sering kita gunakan juga merupakan stream, yaitu input stream dari keyboard dan output stream ke layar.

Untuk bekerja dengan file, C++ menyediakan library `<fstream>` yang berisi tiga class utama. Class `ifstream` (input file stream) digunakan untuk membaca data dari file. Class `ofstream` (output file stream) digunakan untuk menulis data ke file. Class `fstream` (file stream) merupakan class yang paling fleksibel karena dapat digunakan untuk membaca maupun menulis file.

*Gambar 14.1: Diagram konsep stream dalam C++. Gambar menunjukkan aliran data dari keyboard melalui cin ke program, dari program melalui cout ke monitor, dari file melalui ifstream ke program, dan dari program melalui ofstream ke file.*

### 14.2.2 Jenis-Jenis File

Secara umum, file dalam pemrograman dibagi menjadi dua kategori utama. Pertama adalah file teks (text file) yang menyimpan data dalam bentuk karakter yang dapat dibaca manusia. File teks menggunakan encoding seperti ASCII atau UTF-8, dan dapat dibuka dengan text editor seperti Notepad. Contoh file teks termasuk file .txt, .cpp, .csv, dan .html. Setiap baris dalam file teks biasanya diakhiri dengan karakter newline.

Kategori kedua adalah file biner (binary file) yang menyimpan data dalam bentuk byte mentah, persis seperti representasinya di memori komputer. File biner tidak dapat dibaca langsung dengan text editor biasa karena isinya bukan karakter yang bisa diinterpretasi. Contoh file biner termasuk file gambar (.jpg, .png), file executable (.exe), file audio (.mp3), dan file dokumen tertentu (.docx).

Pada pertemuan ini, kita akan fokus pada file teks karena lebih mudah dipahami dan di-debug. Konsep dasar yang dipelajari juga berlaku untuk file biner dengan sedikit penyesuaian.

## 14.3 Membuka dan Menutup File

### 14.3.1 Membuka File dengan Constructor

Cara paling sederhana untuk membuka file adalah dengan menyertakan nama file saat membuat objek stream. Ketika objek stream dibuat dengan nama file sebagai parameter, file tersebut otomatis dibuka dan siap digunakan.

```cpp
// Membuka file untuk dibaca
// File "data.txt" harus sudah ada, jika tidak akan error
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    // Membuka file untuk membaca
    ifstream fileInput("data.txt");
    
    // Membuka file untuk menulis
    // Jika file belum ada, akan dibuat baru
    // Jika file sudah ada, isinya akan ditimpa
    ofstream fileOutput("hasil.txt");
    
    // ... operasi file ...
    
    // File otomatis ditutup saat objek keluar dari scope
    return 0;
}
```
*Contoh 14.1: Cara membuka file menggunakan constructor. File input harus sudah ada sebelumnya, sedangkan file output akan dibuat otomatis jika belum ada.*

### 14.3.2 Membuka File dengan Fungsi open()

Alternatif lain adalah dengan menggunakan fungsi member open(). Cara ini berguna jika kita ingin mendeklarasikan objek stream terlebih dahulu dan membuka file-nya nanti, atau jika kita ingin menggunakan satu objek stream untuk membuka beberapa file secara bergantian.

```cpp
// Membuka file menggunakan fungsi open()
// Memungkinkan pembuatan objek stream tanpa langsung membuka file
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    ifstream fileInput;     // Deklarasi tanpa membuka file
    ofstream fileOutput;
    
    // Membuka file nanti saat dibutuhkan
    fileInput.open("data.txt");
    fileOutput.open("hasil.txt");
    
    // Cek apakah file berhasil dibuka
    if (!fileInput.is_open()) {
        cout << "Gagal membuka file input!" << endl;
        return 1;
    }
    
    if (!fileOutput.is_open()) {
        cout << "Gagal membuka file output!" << endl;
        return 1;
    }
    
    cout << "Kedua file berhasil dibuka." << endl;
    
    // Menutup file
    fileInput.close();
    fileOutput.close();
    
    return 0;
}
```
*Contoh 14.2: Membuka file dengan fungsi open() dan melakukan pengecekan apakah file berhasil dibuka menggunakan is_open().*

### 14.3.3 Mode Pembukaan File

Saat membuka file, kita dapat menentukan mode pembukaan yang mengatur bagaimana file tersebut akan diakses. Mode-mode ini didefinisikan sebagai konstanta dalam class ios dan dapat dikombinasikan menggunakan operator bitwise OR (|).

Mode `ios::in` membuka file untuk operasi input (membaca). Mode `ios::out` membuka file untuk operasi output (menulis) dan akan menghapus isi file yang sudah ada. Mode `ios::app` (append) membuka file untuk menulis di akhir file tanpa menghapus isi yang sudah ada. Mode `ios::binary` membuka file dalam mode biner, bukan mode teks. Mode `ios::ate` (at end) menempatkan posisi baca/tulis di akhir file saat pertama kali dibuka. Mode `ios::trunc` (truncate) menghapus isi file yang sudah ada saat dibuka.

```cpp
// Demonstrasi berbagai mode pembukaan file
// Setiap mode memiliki perilaku yang berbeda
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    // Mode default untuk ofstream adalah ios::out | ios::trunc
    // Isi file akan dihapus dan ditulis ulang
    ofstream file1("test1.txt");
    file1 << "Data baru menggantikan data lama" << endl;
    file1.close();
    
    // Mode append: menulis di akhir file tanpa menghapus
    ofstream file2("test2.txt", ios::app);
    file2 << "Data ini ditambahkan di akhir file" << endl;
    file2.close();
    
    // Mode biner: untuk file non-teks
    ofstream file3("test3.bin", ios::binary);
    int angka = 12345;
    file3.write(reinterpret_cast<char*>(&angka), sizeof(angka));
    file3.close();
    
    // Kombinasi mode: membaca dan menulis
    fstream file4("test4.txt", ios::in | ios::out);
    // ... operasi baca tulis ...
    file4.close();
    
    cout << "Semua file berhasil dibuat dengan mode berbeda." << endl;
    
    return 0;
}
```
*Contoh 14.3: Demonstrasi berbagai mode pembukaan file. Mode dapat dikombinasikan dengan operator OR untuk mendapatkan perilaku yang diinginkan.*

### 14.3.4 Menutup File

Setelah selesai menggunakan file, sangat penting untuk menutupnya dengan memanggil fungsi close(). Menutup file memastikan semua data yang masih ada di buffer benar-benar ditulis ke file (flush), dan melepaskan resource sistem yang digunakan untuk menangani file tersebut.

Meskipun file akan otomatis ditutup ketika objek stream keluar dari scope (berkat destructor), menutup file secara eksplisit adalah praktik yang baik. Hal ini terutama penting jika program akan membuka banyak file atau jika file yang sama akan dibuka kembali dengan mode berbeda.

```cpp
// Pentingnya menutup file secara eksplisit
// Mendemonstrasikan penggunaan file yang sama secara berurutan
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    string namaFile = "catatan.txt";
    
    // Pertama: Menulis ke file
    ofstream fileWrite(namaFile);
    fileWrite << "Baris pertama" << endl;
    fileWrite << "Baris kedua" << endl;
    fileWrite.close();  // PENTING: tutup sebelum membuka lagi
    
    // Kedua: Membaca dari file yang sama
    ifstream fileRead(namaFile);
    string baris;
    cout << "Isi file:" << endl;
    while (getline(fileRead, baris)) {
        cout << baris << endl;
    }
    fileRead.close();
    
    // Ketiga: Menambahkan ke file (append)
    ofstream fileAppend(namaFile, ios::app);
    fileAppend << "Baris ketiga (ditambahkan)" << endl;
    fileAppend.close();
    
    cout << "\nFile berhasil diproses." << endl;
    
    return 0;
}
```
*Contoh 14.4: Demonstrasi pentingnya menutup file. File yang sama dibuka berkali-kali dengan mode berbeda, dan harus ditutup sebelum dibuka kembali.*

## 14.4 Menulis Data ke File

### 14.4.1 Menulis dengan Operator <<

Cara termudah untuk menulis ke file teks adalah menggunakan operator insertion (<<), sama seperti yang kita gunakan untuk cout. Operator ini dapat digunakan untuk menulis berbagai tipe data seperti string, integer, float, dan karakter.

```cpp
// Menulis berbagai tipe data ke file menggunakan operator <<
// Operator ini bekerja sama persis seperti cout
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    ofstream file("biodata.txt");
    
    if (!file.is_open()) {
        cout << "Gagal membuka file!" << endl;
        return 1;
    }
    
    // Menulis berbagai tipe data
    string nama = "Ahmad Budi";
    int umur = 20;
    float ipk = 3.75;
    char grade = 'A';
    
    file << "=== DATA MAHASISWA ===" << endl;
    file << "Nama  : " << nama << endl;
    file << "Umur  : " << umur << " tahun" << endl;
    file << "IPK   : " << ipk << endl;
    file << "Grade : " << grade << endl;
    
    file.close();
    
    cout << "Data berhasil ditulis ke biodata.txt" << endl;
    
    return 0;
}
```
*Contoh 14.5: Menulis berbagai tipe data ke file teks menggunakan operator <<. Cara ini identik dengan penggunaan cout.*

**Output file biodata.txt:**
```
=== DATA MAHASISWA ===
Nama  : Ahmad Budi
Umur  : 20 tahun
IPK   : 3.75
Grade : A
```

### 14.4.2 Menulis dengan Fungsi put() dan write()

Selain operator <<, C++ juga menyediakan fungsi put() untuk menulis satu karakter dan write() untuk menulis sejumlah byte tertentu. Fungsi write() terutama berguna untuk file biner.

```cpp
// Menggunakan put() untuk menulis karakter satu per satu
// dan write() untuk menulis sejumlah byte
#include <iostream>
#include <fstream>
#include <cstring>
using namespace std;

int main() {
    ofstream file("output.txt");
    
    // Menggunakan put() untuk menulis karakter
    file.put('H');
    file.put('a');
    file.put('l');
    file.put('o');
    file.put('\n');
    
    // Menggunakan write() untuk menulis string
    const char* pesan = "Selamat belajar C++!\n";
    file.write(pesan, strlen(pesan));
    
    // Menggunakan write() untuk menulis array char
    char buffer[] = "Ini ditulis dengan write()";
    file.write(buffer, sizeof(buffer) - 1);  // -1 untuk mengabaikan null terminator
    
    file.close();
    
    cout << "File output.txt berhasil dibuat." << endl;
    
    return 0;
}
```
*Contoh 14.6: Menggunakan fungsi put() untuk menulis karakter dan write() untuk menulis sejumlah byte ke file.*

### 14.4.3 Menulis Data Terstruktur ke File

Dalam aplikasi nyata, kita sering perlu menyimpan data terstruktur seperti array of struct ke dalam file. Data dapat disimpan dalam format yang mudah dibaca (human-readable) atau dalam format yang mudah diproses oleh program (machine-readable) seperti CSV.

```cpp
// Menyimpan data struct ke file dalam format CSV
// CSV (Comma Separated Values) adalah format standar untuk pertukaran data
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

struct Mahasiswa {
    string nim;
    string nama;
    float ipk;
};

int main() {
    // Data mahasiswa
    Mahasiswa mhs[] = {
        {"2024001", "Ahmad Budi", 3.75},
        {"2024002", "Siti Aminah", 3.90},
        {"2024003", "Budi Santoso", 3.50},
        {"2024004", "Dewi Lestari", 3.85},
        {"2024005", "Eko Prasetyo", 3.60}
    };
    int jumlah = 5;
    
    // Menyimpan ke file CSV
    ofstream file("mahasiswa.csv");
    
    // Header CSV
    file << "NIM,Nama,IPK" << endl;
    
    // Data
    for (int i = 0; i < jumlah; i++) {
        file << mhs[i].nim << ","
             << mhs[i].nama << ","
             << mhs[i].ipk << endl;
    }
    
    file.close();
    
    cout << "Data " << jumlah << " mahasiswa berhasil disimpan ke mahasiswa.csv" << endl;
    
    return 0;
}
```
*Contoh 14.7: Menyimpan array of struct ke file dalam format CSV. Format ini adalah standar industri untuk pertukaran data tabular.*

**Output file mahasiswa.csv:**
```
NIM,Nama,IPK
2024001,Ahmad Budi,3.75
2024002,Siti Aminah,3.90
2024003,Budi Santoso,3.50
2024004,Dewi Lestari,3.85
2024005,Eko Prasetyo,3.60
```

## 14.5 Membaca Data dari File

### 14.5.1 Membaca dengan Operator >>

Operator extraction (>>) dapat digunakan untuk membaca data dari file, sama seperti cin. Operator ini membaca data hingga menemukan whitespace (spasi, tab, atau newline).

```cpp
// Membaca data dari file menggunakan operator >>
// Operator ini membaca data yang dipisahkan whitespace
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    // Pertama, buat file untuk demo
    ofstream fileOut("angka.txt");
    fileOut << "10 20 30 40 50" << endl;
    fileOut << "100 200 300" << endl;
    fileOut.close();
    
    // Baca file yang baru dibuat
    ifstream fileIn("angka.txt");
    
    if (!fileIn.is_open()) {
        cout << "Gagal membuka file!" << endl;
        return 1;
    }
    
    int angka;
    int total = 0;
    int count = 0;
    
    // Membaca semua angka dalam file
    while (fileIn >> angka) {
        cout << "Membaca: " << angka << endl;
        total += angka;
        count++;
    }
    
    cout << "\nTotal angka dibaca: " << count << endl;
    cout << "Jumlah total: " << total << endl;
    cout << "Rata-rata: " << (float)total / count << endl;
    
    fileIn.close();
    
    return 0;
}
```
*Contoh 14.8: Membaca angka dari file menggunakan operator >>. Loop while terus membaca sampai mencapai akhir file.*

**Output:**
```
Membaca: 10
Membaca: 20
Membaca: 30
Membaca: 40
Membaca: 50
Membaca: 100
Membaca: 200
Membaca: 300

Total angka dibaca: 8
Jumlah total: 750
Rata-rata: 93.75
```

### 14.5.2 Membaca Baris dengan getline()

Fungsi getline() membaca satu baris penuh dari file hingga menemukan karakter newline. Fungsi ini sangat berguna untuk membaca teks yang mengandung spasi.

```cpp
// Membaca file baris per baris menggunakan getline()
// Cocok untuk file yang berisi teks dengan spasi
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    // Buat file contoh
    ofstream fileOut("puisi.txt");
    fileOut << "Di Bawah Langit Biru" << endl;
    fileOut << "" << endl;
    fileOut << "Aku berdiri di padang rumput hijau" << endl;
    fileOut << "Memandang langit biru yang begitu indah" << endl;
    fileOut << "Angin sepoi-sepoi menerpa wajahku" << endl;
    fileOut << "Membawa kedamaian ke dalam jiwa" << endl;
    fileOut.close();
    
    // Baca dan tampilkan dengan nomor baris
    ifstream fileIn("puisi.txt");
    
    if (!fileIn.is_open()) {
        cout << "Gagal membuka file!" << endl;
        return 1;
    }
    
    string baris;
    int nomorBaris = 1;
    
    cout << "=== Isi File puisi.txt ===" << endl;
    cout << endl;
    
    while (getline(fileIn, baris)) {
        cout << nomorBaris << ": " << baris << endl;
        nomorBaris++;
    }
    
    cout << endl;
    cout << "Total baris: " << nomorBaris - 1 << endl;
    
    fileIn.close();
    
    return 0;
}
```
*Contoh 14.9: Membaca file baris per baris menggunakan getline(). Fungsi ini membaca seluruh baris termasuk spasi.*

**Output:**
```
=== Isi File puisi.txt ===

1: Di Bawah Langit Biru
2: 
3: Aku berdiri di padang rumput hijau
4: Memandang langit biru yang begitu indah
5: Angin sepoi-sepoi menerpa wajahku
6: Membawa kedamaian ke dalam jiwa

Total baris: 6
```

### 14.5.3 Membaca Karakter dengan get()

Fungsi get() membaca satu karakter dari file. Fungsi ini berguna untuk memproses file karakter per karakter atau untuk membaca karakter whitespace yang diabaikan oleh operator >>.

```cpp
// Membaca file karakter per karakter menggunakan get()
// Berguna untuk menghitung statistik file
#include <iostream>
#include <fstream>
using namespace std;

int main() {
    // Buat file contoh
    ofstream fileOut("sample.txt");
    fileOut << "Hello World!" << endl;
    fileOut << "C++ Programming" << endl;
    fileOut.close();
    
    // Hitung statistik file
    ifstream fileIn("sample.txt");
    
    if (!fileIn.is_open()) {
        cout << "Gagal membuka file!" << endl;
        return 1;
    }
    
    char ch;
    int totalKarakter = 0;
    int huruf = 0;
    int angka = 0;
    int spasi = 0;
    int barisBaru = 0;
    
    while (fileIn.get(ch)) {
        totalKarakter++;
        
        if (isalpha(ch)) {
            huruf++;
        } else if (isdigit(ch)) {
            angka++;
        } else if (ch == ' ') {
            spasi++;
        } else if (ch == '\n') {
            barisBaru++;
        }
    }
    
    cout << "=== Statistik File ===" << endl;
    cout << "Total karakter : " << totalKarakter << endl;
    cout << "Huruf          : " << huruf << endl;
    cout << "Angka          : " << angka << endl;
    cout << "Spasi          : " << spasi << endl;
    cout << "Baris baru     : " << barisBaru << endl;
    
    fileIn.close();
    
    return 0;
}
```
*Contoh 14.10: Membaca file karakter per karakter untuk menghitung statistik. Fungsi get() tidak melewatkan whitespace.*

### 14.5.4 Membaca Data CSV

File CSV (Comma Separated Values) adalah format umum untuk menyimpan data tabular. Membaca CSV membutuhkan parsing khusus untuk memisahkan nilai berdasarkan delimiter (biasanya koma).

```cpp
// Membaca data CSV ke dalam array of struct
// Menggunakan getline dengan delimiter khusus
#include <iostream>
#include <fstream>
#include <sstream>
#include <string>
using namespace std;

struct Mahasiswa {
    string nim;
    string nama;
    float ipk;
};

int main() {
    ifstream file("mahasiswa.csv");
    
    if (!file.is_open()) {
        cout << "Gagal membuka file mahasiswa.csv!" << endl;
        cout << "Pastikan file sudah ada (jalankan Contoh 14.7 terlebih dahulu)." << endl;
        return 1;
    }
    
    Mahasiswa mhs[100];  // Maksimal 100 mahasiswa
    int jumlah = 0;
    string baris;
    
    // Skip header
    getline(file, baris);
    
    // Baca data
    while (getline(file, baris) && jumlah < 100) {
        stringstream ss(baris);
        string token;
        
        // Baca NIM
        getline(ss, mhs[jumlah].nim, ',');
        
        // Baca Nama
        getline(ss, mhs[jumlah].nama, ',');
        
        // Baca IPK
        getline(ss, token, ',');
        mhs[jumlah].ipk = stof(token);
        
        jumlah++;
    }
    
    file.close();
    
    // Tampilkan data yang dibaca
    cout << "=== Data Mahasiswa dari CSV ===" << endl;
    cout << endl;
    
    for (int i = 0; i < jumlah; i++) {
        cout << "Mahasiswa " << i + 1 << ":" << endl;
        cout << "  NIM  : " << mhs[i].nim << endl;
        cout << "  Nama : " << mhs[i].nama << endl;
        cout << "  IPK  : " << mhs[i].ipk << endl;
        cout << endl;
    }
    
    cout << "Total data dibaca: " << jumlah << " mahasiswa" << endl;
    
    return 0;
}
```
*Contoh 14.11: Membaca file CSV dan mem-parsing datanya ke dalam array of struct menggunakan stringstream.*

## 14.6 Memeriksa Status File

### 14.6.1 Fungsi-Fungsi Pengecekan Status

C++ menyediakan beberapa fungsi untuk memeriksa kondisi stream file. Fungsi `is_open()` memeriksa apakah file berhasil dibuka. Fungsi `eof()` memeriksa apakah sudah mencapai akhir file (End Of File). Fungsi `fail()` memeriksa apakah operasi terakhir gagal. Fungsi `bad()` memeriksa apakah terjadi error serius yang tidak dapat dipulihkan. Fungsi `good()` memeriksa apakah stream dalam kondisi baik dan siap digunakan.

```cpp
// Demonstrasi berbagai fungsi pengecekan status file
// Penting untuk memastikan operasi file berjalan dengan benar
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

void cekStatus(ifstream& file, const string& pesan) {
    cout << pesan << endl;
    cout << "  good(): " << file.good() << endl;
    cout << "  eof():  " << file.eof() << endl;
    cout << "  fail(): " << file.fail() << endl;
    cout << "  bad():  " << file.bad() << endl;
    cout << endl;
}

int main() {
    // Buat file untuk testing
    ofstream fileOut("status_test.txt");
    fileOut << "Baris 1" << endl;
    fileOut << "Baris 2" << endl;
    fileOut.close();
    
    ifstream file("status_test.txt");
    
    // Status setelah membuka file
    cekStatus(file, "Setelah membuka file:");
    
    string baris;
    
    // Baca baris pertama
    getline(file, baris);
    cout << "Dibaca: " << baris << endl;
    cekStatus(file, "Setelah baca baris 1:");
    
    // Baca baris kedua
    getline(file, baris);
    cout << "Dibaca: " << baris << endl;
    cekStatus(file, "Setelah baca baris 2:");
    
    // Coba baca lagi (sudah EOF)
    getline(file, baris);
    cekStatus(file, "Setelah mencoba baca di EOF:");
    
    file.close();
    
    // Coba buka file yang tidak ada
    ifstream fileError("tidak_ada.txt");
    if (!fileError.is_open()) {
        cout << "File 'tidak_ada.txt' tidak ditemukan!" << endl;
    }
    
    return 0;
}
```
*Contoh 14.12: Demonstrasi berbagai fungsi pengecekan status stream file. Memahami status file penting untuk menulis program yang robust.*

### 14.6.2 File Position Pointer

Setiap file stream memiliki posisi pointer yang menunjukkan lokasi saat ini dalam file. Untuk input stream, fungsi `tellg()` mengembalikan posisi pointer dan `seekg()` memindahkan posisi pointer. Untuk output stream, fungsi yang setara adalah `tellp()` dan `seekp()`.

```cpp
// Demonstrasi penggunaan file position pointer
// Memungkinkan pembacaan file secara non-sekuensial
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    // Buat file untuk testing
    ofstream fileOut("posisi.txt");
    fileOut << "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    fileOut.close();
    
    ifstream file("posisi.txt");
    char ch;
    
    // Baca dari awal
    cout << "Posisi awal: " << file.tellg() << endl;
    file.get(ch);
    cout << "Karakter di posisi 0: " << ch << endl;
    
    // Pindah ke posisi 10
    file.seekg(10, ios::beg);  // beg = dari awal file
    cout << "\nPosisi setelah seekg(10): " << file.tellg() << endl;
    file.get(ch);
    cout << "Karakter di posisi 10: " << ch << endl;
    
    // Pindah ke 5 karakter sebelum akhir
    file.seekg(-5, ios::end);  // end = dari akhir file
    cout << "\nPosisi setelah seekg(-5, end): " << file.tellg() << endl;
    file.get(ch);
    cout << "Karakter di posisi tersebut: " << ch << endl;
    
    // Pindah relatif dari posisi saat ini
    file.seekg(-3, ios::cur);  // cur = dari posisi saat ini
    cout << "\nPosisi setelah seekg(-3, cur): " << file.tellg() << endl;
    file.get(ch);
    cout << "Karakter di posisi tersebut: " << ch << endl;
    
    // Kembali ke awal
    file.seekg(0, ios::beg);
    cout << "\nMembaca seluruh file dari awal:" << endl;
    while (file.get(ch)) {
        cout << ch;
    }
    cout << endl;
    
    file.close();
    
    return 0;
}
```
*Contoh 14.13: Manipulasi file position pointer dengan seekg() dan tellg(). Parameter kedua menentukan titik referensi (beg, end, atau cur).*

## 14.7 Konsep Exception Handling

### 14.7.1 Apa itu Exception?

Exception adalah situasi abnormal atau tidak terduga yang terjadi saat program berjalan. Contoh exception termasuk pembagian dengan nol, akses array di luar batas, kegagalan membuka file, kehabisan memori, dan input yang tidak valid. Tanpa penanganan yang tepat, exception akan menyebabkan program crash.

Sebelum adanya exception handling, programmer biasanya menggunakan return code atau flag untuk menandai error. Pendekatan ini memiliki beberapa kelemahan. Pertama, kode pengecekan error bercampur dengan logika program utama sehingga sulit dibaca. Kedua, programmer bisa lupa mengecek return code. Ketiga, sulit untuk propagate error ke caller function.

Exception handling menyediakan mekanisme yang lebih terstruktur dan elegan untuk menangani situasi error. Dengan exception handling, kode penanganan error dipisahkan dari logika normal, membuat program lebih mudah dibaca dan di-maintain.

*Gambar 14.2: Diagram alur exception handling. Gambar menunjukkan normal execution flow yang dapat terganggu oleh exception, kemudian ditangkap oleh catch block untuk penanganan error, sebelum program melanjutkan atau terminasi.*

### 14.7.2 Struktur Try-Catch

Exception handling di C++ menggunakan tiga keyword utama: try, catch, dan throw. Block try berisi kode yang mungkin menghasilkan exception. Block catch berisi kode untuk menangani exception. Keyword throw digunakan untuk melempar (mengangkat) exception.

```cpp
// Struktur dasar try-catch
// Exception yang terjadi di try block ditangkap oleh catch block
#include <iostream>
using namespace std;

int main() {
    int pembilang = 10;
    int penyebut = 0;
    
    try {
        // Kode yang mungkin menghasilkan exception
        if (penyebut == 0) {
            throw "Error: Pembagian dengan nol!";
        }
        int hasil = pembilang / penyebut;
        cout << "Hasil: " << hasil << endl;
    }
    catch (const char* pesan) {
        // Kode untuk menangani exception
        cout << "Exception ditangkap: " << pesan << endl;
    }
    
    cout << "Program tetap berjalan setelah exception ditangani." << endl;
    
    return 0;
}
```
*Contoh 14.14: Struktur dasar try-catch. Exception yang dilempar di try block ditangkap oleh catch block yang sesuai.*

**Output:**
```
Exception ditangkap: Error: Pembagian dengan nol!
Program tetap berjalan setelah exception ditangani.
```

### 14.7.3 Melempar Exception dengan throw

Keyword throw digunakan untuk melempar exception ketika kondisi error terdeteksi. Exception yang dilempar bisa berupa nilai dari berbagai tipe data: integer, string, objek class, dan lain-lain.

```cpp
// Berbagai cara melempar exception
// Exception dapat berupa berbagai tipe data
#include <iostream>
#include <string>
using namespace std;

// Fungsi yang melempar exception bertipe int
double hitungAkar(double x) {
    if (x < 0) {
        throw -1;  // Lempar integer sebagai kode error
    }
    return sqrt(x);
}

// Fungsi yang melempar exception bertipe string
void cekUmur(int umur) {
    if (umur < 0) {
        throw string("Umur tidak boleh negatif!");
    }
    if (umur > 150) {
        throw string("Umur tidak realistis!");
    }
    cout << "Umur " << umur << " tahun valid." << endl;
}

// Fungsi yang melempar exception bertipe char*
void cekPassword(const string& password) {
    if (password.length() < 8) {
        throw "Password minimal 8 karakter!";
    }
    cout << "Password valid." << endl;
}

int main() {
    // Test 1: Exception bertipe int
    try {
        double hasil = hitungAkar(-25);
        cout << "Akar: " << hasil << endl;
    }
    catch (int kode) {
        cout << "Error dengan kode: " << kode << endl;
    }
    
    cout << endl;
    
    // Test 2: Exception bertipe string
    try {
        cekUmur(200);
    }
    catch (const string& pesan) {
        cout << "Error: " << pesan << endl;
    }
    
    cout << endl;
    
    // Test 3: Exception bertipe char*
    try {
        cekPassword("abc");
    }
    catch (const char* pesan) {
        cout << "Error: " << pesan << endl;
    }
    
    return 0;
}
```
*Contoh 14.15: Melempar exception dengan berbagai tipe data. Tipe exception harus sesuai dengan tipe yang ditangkap di catch block.*

### 14.7.4 Multiple Catch Blocks

Satu try block dapat memiliki beberapa catch block untuk menangani berbagai tipe exception yang berbeda. Catch block dievaluasi secara berurutan, dan yang pertama cocok yang akan dieksekusi.

```cpp
// Multiple catch blocks untuk menangani berbagai tipe exception
// Urutan catch block penting - yang lebih spesifik harus di atas
#include <iostream>
#include <string>
#include <stdexcept>
using namespace std;

void prosesNilai(int nilai) {
    if (nilai < 0) {
        throw runtime_error("Nilai tidak boleh negatif");
    }
    if (nilai > 100) {
        throw out_of_range("Nilai di luar rentang 0-100");
    }
    if (nilai == 0) {
        throw 0;  // Lempar integer
    }
    if (nilai == 13) {
        throw "Angka sial!";  // Lempar C-string
    }
    
    cout << "Nilai " << nilai << " valid dan diproses." << endl;
}

int main() {
    int nilaiTest[] = {50, -5, 150, 0, 13, 75};
    
    for (int nilai : nilaiTest) {
        cout << "Memproses nilai " << nilai << ": ";
        
        try {
            prosesNilai(nilai);
        }
        catch (const out_of_range& e) {
            cout << "[Out of Range] " << e.what() << endl;
        }
        catch (const runtime_error& e) {
            cout << "[Runtime Error] " << e.what() << endl;
        }
        catch (int kode) {
            cout << "[Integer Exception] Kode: " << kode << endl;
        }
        catch (const char* pesan) {
            cout << "[C-String Exception] " << pesan << endl;
        }
        catch (...) {
            // Catch-all handler
            cout << "[Unknown Exception]" << endl;
        }
    }
    
    return 0;
}
```
*Contoh 14.16: Multiple catch blocks untuk menangani berbagai tipe exception. Catch (...) adalah catch-all handler yang menangkap semua exception.*

### 14.7.5 Standard Exception Classes

C++ menyediakan hierarki class exception standar yang didefinisikan di header `<stdexcept>`. Class dasar adalah `std::exception` dengan fungsi virtual `what()` yang mengembalikan pesan error. Turunannya termasuk `logic_error` untuk error logika program (seperti `invalid_argument`, `out_of_range`, `domain_error`) dan `runtime_error` untuk error saat runtime (seperti `overflow_error`, `underflow_error`, `range_error`).

```cpp
// Menggunakan standard exception classes
// Memberikan informasi error yang lebih terstruktur
#include <iostream>
#include <stdexcept>
#include <string>
#include <vector>
using namespace std;

class RekeningBank {
private:
    string pemilik;
    double saldo;
    
public:
    RekeningBank(const string& nama, double saldoAwal) {
        if (saldoAwal < 0) {
            throw invalid_argument("Saldo awal tidak boleh negatif");
        }
        pemilik = nama;
        saldo = saldoAwal;
    }
    
    void setor(double jumlah) {
        if (jumlah <= 0) {
            throw invalid_argument("Jumlah setoran harus positif");
        }
        saldo += jumlah;
        cout << "Setor Rp " << jumlah << " berhasil. Saldo: Rp " << saldo << endl;
    }
    
    void tarik(double jumlah) {
        if (jumlah <= 0) {
            throw invalid_argument("Jumlah penarikan harus positif");
        }
        if (jumlah > saldo) {
            throw runtime_error("Saldo tidak mencukupi");
        }
        saldo -= jumlah;
        cout << "Tarik Rp " << jumlah << " berhasil. Saldo: Rp " << saldo << endl;
    }
    
    double getSaldo() const { return saldo; }
    string getPemilik() const { return pemilik; }
};

int main() {
    try {
        // Buat rekening
        RekeningBank rekening("Ahmad", 1000000);
        cout << "Rekening atas nama " << rekening.getPemilik() << " dibuat." << endl;
        cout << "Saldo awal: Rp " << rekening.getSaldo() << endl;
        cout << endl;
        
        // Operasi normal
        rekening.setor(500000);
        rekening.tarik(200000);
        
        cout << endl;
        
        // Operasi yang akan gagal
        cout << "Mencoba tarik Rp 2000000..." << endl;
        rekening.tarik(2000000);
        
    }
    catch (const invalid_argument& e) {
        cout << "Argument Error: " << e.what() << endl;
    }
    catch (const runtime_error& e) {
        cout << "Runtime Error: " << e.what() << endl;
    }
    catch (const exception& e) {
        cout << "Exception: " << e.what() << endl;
    }
    
    cout << "\nProgram selesai." << endl;
    
    return 0;
}
```
*Contoh 14.17: Menggunakan standard exception classes untuk error handling yang lebih terstruktur dalam simulasi rekening bank.*

## 14.8 Exception Handling dalam File Operations

### 14.8.1 Menangani Error File dengan Exception

Secara default, operasi file di C++ tidak melempar exception ketika terjadi error. Namun, kita dapat mengaktifkan exception dengan memanggil fungsi `exceptions()` pada stream object.

```cpp
// Mengaktifkan exception pada operasi file
// Memudahkan penanganan error yang lebih terstruktur
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main() {
    ifstream file;
    
    // Aktifkan exception untuk failbit dan badbit
    file.exceptions(ifstream::failbit | ifstream::badbit);
    
    try {
        // Mencoba membuka file yang tidak ada
        file.open("file_tidak_ada.txt");
        
        string baris;
        while (getline(file, baris)) {
            cout << baris << endl;
        }
        
        file.close();
    }
    catch (const ios_base::failure& e) {
        cout << "File Error: " << e.what() << endl;
        cout << "Pastikan file yang dimaksud ada dan dapat diakses." << endl;
    }
    
    cout << "\nProgram tetap berjalan." << endl;
    
    return 0;
}
```
*Contoh 14.18: Mengaktifkan dan menangani exception pada operasi file. Metode ini membuat penanganan error lebih eksplisit.*

### 14.8.2 Pola Penanganan File yang Robust

Berikut adalah contoh lengkap yang menggabungkan file handling dengan exception handling untuk membuat program yang robust.

```cpp
// Program CRUD sederhana dengan exception handling
// Menyimpan dan memuat data kontak ke/dari file
#include <iostream>
#include <fstream>
#include <string>
#include <vector>
#include <stdexcept>
#include <limits>
using namespace std;

struct Kontak {
    string nama;
    string telepon;
    string email;
};

class BukuAlamat {
private:
    vector<Kontak> daftarKontak;
    string namaFile;
    
public:
    BukuAlamat(const string& file) : namaFile(file) {
        muat();  // Coba muat data saat inisialisasi
    }
    
    void tambah(const Kontak& k) {
        if (k.nama.empty()) {
            throw invalid_argument("Nama tidak boleh kosong");
        }
        if (k.telepon.empty()) {
            throw invalid_argument("Telepon tidak boleh kosong");
        }
        daftarKontak.push_back(k);
        cout << "Kontak '" << k.nama << "' berhasil ditambahkan." << endl;
    }
    
    void tampilkan() const {
        if (daftarKontak.empty()) {
            cout << "Buku alamat kosong." << endl;
            return;
        }
        
        cout << "\n=== DAFTAR KONTAK ===" << endl;
        for (size_t i = 0; i < daftarKontak.size(); i++) {
            cout << i + 1 << ". " << daftarKontak[i].nama << endl;
            cout << "   Tel: " << daftarKontak[i].telepon << endl;
            cout << "   Email: " << daftarKontak[i].email << endl;
        }
        cout << "Total: " << daftarKontak.size() << " kontak" << endl;
    }
    
    void simpan() const {
        ofstream file(namaFile);
        
        if (!file.is_open()) {
            throw runtime_error("Gagal membuka file untuk menulis: " + namaFile);
        }
        
        for (const auto& k : daftarKontak) {
            file << k.nama << "|" << k.telepon << "|" << k.email << endl;
        }
        
        if (file.fail()) {
            throw runtime_error("Gagal menulis ke file: " + namaFile);
        }
        
        file.close();
        cout << "Data berhasil disimpan ke " << namaFile << endl;
    }
    
    void muat() {
        ifstream file(namaFile);
        
        if (!file.is_open()) {
            // File belum ada - bukan error, hanya tidak ada data
            cout << "File " << namaFile << " belum ada. Memulai dengan data kosong." << endl;
            return;
        }
        
        daftarKontak.clear();
        string baris;
        int barisKe = 0;
        
        while (getline(file, baris)) {
            barisKe++;
            
            // Parse baris dengan delimiter |
            size_t pos1 = baris.find('|');
            size_t pos2 = baris.find('|', pos1 + 1);
            
            if (pos1 == string::npos || pos2 == string::npos) {
                cerr << "Warning: Format tidak valid di baris " << barisKe << endl;
                continue;
            }
            
            Kontak k;
            k.nama = baris.substr(0, pos1);
            k.telepon = baris.substr(pos1 + 1, pos2 - pos1 - 1);
            k.email = baris.substr(pos2 + 1);
            
            daftarKontak.push_back(k);
        }
        
        file.close();
        cout << "Berhasil memuat " << daftarKontak.size() << " kontak dari " << namaFile << endl;
    }
    
    void hapus(int indeks) {
        if (indeks < 1 || indeks > (int)daftarKontak.size()) {
            throw out_of_range("Indeks tidak valid");
        }
        
        string namaHapus = daftarKontak[indeks - 1].nama;
        daftarKontak.erase(daftarKontak.begin() + indeks - 1);
        cout << "Kontak '" << namaHapus << "' berhasil dihapus." << endl;
    }
};

void tampilkanMenu() {
    cout << "\n=== BUKU ALAMAT ===" << endl;
    cout << "1. Tambah Kontak" << endl;
    cout << "2. Tampilkan Semua" << endl;
    cout << "3. Hapus Kontak" << endl;
    cout << "4. Simpan ke File" << endl;
    cout << "5. Muat dari File" << endl;
    cout << "0. Keluar" << endl;
    cout << "Pilihan: ";
}

int main() {
    try {
        BukuAlamat buku("kontak.txt");
        
        int pilihan;
        
        do {
            tampilkanMenu();
            cin >> pilihan;
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            
            try {
                switch (pilihan) {
                    case 1: {
                        Kontak k;
                        cout << "Nama: ";
                        getline(cin, k.nama);
                        cout << "Telepon: ";
                        getline(cin, k.telepon);
                        cout << "Email: ";
                        getline(cin, k.email);
                        buku.tambah(k);
                        break;
                    }
                    case 2:
                        buku.tampilkan();
                        break;
                    case 3: {
                        buku.tampilkan();
                        cout << "Nomor kontak yang akan dihapus: ";
                        int idx;
                        cin >> idx;
                        buku.hapus(idx);
                        break;
                    }
                    case 4:
                        buku.simpan();
                        break;
                    case 5:
                        buku.muat();
                        break;
                    case 0:
                        cout << "Terima kasih!" << endl;
                        break;
                    default:
                        cout << "Pilihan tidak valid!" << endl;
                }
            }
            catch (const invalid_argument& e) {
                cout << "Input Error: " << e.what() << endl;
            }
            catch (const out_of_range& e) {
                cout << "Range Error: " << e.what() << endl;
            }
            catch (const runtime_error& e) {
                cout << "Runtime Error: " << e.what() << endl;
            }
            
        } while (pilihan != 0);
        
    }
    catch (const exception& e) {
        cerr << "Fatal Error: " << e.what() << endl;
        return 1;
    }
    
    return 0;
}
```
*Contoh 14.19: Program CRUD lengkap dengan file handling dan exception handling. Program ini mendemonstrasikan praktik terbaik dalam menangani error.*

## 14.9 Best Practices

### 14.9.1 Defensive Programming

Defensive programming adalah praktik menulis kode yang mengantisipasi kemungkinan error sebelum terjadi. Prinsip utamanya adalah "never trust input" - selalu validasi data yang diterima dari pengguna, file, atau sumber eksternal lainnya.

```cpp
// Contoh defensive programming
// Selalu validasi input sebelum memproses
#include <iostream>
#include <fstream>
#include <string>
#include <limits>
using namespace std;

// Fungsi untuk membaca integer dengan validasi
int bacaInteger(const string& prompt, int min, int max) {
    int nilai;
    
    while (true) {
        cout << prompt;
        
        if (cin >> nilai) {
            if (nilai >= min && nilai <= max) {
                cin.ignore(numeric_limits<streamsize>::max(), '\n');
                return nilai;
            }
            cout << "Nilai harus antara " << min << " dan " << max << endl;
        } else {
            cout << "Input tidak valid. Masukkan angka!" << endl;
            cin.clear();  // Clear error flag
            cin.ignore(numeric_limits<streamsize>::max(), '\n');  // Buang input yang salah
        }
    }
}

// Fungsi untuk membaca string non-kosong
string bacaString(const string& prompt) {
    string nilai;
    
    while (true) {
        cout << prompt;
        getline(cin, nilai);
        
        // Trim whitespace
        size_t start = nilai.find_first_not_of(" \t");
        size_t end = nilai.find_last_not_of(" \t");
        
        if (start != string::npos) {
            return nilai.substr(start, end - start + 1);
        }
        
        cout << "Input tidak boleh kosong!" << endl;
    }
}

// Fungsi untuk membuka file dengan validasi
bool bukaFileDenganRetry(ifstream& file, const string& namaFile, int maxRetry) {
    for (int i = 0; i < maxRetry; i++) {
        file.open(namaFile);
        
        if (file.is_open()) {
            return true;
        }
        
        cout << "Gagal membuka " << namaFile << ". ";
        
        if (i < maxRetry - 1) {
            cout << "Mencoba lagi... (" << i + 2 << "/" << maxRetry << ")" << endl;
        }
    }
    
    return false;
}

int main() {
    cout << "=== Demo Defensive Programming ===" << endl;
    cout << endl;
    
    // Demo input integer dengan validasi
    int umur = bacaInteger("Masukkan umur (1-150): ", 1, 150);
    cout << "Umur yang dimasukkan: " << umur << endl;
    cout << endl;
    
    // Demo input string non-kosong
    string nama = bacaString("Masukkan nama: ");
    cout << "Nama yang dimasukkan: " << nama << endl;
    cout << endl;
    
    // Demo file dengan retry
    ifstream file;
    if (bukaFileDenganRetry(file, "config.txt", 3)) {
        cout << "File berhasil dibuka!" << endl;
        file.close();
    } else {
        cout << "Gagal membuka file setelah beberapa percobaan." << endl;
    }
    
    return 0;
}
```
*Contoh 14.20: Defensive programming dengan validasi input yang ketat dan mekanisme retry untuk operasi yang mungkin gagal.*

### 14.9.2 RAII (Resource Acquisition Is Initialization)

RAII adalah idiom C++ di mana resource (seperti file, memori, atau koneksi) diperoleh dalam constructor dan dilepaskan dalam destructor. Ini memastikan resource selalu dibersihkan dengan benar, bahkan jika terjadi exception.

```cpp
// Demonstrasi prinsip RAII
// Resource otomatis dibersihkan saat objek keluar dari scope
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

// Class sederhana yang mengimplementasikan RAII untuk file
class FileHandler {
private:
    ofstream file;
    string namaFile;
    
public:
    // Constructor: acquire resource
    FileHandler(const string& nama) : namaFile(nama) {
        file.open(namaFile);
        if (!file.is_open()) {
            throw runtime_error("Gagal membuka file: " + namaFile);
        }
        cout << "[FileHandler] File " << namaFile << " dibuka." << endl;
    }
    
    // Destructor: release resource
    ~FileHandler() {
        if (file.is_open()) {
            file.close();
            cout << "[FileHandler] File " << namaFile << " ditutup." << endl;
        }
    }
    
    // Operasi tulis
    void tulis(const string& data) {
        if (!file.is_open()) {
            throw runtime_error("File tidak terbuka");
        }
        file << data << endl;
    }
    
    // Prevent copying
    FileHandler(const FileHandler&) = delete;
    FileHandler& operator=(const FileHandler&) = delete;
};

void prosesData() {
    cout << "Memulai proses data..." << endl;
    
    // File akan otomatis ditutup saat handler keluar dari scope
    // bahkan jika terjadi exception
    FileHandler handler("log.txt");
    
    handler.tulis("Log entry 1");
    handler.tulis("Log entry 2");
    
    // Simulasi exception di tengah proses
    // Uncomment baris berikut untuk test:
    // throw runtime_error("Simulasi error!");
    
    handler.tulis("Log entry 3");
    
    cout << "Proses data selesai." << endl;
    
    // handler otomatis di-destroy di sini, file ditutup
}

int main() {
    try {
        prosesData();
    }
    catch (const exception& e) {
        cout << "Error: " << e.what() << endl;
    }
    
    cout << "\nProgram selesai." << endl;
    
    return 0;
}
```
*Contoh 14.21: Implementasi prinsip RAII dimana file otomatis ditutup saat objek FileHandler keluar dari scope.*

### 14.9.3 Tips Praktis File dan Exception Handling

Beberapa tips praktis yang perlu diingat saat bekerja dengan file dan exception di C++:

Untuk file handling, selalu periksa apakah file berhasil dibuka sebelum melakukan operasi. Tutup file segera setelah selesai digunakan. Gunakan mode pembukaan yang sesuai dengan kebutuhan. Pertimbangkan untuk menggunakan RAII atau smart pointer untuk manajemen resource otomatis. Untuk file penting, pertimbangkan membuat backup sebelum menulis.

Untuk exception handling, tangkap exception yang spesifik lebih dahulu, baru yang umum. Jangan tangkap exception hanya untuk diabaikan. Berikan pesan error yang informatif. Pertimbangkan untuk log exception untuk debugging. Bersihkan resource yang sudah dialokasi sebelum melempar ulang exception.

```cpp
// Program demonstrasi tips praktis
// Menggabungkan berbagai best practices
#include <iostream>
#include <fstream>
#include <string>
#include <ctime>
using namespace std;

// Fungsi untuk mendapatkan timestamp
string getTimestamp() {
    time_t now = time(0);
    char buf[80];
    strftime(buf, sizeof(buf), "%Y-%m-%d %H:%M:%S", localtime(&now));
    return string(buf);
}

// Fungsi untuk logging
void logError(const string& pesan) {
    ofstream logFile("error.log", ios::app);
    if (logFile.is_open()) {
        logFile << "[" << getTimestamp() << "] " << pesan << endl;
        logFile.close();
    }
}

// Fungsi untuk backup file
bool backupFile(const string& namaFile) {
    ifstream src(namaFile, ios::binary);
    if (!src.is_open()) {
        return false;  // File tidak ada, tidak perlu backup
    }
    
    string backupName = namaFile + ".bak";
    ofstream dst(backupName, ios::binary);
    
    if (!dst.is_open()) {
        src.close();
        return false;
    }
    
    dst << src.rdbuf();
    
    src.close();
    dst.close();
    
    return true;
}

// Fungsi utama yang mendemonstrasikan best practices
void prosesFile(const string& namaFile) {
    cout << "Memproses file: " << namaFile << endl;
    
    // 1. Backup file sebelum modifikasi
    if (backupFile(namaFile)) {
        cout << "Backup berhasil dibuat." << endl;
    }
    
    try {
        // 2. Buka file dengan pengecekan
        ifstream file(namaFile);
        if (!file.is_open()) {
            throw runtime_error("Tidak dapat membuka file: " + namaFile);
        }
        
        // 3. Proses file
        string baris;
        int jumlahBaris = 0;
        
        while (getline(file, baris)) {
            jumlahBaris++;
            // Proses setiap baris...
        }
        
        // 4. Tutup segera setelah selesai
        file.close();
        
        cout << "Berhasil memproses " << jumlahBaris << " baris." << endl;
        
    }
    catch (const exception& e) {
        // 5. Log error untuk debugging
        string pesanError = "Error saat memproses " + namaFile + ": " + e.what();
        logError(pesanError);
        
        // 6. Berikan pesan error yang informatif
        cerr << "Terjadi kesalahan: " << e.what() << endl;
        cerr << "Detail telah dicatat di error.log" << endl;
        
        // 7. Rethrow jika perlu ditangani di level atas
        throw;
    }
}

int main() {
    try {
        // Buat file test
        ofstream testFile("data.txt");
        testFile << "Baris 1" << endl;
        testFile << "Baris 2" << endl;
        testFile << "Baris 3" << endl;
        testFile.close();
        
        // Proses file
        prosesFile("data.txt");
        
        // Coba file yang tidak ada
        cout << "\nMencoba file yang tidak ada:" << endl;
        prosesFile("tidak_ada.txt");
        
    }
    catch (const exception& e) {
        cout << "Program error: " << e.what() << endl;
    }
    
    return 0;
}
```
*Contoh 14.22: Program yang mendemonstrasikan berbagai best practices dalam file dan exception handling.*

## 14.10 Ringkasan

Pada bab ini kita telah mempelajari dua konsep penting dalam pemrograman C++ yaitu file handling dan exception handling. File handling memungkinkan program kita untuk menyimpan dan membaca data secara permanen, sementara exception handling memungkinkan program menangani situasi error dengan elegan.

Untuk file handling, kita mempelajari konsep stream sebagai aliran data antara program dan file. C++ menyediakan tiga class utama yaitu ifstream untuk membaca, ofstream untuk menulis, dan fstream untuk keduanya. File dapat dibuka dengan berbagai mode seperti ios::in, ios::out, ios::app, dan ios::binary. Operasi baca dapat dilakukan dengan operator >>, getline(), atau get(), sedangkan operasi tulis dapat dilakukan dengan operator <<, put(), atau write(). Penting untuk selalu memeriksa status file dengan is_open(), eof(), fail(), dan good().

Untuk exception handling, kita mempelajari mekanisme try-catch-throw untuk menangani situasi abnormal. Try block berisi kode yang mungkin menghasilkan exception, catch block menangani exception yang dilempar, dan throw digunakan untuk melempar exception. C++ menyediakan hierarki exception standar seperti runtime_error, invalid_argument, dan out_of_range. Multiple catch blocks dapat digunakan untuk menangani berbagai tipe exception, dan catch(...) sebagai catch-all handler.

Best practices yang perlu diingat termasuk selalu validasi input (defensive programming), menggunakan RAII untuk manajemen resource otomatis, menangkap exception spesifik sebelum yang umum, memberikan pesan error yang informatif, dan melakukan logging untuk debugging.

## 14.11 Latihan

### Soal Latihan

1. Buatlah program yang membaca file teks dan menghitung jumlah kata, jumlah baris, dan jumlah karakter (tidak termasuk whitespace) dalam file tersebut. Program harus menangani kasus file tidak ditemukan dengan exception handling.

2. Buatlah program pencatat pengeluaran harian yang menyimpan data ke file CSV. Program harus memiliki fitur: tambah pengeluaran (tanggal, kategori, jumlah, keterangan), tampilkan semua pengeluaran, hitung total per kategori, dan simpan/muat dari file.

3. Buatlah fungsi template yang membaca array dari file. Fungsi harus dapat membaca array integer atau array float. Gunakan exception handling untuk menangani error format file.

4. Buatlah class Logger yang mengimplementasikan prinsip RAII. Class harus membuka file log saat konstruksi dan menutupnya saat destruksi. Sediakan method untuk menulis log dengan berbagai level (INFO, WARNING, ERROR).

5. Buatlah program yang menyalin file dengan progress indicator. Program harus menampilkan persentase progress saat menyalin file besar. Gunakan exception handling untuk menangani error seperti disk penuh atau permission denied.

6. Buatlah program enkripsi sederhana yang membaca file teks, mengenkripsi isinya dengan Caesar cipher, dan menyimpan ke file baru. Program juga harus bisa mendekripsi file yang sudah dienkripsi.

7. Buatlah program validasi data CSV yang membaca file mahasiswa (NIM, Nama, IPK) dan memeriksa: NIM harus 10 digit angka, Nama tidak boleh kosong, IPK harus antara 0.00 dan 4.00. Program harus melaporkan semua baris yang tidak valid.

8. Buatlah program merge sort untuk file besar. Baca dua file yang berisi angka yang sudah terurut, gabungkan menjadi satu file output yang juga terurut. Gunakan exception handling yang komprehensif.

### Soal Diskusi

1. Jelaskan perbedaan antara file teks dan file biner. Kapan sebaiknya menggunakan masing-masing jenis file? Berikan contoh kasus penggunaan konkret.

2. Mengapa penting untuk selalu menutup file setelah selesai digunakan? Apa yang bisa terjadi jika file tidak ditutup dengan benar?

3. Bandingkan penanganan error menggunakan return code tradisional dengan exception handling. Apa kelebihan dan kekurangan masing-masing pendekatan?

4. Jelaskan konsep RAII dan mengapa konsep ini penting dalam C++. Bagaimana RAII membantu mencegah resource leak?

5. Apa yang dimaksud dengan defensive programming? Berikan contoh praktik defensive programming dalam konteks file handling.

6. Jelaskan hierarki exception class standar di C++. Mengapa penting untuk menangkap exception yang lebih spesifik terlebih dahulu?

7. Diskusikan strategi backup dan recovery untuk aplikasi yang menyimpan data penting ke file. Bagaimana cara memastikan data tidak hilang jika terjadi crash?

8. Bagaimana cara menangani situasi ketika program harus memproses file yang sangat besar yang tidak muat di memori? Jelaskan teknik streaming dan buffering.

## 14.12 Referensi

1. Deitel, P., & Deitel, H. (2016). *C++ How to Program* (10th ed.). Pearson. Chapter 14: File Processing, Chapter 16: Exception Handling.

2. Savitch, W. (2018). *Problem Solving with C++* (10th ed.). Pearson. Chapter 12: Streams and File I/O, Chapter 16: Exception Handling.

3. Stroustrup, B. (2014). *Programming: Principles and Practice Using C++* (2nd ed.). Addison-Wesley. Chapter 5: Errors, Chapter 10: Input and Output Streams, Chapter 11: Customizing Input and Output.

4. Lippman, S. B., Lajoie, J., & Moo, B. E. (2012). *C++ Primer* (5th ed.). Addison-Wesley. Chapter 8: The IO Library, Chapter 18: Tools for Large Programs.

5. ISO/IEC 14882:2020. *Programming Languages — C++*. International Organization for Standardization.

6. cppreference.com. (2024). *C++ Reference Documentation*. https://en.cppreference.com/

7. Meyers, S. (2014). *Effective Modern C++*. O'Reilly Media. Item 13: Prefer const_iterators to iterators, Item 14: Declare functions noexcept if they won't emit exceptions.
