# Worksheet Lab: Pengenalan OOP
## Pertemuan 14 - Dasar-Dasar Pemrograman

**Nama:** ___________________________  
**NIM:** ___________________________  
**Kelas:** ___________________________  
**Tanggal:** ___________________________

---

## Tujuan Praktikum

Setelah menyelesaikan praktikum ini, mahasiswa diharapkan dapat:
1. Membuat dan menggunakan class dan object dalam C++
2. Mengimplementasikan enkapsulasi dengan access specifier
3. Membuat constructor dan destructor
4. Mengimplementasikan inheritance
5. Memahami dan menggunakan polymorphism dengan virtual functions
6. Mengintegrasikan semua konsep OOP dalam aplikasi sederhana

---

## Persiapan

### Software yang Diperlukan:
- Compiler C++ (MinGW/GCC/Visual Studio)
- Text editor atau IDE (VS Code/Code::Blocks/Dev-C++)

### Pengetahuan Prasyarat:
- Sintaks dasar C++
- Fungsi dan parameter
- Struct (akan dikembangkan menjadi class)

---

## Bagian 1: Memahami Class dan Object (30 menit)

### Tugas 1.1: Membuat Class Pertama

Buatlah program dengan class `Mahasiswa` berikut:

```cpp
#include <iostream>
#include <string>
using namespace std;

class Mahasiswa {
private:
    string nama;
    string nim;
    float ipk;

public:
    // TODO: Lengkapi method-method berikut
    void setData(string n, string ni, float i) {
        // Isi implementasi
    }
    
    void tampilkan() {
        // Isi implementasi
    }
};

int main() {
    Mahasiswa mhs1;
    mhs1.setData("Budi Santoso", "2101001", 3.75);
    mhs1.tampilkan();
    
    return 0;
}
```

**Langkah-langkah:**
1. Lengkapi implementasi method `setData()`
2. Lengkapi implementasi method `tampilkan()`
3. Compile dan jalankan program
4. Ambil screenshot output

**Screenshot Output:**  
[Tempelkan screenshot di sini]

**Pertanyaan Refleksi:**
1. Apa perbedaan antara class dan struct?
   
   Jawaban: _______________________________________________

2. Mengapa atribut dibuat private?
   
   Jawaban: _______________________________________________

---

### Tugas 1.2: Multiple Objects

Modifikasi program di atas untuk membuat 3 object Mahasiswa dengan data berbeda. Tampilkan informasi ketiga mahasiswa.

**Screenshot Output:**  
[Tempelkan screenshot di sini]

**Pertanyaan:**
1. Apakah ketiga object memiliki data yang independen?
   
   Jawaban: _______________________________________________

2. Apa yang terjadi jika Anda mengubah data mhs1, apakah mempengaruhi mhs2?
   
   Jawaban: _______________________________________________

---

## Bagian 2: Enkapsulasi dan Validasi (30 menit)

### Tugas 2.1: Getter dan Setter

Tambahkan getter dan setter ke class Mahasiswa:

```cpp
class Mahasiswa {
private:
    string nama;
    string nim;
    float ipk;

public:
    // Getter methods
    string getNama() {
        return nama;
    }
    
    string getNim() {
        // TODO: Implementasi
    }
    
    float getIPK() {
        // TODO: Implementasi
    }
    
    // Setter methods dengan validasi
    void setNama(string n) {
        if (n.length() > 0) {
            nama = n;
        } else {
            cout << "Error: Nama tidak boleh kosong!" << endl;
        }
    }
    
    void setNIM(string ni) {
        // TODO: Validasi NIM harus 7 karakter
    }
    
    void setIPK(float i) {
        // TODO: Validasi IPK harus 0.0 - 4.0
    }
};
```

**Lengkapi kode di atas dan test dengan:**
- Input NIM yang valid dan tidak valid
- Input IPK yang valid dan tidak valid

**Screenshot Output Testing:**  
[Tempelkan screenshot di sini]

**Pertanyaan:**
1. Apa keuntungan validasi di setter dibanding validasi di luar class?
   
   Jawaban: _______________________________________________

---

### Tugas 2.2: Enkapsulasi Penuh

Buatlah class `RekeningBank` dengan enkapsulasi penuh:

```cpp
class RekeningBank {
private:
    string nomorRekening;
    string namaPemilik;
    double saldo;

public:
    // Constructor
    RekeningBank(string nomor, string nama, double saldoAwal) {
        nomorRekening = nomor;
        namaPemilik = nama;
        saldo = saldoAwal;
    }
    
    // Method setor
    void setor(double jumlah) {
        // TODO: Implementasi
        // Validasi: jumlah harus positif
    }
    
    // Method tarik
    void tarik(double jumlah) {
        // TODO: Implementasi
        // Validasi: saldo harus mencukupi
    }
    
    // Method tampilkan info
    void tampilkanInfo() {
        // TODO: Implementasi
    }
    
    // Getter
    double getSaldo() {
        return saldo;
    }
};
```

**Test case:**
1. Buat rekening dengan saldo awal 1000000
2. Setor 500000
3. Tarik 200000
4. Coba tarik 2000000 (harus gagal)
5. Tampilkan info akhir

**Screenshot Output:**  
[Tempelkan screenshot di sini]

---

## Bagian 3: Constructor dan Destructor (25 menit)

### Tugas 3.1: Constructor Berbeda

Buatlah class `Produk` dengan multiple constructors:

```cpp
class Produk {
private:
    string kode;
    string nama;
    double harga;
    int stok;

public:
    // Default constructor
    Produk() {
        kode = "P0000";
        nama = "Produk Kosong";
        harga = 0.0;
        stok = 0;
        cout << "Default constructor dipanggil" << endl;
    }
    
    // Parameterized constructor
    Produk(string k, string n, double h, int s) 
        : kode(k), nama(n), harga(h), stok(s) {
        cout << "Parameterized constructor dipanggil untuk " << nama << endl;
    }
    
    // Destructor
    ~Produk() {
        cout << "Destructor dipanggil untuk " << nama << endl;
    }
    
    void tampilkan() {
        cout << "\nKode: " << kode << endl;
        cout << "Nama: " << nama << endl;
        cout << "Harga: Rp " << harga << endl;
        cout << "Stok: " << stok << endl;
    }
};
```

**Test dengan:**
```cpp
int main() {
    {
        Produk p1;
        p1.tampilkan();
    } // p1 keluar dari scope
    
    cout << "\n=== Membuat produk dengan parameter ===" << endl;
    
    {
        Produk p2("P001", "Laptop", 5000000, 10);
        p2.tampilkan();
    } // p2 keluar dari scope
    
    return 0;
}
```

**Screenshot Output:**  
[Tempelkan screenshot di sini]

**Pertanyaan:**
1. Kapan constructor dipanggil?
   
   Jawaban: _______________________________________________

2. Kapan destructor dipanggil?
   
   Jawaban: _______________________________________________

3. Apa perbedaan constructor dengan initializer list dan assignment biasa?
   
   Jawaban: _______________________________________________

---

## Bagian 4: Inheritance (35 menit)

### Tugas 4.1: Basic Inheritance

Buatlah hierarki class berikut:

```cpp
// Base class
class Person {
protected:
    string nama;
    int umur;

public:
    Person(string n, int u) : nama(n), umur(u) {
        cout << "Constructor Person: " << nama << endl;
    }
    
    void tampilkanInfo() {
        cout << "Nama: " << nama << endl;
        cout << "Umur: " << umur << " tahun" << endl;
    }
    
    ~Person() {
        cout << "Destructor Person: " << nama << endl;
    }
};

// Derived class
class Mahasiswa : public Person {
private:
    string nim;
    string jurusan;
    float ipk;

public:
    // TODO: Buat constructor yang memanggil base class constructor
    Mahasiswa(string n, int u, string ni, string j, float i) 
        : /* TODO */ {
        // TODO: Inisialisasi member derived class
        cout << "Constructor Mahasiswa" << endl;
    }
    
    // TODO: Override method tampilkanInfo
    void tampilkanInfo() {
        // TODO: Panggil base class method
        // TODO: Tampilkan info tambahan
    }
    
    string hitungPredikat() {
        // TODO: Implementasi
    }
    
    ~Mahasiswa() {
        cout << "Destructor Mahasiswa" << endl;
    }
};
```

**Lengkapi code di atas dan test dengan:**
```cpp
int main() {
    cout << "=== Membuat object Mahasiswa ===" << endl;
    {
        Mahasiswa mhs("Budi Santoso", 20, "2101001", "Informatika", 3.75);
        mhs.tampilkanInfo();
        cout << "Predikat: " << mhs.hitungPredikat() << endl;
    }
    cout << "=== Object keluar dari scope ===" << endl;
    
    return 0;
}
```

**Screenshot Output:**  
[Tempelkan screenshot di sini]

**Pertanyaan:**
1. Apa urutan pemanggilan constructor?
   
   Jawaban: _______________________________________________

2. Apa urutan pemanggilan destructor?
   
   Jawaban: _______________________________________________

3. Mengapa atribut di base class menggunakan protected, bukan private?
   
   Jawaban: _______________________________________________

---

### Tugas 4.2: Hierarchical Inheritance

Buatlah hierarki berikut:

```
       Kendaraan
       /       \
    Mobil     Motor
```

**Implementasi:**

```cpp
class Kendaraan {
protected:
    string merk;
    int tahun;
    string warna;

public:
    Kendaraan(string m, int t, string w) 
        : merk(m), tahun(t), warna(w) {}
    
    void tampilkanInfo() {
        cout << "Merk: " << merk << endl;
        cout << "Tahun: " << tahun << endl;
        cout << "Warna: " << warna << endl;
    }
};

class Mobil : public Kendaraan {
private:
    int jumlahPintu;
    string jenisBahanBakar;

public:
    // TODO: Constructor
    
    // TODO: Override tampilkanInfo
};

class Motor : public Kendaraan {
private:
    string jenisMotor; // bebek/sport/matic

public:
    // TODO: Constructor
    
    // TODO: Override tampilkanInfo
};
```

**Test dengan membuat 1 object Mobil dan 1 object Motor.**

**Screenshot Output:**  
[Tempelkan screenshot di sini]

---

## Bagian 5: Polymorphism (40 menit)

### Tugas 5.1: Function Overriding

Buatlah program dengan function overriding:

```cpp
class BangunDatar {
protected:
    string nama;

public:
    BangunDatar(string n) : nama(n) {}
    
    void hitungLuas() {
        cout << "Luas belum didefinisikan untuk " << nama << endl;
    }
};

class Persegi : public BangunDatar {
private:
    double sisi;

public:
    Persegi(double s) : BangunDatar("Persegi"), sisi(s) {}
    
    void hitungLuas() {
        cout << "Luas persegi: " << (sisi * sisi) << " cm²" << endl;
    }
};

// TODO: Buat class Lingkaran yang override hitungLuas
// TODO: Buat class Segitiga yang override hitungLuas
```

**Screenshot Output:**  
[Tempelkan screenshot di sini]

**Pertanyaan:**
Tanpa keyword `virtual`, apakah ini sudah polymorphism? Jelaskan!

Jawaban: _______________________________________________

---

### Tugas 5.2: Virtual Functions dan Runtime Polymorphism

Modifikasi program di atas dengan menambahkan keyword `virtual`:

```cpp
class BangunDatar {
protected:
    string nama;

public:
    BangunDatar(string n) : nama(n) {}
    
    // Tambahkan virtual
    virtual void hitungLuas() {
        cout << "Luas belum didefinisikan untuk " << nama << endl;
    }
    
    virtual ~BangunDatar() {}
};

class Persegi : public BangunDatar {
private:
    double sisi;

public:
    Persegi(double s) : BangunDatar("Persegi"), sisi(s) {}
    
    void hitungLuas() override {
        cout << "Luas persegi: " << (sisi * sisi) << " cm²" << endl;
    }
};

// Lengkapi class Lingkaran dan Segitiga
```

**Test dengan polymorphism:**

```cpp
int main() {
    // Array of pointers ke base class
    BangunDatar* bentuk[3];
    
    bentuk[0] = new Persegi(5.0);
    bentuk[1] = new Lingkaran(7.0);
    bentuk[2] = new Segitiga(4.0, 6.0);
    
    // Polymorphism!
    cout << "=== Menghitung Luas dengan Polymorphism ===" << endl;
    for (int i = 0; i < 3; i++) {
        bentuk[i]->hitungLuas();
    }
    
    // Cleanup
    for (int i = 0; i < 3; i++) {
        delete bentuk[i];
    }
    
    return 0;
}
```

**Screenshot Output:**  
[Tempelkan screenshot di sini]

**Pertanyaan:**
1. Apa perbedaan output dengan dan tanpa keyword virtual?
   
   Jawaban: _______________________________________________

2. Mengapa destructor harus virtual?
   
   Jawaban: _______________________________________________

---

## Bagian 6: Aplikasi Terintegrasi (50 menit)

### Tugas 6: Sistem Perpustakaan Sederhana

Buatlah sistem perpustakaan dengan struktur berikut:

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

// Base class
class ItemPerpustakaan {
protected:
    string kode;
    string judul;
    bool dipinjam;

public:
    ItemPerpustakaan(string k, string j) 
        : kode(k), judul(j), dipinjam(false) {}
    
    virtual void tampilkanInfo() {
        cout << "Kode: " << kode << endl;
        cout << "Judul: " << judul << endl;
        cout << "Status: " << (dipinjam ? "Dipinjam" : "Tersedia") << endl;
    }
    
    virtual string getTipe() {
        return "Item Umum";
    }
    
    void pinjam() {
        if (!dipinjam) {
            dipinjam = true;
            cout << "Item berhasil dipinjam." << endl;
        } else {
            cout << "Item sedang dipinjam!" << endl;
        }
    }
    
    void kembalikan() {
        if (dipinjam) {
            dipinjam = false;
            cout << "Item berhasil dikembalikan." << endl;
        } else {
            cout << "Item tidak sedang dipinjam!" << endl;
        }
    }
    
    bool isDipinjam() { return dipinjam; }
    string getKode() { return kode; }
    
    virtual ~ItemPerpustakaan() {}
};

// TODO: Derived class Buku
class Buku : public ItemPerpustakaan {
private:
    string pengarang;
    int tahunTerbit;

public:
    // TODO: Constructor
    
    // TODO: Override tampilkanInfo()
    
    // TODO: Override getTipe()
};

// TODO: Derived class Majalah
class Majalah : public ItemPerpustakaan {
private:
    string penerbit;
    int edisi;

public:
    // TODO: Constructor
    
    // TODO: Override tampilkanInfo()
    
    // TODO: Override getTipe()
};

// Class Perpustakaan
class Perpustakaan {
private:
    vector<ItemPerpustakaan*> koleksi;
    string namaPerpustakaan;

public:
    Perpustakaan(string nama) : namaPerpustakaan(nama) {}
    
    void tambahItem(ItemPerpustakaan* item) {
        koleksi.push_back(item);
        cout << "Item " << item->getKode() << " ditambahkan." << endl;
    }
    
    void tampilkanSemuaItem() {
        // TODO: Implementasi
    }
    
    ItemPerpustakaan* cariItem(string kode) {
        // TODO: Implementasi
    }
    
    ~Perpustakaan() {
        for (size_t i = 0; i < koleksi.size(); i++) {
            delete koleksi[i];
        }
    }
};
```

**Lengkapi implementasi di atas dan buat main() yang:**
1. Membuat perpustakaan
2. Menambah minimal 2 buku dan 2 majalah
3. Menampilkan semua koleksi
4. Meminjam 2 item
5. Menampilkan item yang masih tersedia
6. Mengembalikan 1 item
7. Menampilkan item yang masih tersedia lagi

**Screenshot Output Lengkap:**  
[Tempelkan screenshot di sini]

---

## Checklist Penyelesaian

Tandai (✓) setelah menyelesaikan setiap bagian:

- [ ] Bagian 1: Class dan Object
  - [ ] Tugas 1.1: Membuat class pertama
  - [ ] Tugas 1.2: Multiple objects

- [ ] Bagian 2: Enkapsulasi
  - [ ] Tugas 2.1: Getter dan Setter
  - [ ] Tugas 2.2: Enkapsulasi penuh (RekeningBank)

- [ ] Bagian 3: Constructor dan Destructor
  - [ ] Tugas 3.1: Multiple constructors

- [ ] Bagian 4: Inheritance
  - [ ] Tugas 4.1: Basic inheritance (Person-Mahasiswa)
  - [ ] Tugas 4.2: Hierarchical inheritance (Kendaraan)

- [ ] Bagian 5: Polymorphism
  - [ ] Tugas 5.1: Function overriding
  - [ ] Tugas 5.2: Virtual functions

- [ ] Bagian 6: Aplikasi Terintegrasi
  - [ ] Tugas 6: Sistem perpustakaan

---

## Refleksi Akhir

1. **Konsep apa yang paling sulit dipahami dalam praktikum ini?**
   
   Jawaban: _______________________________________________
   _______________________________________________

2. **Bagaimana OOP membuat program lebih terorganisir dibanding pendekatan prosedural?**
   
   Jawaban: _______________________________________________
   _______________________________________________

3. **Dalam skenario apa Anda akan memilih menggunakan inheritance vs composition?**
   
   Jawaban: _______________________________________________
   _______________________________________________

4. **Apa keuntungan utama dari polymorphism dalam pengembangan software?**
   
   Jawaban: _______________________________________________
   _______________________________________________

---

## Submission

**File yang harus dikumpulkan:**
1. Source code semua tugas (format: NIM_Nama_Pertemuan14.cpp)
2. Screenshot output setiap tugas
3. Worksheet ini yang sudah diisi lengkap (format PDF)

**Deadline:** _______________

**Nilai:** _____ / 100

**Catatan Asisten:**

_______________________________________________
_______________________________________________
_______________________________________________

---

**Selamat Mengerjakan! 🚀**

OOP adalah paradigma yang powerful. Praktik terus menerus akan membuat Anda mahir!
