# Latihan Drill: Pengenalan OOP
## Pertemuan 14 - Dasar-Dasar Pemrograman

---

## Petunjuk Umum

Latihan drill ini dirancang untuk membantu Anda memahami konsep dasar OOP melalui latihan terstruktur dari yang mudah hingga menantang. Kerjakan soal-soal berikut secara berurutan.

---

## Bagian 1: Class dan Object Dasar (15 soal)

### Soal 1: Definisi Class Sederhana
Buatlah class `Buku` dengan atribut private: judul, pengarang, dan tahunTerbit. Tambahkan method public `tampilkanInfo()` untuk menampilkan informasi buku.

**Input yang diharapkan:**
```cpp
// Dalam main()
Buku buku1;
buku1.setData("C++ Programming", "Bjarne Stroustrup", 2013);
buku1.tampilkanInfo();
```

**Output yang diharapkan:**
```
Judul: C++ Programming
Pengarang: Bjarne Stroustrup
Tahun Terbit: 2013
```

---

### Soal 2: Multiple Objects
Menggunakan class `Buku` dari soal 1, buatlah 3 object berbeda dengan data yang berbeda-beda. Tampilkan informasi dari ketiga buku tersebut.

---

### Soal 3: Access Specifier
Jelaskan apa yang terjadi jika kita mencoba mengakses atribut private secara langsung dari main():
```cpp
Buku buku1;
buku1.judul = "Test";  // Apa yang terjadi?
```

Perbaiki code di atas agar dapat berfungsi dengan benar tanpa melanggar prinsip enkapsulasi.

---

### Soal 4: Class Mahasiswa
Buatlah class `Mahasiswa` dengan:
- Atribut private: nama, nim, jurusan, ipk
- Method public: setData(), getNama(), getNim(), getIPK()
- Method tampilkan() untuk menampilkan semua informasi

---

### Soal 5: Validasi dalam Setter
Tambahkan method `setIPK(float ipk)` pada class `Mahasiswa` yang memvalidasi bahwa IPK harus antara 0.0 hingga 4.0. Jika tidak valid, tampilkan pesan error dan jangan ubah nilai IPK.

---

### Soal 6: Method Perhitungan
Tambahkan method `string hitungPredikat()` pada class `Mahasiswa` yang mengembalikan:
- "Cum Laude" jika IPK >= 3.5
- "Sangat Memuaskan" jika IPK >= 3.0
- "Memuaskan" jika IPK >= 2.75
- "Cukup" jika IPK < 2.75

---

### Soal 7: Class Lingkaran
Buatlah class `Lingkaran` dengan:
- Atribut private: jariJari
- Constructor untuk inisialisasi jariJari
- Method hitungLuas() yang mengembalikan luas lingkaran (π × r²)
- Method hitungKeliling() yang mengembalikan keliling lingkaran (2 × π × r)

Gunakan nilai π = 3.14159

---

### Soal 8: Class Persegi
Buatlah class `Persegi` dengan:
- Atribut private: sisi
- Constructor untuk inisialisasi sisi
- Method hitungLuas()
- Method hitungKeliling()
- Method tampilkanInfo() yang menampilkan sisi, luas, dan keliling

---

### Soal 9: Class RekeningBank
Buatlah class `RekeningBank` dengan:
- Atribut private: nomorRekening, namaPemilik, saldo
- Constructor untuk inisialisasi
- Method setor(double jumlah) untuk menambah saldo
- Method tarik(double jumlah) untuk mengurangi saldo (validasi saldo mencukupi)
- Method getSaldo() untuk mendapatkan saldo
- Method tampilkanInfo()

---

### Soal 10: Enkapsulasi Penuh
Pada class `RekeningBank` soal 9, pastikan semua atribut private dan hanya dapat diakses melalui getter/setter. Implementasikan validasi:
- Nama pemilik tidak boleh kosong
- Nomor rekening harus 10 digit
- Saldo awal tidak boleh negatif

---

### Soal 11: Class Karyawan
Buatlah class `Karyawan` dengan:
- Atribut private: nama, id, gajiPokok, tunjangan
- Method hitungGajiTotal() yang mengembalikan gajiPokok + tunjangan
- Method tampilkanInfo()
- Getter dan setter untuk semua atribut dengan validasi yang sesuai

---

### Soal 12: Array of Objects
Buatlah array yang berisi 5 object `Mahasiswa`. Isi dengan data, lalu tampilkan mahasiswa dengan IPK tertinggi.

---

### Soal 13: Pencarian dalam Array Objects
Dari array 5 mahasiswa di soal 12, buatlah fungsi `cariMahasiswaNIM(string nim)` yang mencari dan mengembalikan pointer ke mahasiswa dengan NIM tertentu. Jika tidak ditemukan, return nullptr.

---

### Soal 14: Class Tanggal
Buatlah class `Tanggal` dengan:
- Atribut private: hari, bulan, tahun
- Constructor untuk inisialisasi
- Method validasi() yang memeriksa apakah tanggal valid
- Method tampilkan() yang menampilkan format: DD/MM/YYYY
- Method hitungSelisihHari(Tanggal lain) untuk menghitung selisih hari

---

### Soal 15: Class Waktu
Buatlah class `Waktu` dengan:
- Atribut private: jam, menit, detik
- Constructor untuk inisialisasi
- Method tambahDetik(int detik) yang menambahkan detik dan update jam/menit jika perlu
- Method selisihWaktu(Waktu lain) yang mengembalikan selisih dalam detik
- Method tampilkan() format: HH:MM:SS

---

## Bagian 2: Constructor dan Destructor (10 soal)

### Soal 16: Default Constructor
Buatlah class `Mahasiswa` yang memiliki:
- Default constructor yang menginisialisasi semua atribut dengan nilai default
- Parameterized constructor yang menerima semua parameter
- Destructor yang menampilkan pesan "Object [nama] dihancurkan"

**Output yang diharapkan:**
```cpp
{
    Mahasiswa mhs1;  // Menggunakan default constructor
    Mahasiswa mhs2("Budi", "2101001", 3.5);  // Parameterized
} // Di sini destructor dipanggil
```

---

### Soal 17: Constructor Initializer List
Ubah constructor pada soal 16 untuk menggunakan initializer list. Bandingkan efisiensinya dengan assignment dalam body constructor.

---

### Soal 18: Constructor Overloading
Buatlah class `Produk` dengan 3 constructor:
1. Default constructor
2. Constructor dengan parameter (kode, nama)
3. Constructor dengan parameter (kode, nama, harga, stok)

Demonstrasikan penggunaan ketiga constructor.

---

### Soal 19: Destructor dengan Resource
Buatlah class `DynamicArray` yang:
- Mengalokasikan array dinamis dalam constructor
- Menyimpan data ke array
- Dealokasikan array dalam destructor
- Tampilkan pesan saat alokasi dan dealokasi

---

### Soal 20: Copy Constructor (Opsional)
Buatlah class `Kotak` dengan atribut panjang, lebar, tinggi. Implementasikan:
- Default constructor
- Parameterized constructor
- Copy constructor
- Destructor

Demonstrasikan deep copy vs shallow copy.

---

### Soal 21: Constructor Chaining
Buatlah class `Person` dengan:
- Constructor dengan 1 parameter (nama)
- Constructor dengan 2 parameter (nama, umur) yang memanggil constructor pertama
- Constructor dengan 3 parameter (nama, umur, alamat) yang memanggil constructor kedua

---

### Soal 22: Const Members
Buatlah class `Segitiga` dengan atribut const untuk alas dan tinggi. Inisialisasi harus menggunakan initializer list. Jelaskan mengapa tidak bisa menggunakan assignment dalam body constructor.

---

### Soal 23: Static Members
Buatlah class `Mahasiswa` dengan static member `jumlahMahasiswa` yang menghitung berapa banyak object Mahasiswa yang pernah dibuat. Update di constructor, kurangi di destructor.

---

### Soal 24: Constructor dengan Validasi
Buatlah class `RekeningBank` yang melakukan validasi di constructor. Jika data tidak valid, lempar exception atau set ke nilai default dan tampilkan warning.

---

### Soal 25: Explicit Constructor
Buatlah class `Nilai` dengan constructor explicit untuk mencegah implicit conversion. Jelaskan perbedaan behavior dengan dan tanpa keyword explicit.

---

## Bagian 3: Inheritance (15 soal)

### Soal 26: Basic Inheritance
Buatlah:
- Base class `Kendaraan` dengan atribut merk dan tahun
- Derived class `Mobil` yang menambahkan atribut jumlahPintu
- Demonstrasikan pembuatan object dan akses ke atribut yang diwarisi

---

### Soal 27: Protected vs Private
Jelaskan perbedaan akses ke member yang private vs protected dalam inheritance. Buat contoh yang mendemonstrasikan kedua kasus.

---

### Soal 28: Constructor dalam Inheritance
Buatlah hierarki:
```
Person (nama, umur)
    |
Mahasiswa (nama, umur, nim, jurusan)
```

Implementasikan constructor untuk kedua class dan demonstrasikan urutan pemanggilan.

---

### Soal 29: Destructor dalam Inheritance
Tambahkan destructor pada hierarki soal 28. Tampilkan pesan di setiap destructor untuk melihat urutan pemanggilan.

---

### Soal 30: Method Overriding
Buatlah base class `BangunDatar` dengan method `hitungLuas()`. Buat derived classes:
- `Persegi` yang override hitungLuas()
- `Lingkaran` yang override hitungLuas()
- `Segitiga` yang override hitungLuas()

---

### Soal 31: Calling Base Class Method
Dalam derived class, panggil method dari base class menggunakan scope resolution operator (::). Contoh: `BaseClass::methodName()`

---

### Soal 32: Multiple Level Inheritance
Buatlah hierarki 3 level:
```
Makhluk Hidup
    |
Hewan
    |
Mamalia
```

Setiap level menambahkan atribut spesifik. Demonstrasikan object dari class paling bawah.

---

### Soal 33: Protected Constructor
Buatlah base class dengan protected constructor untuk mencegah instantiation langsung. Hanya derived class yang bisa membuat object.

---

### Soal 34: Inheritance dengan Composition
Buatlah class `Alamat` dan class `Person` yang memiliki atribut Alamat (composition). Lalu buat class `Mahasiswa` yang inherit dari Person.

---

### Soal 35: Access Specifier dalam Inheritance
Demonstrasikan perbedaan public, protected, dan private inheritance. Jelaskan bagaimana masing-masing mempengaruhi akses ke base class members.

---

### Soal 36: Hierarchical Inheritance
Buatlah satu base class `Karyawan` dan beberapa derived classes:
- `KaryawanTetap`
- `KaryawanKontrak`
- `KaryawanMagang`

Setiap derived class memiliki method `hitungGaji()` yang berbeda.

---

### Soal 37: Multilevel Inheritance
Buatlah hierarki:
```
BangunRuang
    |
Kubus (turunan dari BangunRuang)
    |
KubusKhusus (turunan dari Kubus)
```

---

### Soal 38: Virtual Base Class (Opsional Advanced)
Jelaskan diamond problem dalam multiple inheritance dan bagaimana virtual base class mengatasinya. (Catatan: Multiple inheritance tidak dibahas detail di pertemuan ini, ini hanya untuk pengetahuan)

---

### Soal 39: Is-A Relationship
Untuk setiap pair berikut, tentukan apakah inheritance cocok (is-a relationship):
- Mobil - Kendaraan
- Mahasiswa - Person
- Persegi - Lingkaran
- Buku - Perpustakaan

Jelaskan reasoning Anda.

---

### Soal 40: Refactoring ke Inheritance
Diberikan dua class terpisah `Dosen` dan `Mahasiswa` yang memiliki banyak atribut sama. Refactor dengan membuat base class `Civitas` yang berisi atribut umum.

---

## Bagian 4: Polymorphism (10 soal)

### Soal 41: Function Overriding
Buatlah base class `Hewan` dengan method `bersuara()`. Buat derived classes `Kucing`, `Anjing`, `Burung` yang masing-masing override method `bersuara()` dengan implementasi berbeda.

---

### Soal 42: Virtual Functions
Tambahkan keyword `virtual` pada base class di soal 41. Buat array of pointers ke base class, isi dengan berbagai derived class objects, dan panggil `bersuara()`. Apa perbedaannya dengan tanpa virtual?

---

### Soal 43: Pure Virtual Function (Opsional)
Buatlah abstract base class `BangunDatar` dengan pure virtual function `hitungLuas()`. Buat derived classes yang mengimplementasikan method tersebut. Coba buat object dari base class - apa yang terjadi?

---

### Soal 44: Virtual Destructor
Buatlah hierarki class dengan base class yang memiliki virtual destructor. Demonstrasikan bahwa derived class destructor dipanggil dengan benar saat delete pointer to base class.

---

### Soal 45: Runtime Polymorphism
Buatlah sistem untuk menghitung gaji berbagai tipe karyawan:
```cpp
class Karyawan {
public:
    virtual double hitungGaji() = 0;
};

class KaryawanTetap : public Karyawan {
    // Gaji pokok + tunjangan
};

class KaryawanKontrak : public Karyawan {
    // Upah per hari × jumlah hari kerja
};
```

Buat array of pointers dan hitung total gaji semua karyawan.

---

### Soal 46: Keyword override
Demonstrasikan penggunaan keyword `override` (C++11). Coba buat typo dalam signature method - bagaimana compiler memberi warning?

---

### Soal 47: Virtual Function dengan Default Implementation
Buatlah base class dengan virtual function yang memiliki implementasi default. Beberapa derived class override, beberapa menggunakan default implementation.

---

### Soal 48: Type Casting dalam Polymorphism
Demonstrasikan dynamic_cast untuk safely cast base class pointer ke derived class pointer. Tangani kasus ketika cast gagal.

---

### Soal 49: Polymorphic Container
Buatlah vector<ItemPerpustakaan*> yang bisa menampung pointer ke Buku, Majalah, DVD, dll. Iterasi dan panggil method virtual untuk setiap item.

---

### Soal 50: Design dengan Polymorphism
Rancanglah sistem pembayaran yang mendukung berbagai metode:
- Transfer Bank
- Kartu Kredit
- E-Wallet
- Cash

Gunakan polymorphism untuk method `prosesPembayaran()`.

---

## Bagian 5: Aplikasi Terintegrasi (5 soal)

### Soal 51: Sistem Akademik
Buatlah aplikasi sistem akademik sederhana dengan class-class:
- `Person` (base)
- `Mahasiswa` (derived)
- `Dosen` (derived)
- `MataKuliah`
- `Nilai`

Fitur: input mahasiswa, input nilai, hitung IPK, tampilkan transkrip.

---

### Soal 52: Sistem Toko Online
Buatlah aplikasi toko online dengan:
- `Produk` (base class)
- `Elektronik`, `Pakaian`, `Makanan` (derived classes)
- `Keranjang`
- `Transaksi`

Fitur: tambah produk ke keranjang, hitung total, proses checkout.

---

### Soal 53: Sistem Perpustakaan
Buatlah sistem perpustakaan lengkap dengan:
- `ItemPerpustakaan` (base)
- `Buku`, `Majalah`, `DVD` (derived)
- `Anggota`
- `Peminjaman`

Fitur: pinjam, kembalikan, cari, denda keterlambatan.

---

### Soal 54: Sistem Parkir
Buatlah sistem parkir dengan:
- `Kendaraan` (base)
- `Mobil`, `Motor`, `Truk` (derived, tarif berbeda)
- `TempatParkir`
- `Tiket`

Fitur: masuk parkir, keluar parkir, hitung biaya berdasarkan durasi dan jenis kendaraan.

---

### Soal 55: Sistem Rumah Sakit (Final Project)
Buatlah sistem rumah sakit dengan class-class:
- `Person` (base)
- `Pasien`, `Dokter`, `Perawat` (derived)
- `RuangRawat`
- `Obat`
- `RekamMedis`
- `Transaksi`

Fitur lengkap:
- Registrasi pasien
- Assign dokter
- Input diagnosa dan obat
- Hitung biaya perawatan
- Laporan harian

---

## Kunci Jawaban Singkat

Kunci jawaban lengkap tidak disediakan agar Anda belajar mandiri. Beberapa tips:

- **Soal 1-15**: Fokus pada definisi class yang benar dan enkapsulasi
- **Soal 16-25**: Perhatikan urutan eksekusi constructor/destructor
- **Soal 26-40**: Pahami hubungan is-a dan code reuse
- **Soal 41-50**: Virtual functions adalah kunci polymorphism
- **Soal 51-55**: Integrasikan semua konsep OOP

## Tips Mengerjakan

1. **Mulai dari yang mudah** - Jangan skip soal dasar
2. **Compile dan test** - Jangan hanya menulis, test setiap code
3. **Buat dokumentasi** - Comment code Anda
4. **Refactor** - Perbaiki code setelah works
5. **Diskusi** - Diskusikan dengan teman jika stuck

## Kriteria Penilaian (Jika Dikumpulkan)

- **Correctness (40%)**: Program berjalan tanpa error
- **Code Quality (30%)**: Clean code, proper naming, good structure
- **OOP Principles (20%)**: Proper encapsulation, inheritance, polymorphism
- **Documentation (10%)**: Comments dan penjelasan

---

**Selamat Berlatih! 💪**

Pemrograman OOP memerlukan latihan konsisten. Semakin banyak Anda praktik, semakin alami paradigma OOP akan terasa.
