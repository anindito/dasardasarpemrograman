# Pertemuan 14: Pengenalan Pemrograman Berorientasi Objek (OOP)

## 📚 Deskripsi

Pertemuan ini memperkenalkan paradigma Pemrograman Berorientasi Objek (Object-Oriented Programming / OOP) dalam C++. Materi ini telah dipadatkan dari tiga pertemuan menjadi satu pertemuan fokus yang mencakup konsep dasar OOP tanpa topik lanjutan seperti operator overloading, friend functions, atau multiple inheritance.

## 🎯 Capaian Pembelajaran

Setelah mempelajari materi ini, mahasiswa diharapkan dapat:

1. Memahami perbedaan paradigma pemrograman prosedural dan berorientasi objek
2. Memahami dan menjelaskan empat pilar OOP (Encapsulation, Inheritance, Polymorphism, Abstraction)
3. Mendefinisikan dan menggunakan class dan object
4. Mengimplementasikan constructor dan destructor
5. Menerapkan enkapsulasi dengan access specifier (private, public, protected)
6. Memahami dan mengimplementasikan inheritance dasar
7. Memahami konsep polymorphism dengan virtual functions
8. Mengembangkan aplikasi sederhana menggunakan prinsip-prinsip OOP

## 📖 Materi

### 1. Paradigma Pemrograman
- Pemrograman Prosedural vs OOP
- Empat Pilar OOP:
  - Encapsulation (Enkapsulasi)
  - Inheritance (Pewarisan)
  - Polymorphism (Polimorfisme)
  - Abstraction (Abstraksi)

### 2. Class dan Object
- Pengertian dan perbedaan class vs object
- Sintaks definisi class
- Access specifier (private, public, protected)
- Data members dan member functions
- Membuat dan menggunakan object

### 3. Constructor dan Destructor
- Default constructor
- Parameterized constructor
- Constructor initializer list
- Destructor
- Urutan pemanggilan dalam inheritance

### 4. Encapsulation
- Konsep data hiding
- Getter dan setter methods
- Validasi data
- Keuntungan enkapsulasi

### 5. Inheritance
- Konsep pewarisan
- Base class dan derived class
- Sintaks inheritance
- Protected access specifier
- Constructor dalam inheritance
- Code reusability

### 6. Polymorphism
- Function overriding
- Virtual functions
- Runtime polymorphism
- Virtual destructor
- Keyword override (C++11)

### 7. Contoh Aplikasi
- Sistem perpustakaan sederhana
- Demonstrasi empat pilar OOP
- Best practices

## 📂 File dalam Folder Ini

- `Bahan_Ajar_Pertemuan_14.md` - Bahan ajar lengkap dalam format Markdown
- `Slide_Pertemuan_14.html` - Slide presentasi menggunakan Reveal.js
- `README.md` - File ini

## 🔑 Konsep Kunci

### Class vs Object
```cpp
// Class = Blueprint
class Mahasiswa {
private:
    string nama;
    float ipk;
public:
    Mahasiswa(string n, float i) : nama(n), ipk(i) {}
};

// Object = Instance
Mahasiswa mhs1("Budi", 3.75);  // Object pertama
Mahasiswa mhs2("Ani", 3.25);   // Object kedua
```

### Encapsulation
```cpp
class Mahasiswa {
private:
    float ipk;  // Data hidden
    
public:
    // Getter
    float getIPK() { return ipk; }
    
    // Setter dengan validasi
    void setIPK(float i) {
        if (i >= 0.0 && i <= 4.0) {
            ipk = i;
        } else {
            cout << "IPK tidak valid!" << endl;
        }
    }
};
```

### Inheritance
```cpp
// Base class
class Person {
protected:
    string nama;
public:
    Person(string n) : nama(n) {}
};

// Derived class
class Mahasiswa : public Person {
private:
    string nim;
public:
    Mahasiswa(string n, string ni) : Person(n), nim(ni) {}
};
```

### Polymorphism
```cpp
class BangunDatar {
public:
    virtual double hitungLuas() { return 0.0; }
};

class Persegi : public BangunDatar {
private:
    double sisi;
public:
    double hitungLuas() override {
        return sisi * sisi;
    }
};

// Runtime polymorphism
BangunDatar* bentuk = new Persegi(5.0);
cout << bentuk->hitungLuas();  // Memanggil method Persegi
```

## ⚠️ Topik yang TIDAK Dibahas (Akan Dipelajari di Mata Kuliah PBO)

Pertemuan ini adalah pengenalan dasar OOP. Topik-topik berikut **tidak dibahas** dan akan dipelajari di mata kuliah Pemrograman Berorientasi Objek:

- Operator overloading
- Friend functions dan friend classes
- Multiple inheritance
- Virtual functions secara mendalam
- Abstract classes dan pure virtual functions
- RTTI (Runtime Type Information)
- Design patterns
- SOLID principles
- STL (Standard Template Library) secara mendalam

## 💡 Tips Belajar

1. **Pahami Konsep, Bukan Hafal Syntax**
   - Fokus pada pemahaman empat pilar OOP
   - Pahami kapan menggunakan OOP vs prosedural

2. **Praktik dengan Contoh Sederhana**
   - Mulai dengan class sederhana (Mahasiswa, Mobil, dll)
   - Bertahap ke aplikasi yang lebih kompleks

3. **Perhatikan Access Specifier**
   - Data members → private
   - Interface methods → public
   - Helper methods → private

4. **Jangan Lupa Virtual Destructor**
   - Jika ada virtual function, destructor harus virtual
   - Penting untuk polymorphism yang benar

5. **Gunakan Initializer List**
   - Lebih efisien untuk constructor
   - Wajib untuk const members dan references

## 🔗 Referensi Utama

1. **Stroustrup, B.** (2013). *The C++ Programming Language* (4th ed.). Addison-Wesley.
   - Chapter 2-3: Classes and Inheritance

2. **Savitch, W.** (2017). *Problem Solving with C++* (10th ed.). Pearson.
   - Chapter 10-11: Defining Classes and Inheritance

3. **Lippman, S. B., Lajoie, J., & Moo, B. E.** (2012). *C++ Primer* (5th ed.). Addison-Wesley.
   - Chapter 7, 13, 15: Classes, Copy Control, OOP

4. **Deitel, P., & Deitel, H.** (2016). *C++ How to Program* (10th ed.). Pearson.
   - Chapter 9, 12: Classes and Objects, OOP

## 🎓 Catatan Penting

- **Pertemuan ini adalah pengenalan** - Konsep OOP sangat luas dan akan diperdalam di mata kuliah PBO
- **Fokus pada fondasi** - Pahami dengan baik empat pilar OOP sebagai bekal untuk pembelajaran lanjutan
- **Practice makes perfect** - OOP memerlukan banyak latihan untuk benar-benar memahami konsepnya
- **Think in objects** - Mulai berpikir dalam terms of objects dan interactions, bukan hanya functions dan data

## 📝 Latihan Mandiri

Untuk memperdalam pemahaman, cobalah:

1. Buat hierarki class untuk sistem akademik (Civitas, Dosen, Mahasiswa, Staff)
2. Implementasikan sistem toko online sederhana dengan class Produk, Keranjang, Transaksi
3. Buat class diagram untuk sistem yang Anda buat
4. Refactor program prosedural yang pernah Anda buat ke paradigma OOP

## ⏭️ Pertemuan Selanjutnya

**Pertemuan 15: File Handling dan Exception Handling**
- Stream classes (ifstream, ofstream, fstream)
- Membaca dan menulis file
- Exception handling dengan try-catch
- Best practices untuk error handling

---

📧 **Pertanyaan?** Silakan hubungi dosen atau asisten praktikum.

💻 **Repository:** [Link ke repository GitHub]
