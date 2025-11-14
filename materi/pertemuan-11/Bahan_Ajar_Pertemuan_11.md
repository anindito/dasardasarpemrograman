# BAB 11: POINTER DAN MEMORI DINAMIS

## 11.1 Pendahuluan

Selamat datang di pertemuan kesebelas mata kuliah Dasar-Dasar Pemrograman. Setelah mempelajari array sebagai struktur data fundamental, kita akan memasuki topik yang sangat penting namun sering dianggap menantang oleh banyak programmer pemula: pointer dan manajemen memori dinamis. Pointer adalah salah satu fitur paling powerful dalam C++ yang membedakannya dari banyak bahasa pemrograman modern lainnya.

Bayangkan Anda berada di perpustakaan besar yang memiliki jutaan buku. Alih-alih membawa buku fisik yang berat ke mana-mana, Anda cukup membawa kartu katalog kecil yang berisi informasi lokasi buku tersebut. Ketika Anda membutuhkan buku itu, Anda tinggal pergi ke lokasi yang tertera di kartu. Inilah analogi sederhana tentang pointer: alih-alih menyalin data yang besar, kita cukup menyimpan "alamat" dimana data tersebut berada di memori komputer.

Pemahaman mendalam tentang pointer akan membuka pintu ke berbagai konsep pemrograman lanjutan seperti linked list, tree, graph, dan struktur data dinamis lainnya. Pada bab ini, kita akan mempelajari konsep pointer dari dasar, bagaimana mendeklarasikan dan menggunakannya, hubungan pointer dengan array, serta cara melakukan alokasi memori dinamis yang efisien. Kita juga akan membahas bahaya potensial dari penggunaan pointer yang salah dan bagaimana menghindari memory leak.

## 11.2 Konsep Dasar Pointer

### 11.2.1 Memahami Memori Komputer

Sebelum memahami pointer, kita perlu memahami bagaimana data disimpan di memori komputer. Memori komputer dapat dibayangkan sebagai deretan kotak penyimpanan yang sangat banyak, dimana setiap kotak memiliki alamat unik. Ketika kita mendeklarasikan variabel, komputer akan mengalokasikan satu atau beberapa kotak memori untuk menyimpan nilai variabel tersebut.

Setiap lokasi di memori memiliki alamat yang unik, biasanya dinyatakan dalam sistem heksadesimal seperti `0x7ffd5ba4e8bc`. Alamat ini mirip seperti alamat rumah: ia menunjukkan lokasi spesifik dimana data disimpan. Dalam pemrograman normal, kita tidak perlu tahu alamat spesifik ini karena kita cukup menggunakan nama variabel. Namun dengan pointer, kita dapat secara eksplisit bekerja dengan alamat memori ini.

### 11.2.2 Apa Itu Pointer?

Pointer adalah variabel khusus yang menyimpan alamat memori dari variabel lain. Berbeda dengan variabel biasa yang menyimpan nilai data (seperti angka 42 atau karakter 'A'), pointer menyimpan lokasi dimana data tersebut berada. Dengan kata lain, pointer "menunjuk" ke lokasi memori tertentu.

Mengapa pointer penting? Pertama, pointer memungkinkan kita untuk memanipulasi data secara efisien tanpa harus menyalin data tersebut. Kedua, pointer memungkinkan kita untuk mengalokasikan memori secara dinamis saat program berjalan. Ketiga, pointer adalah fondasi untuk struktur data lanjutan seperti linked list dan tree. Keempat, pointer memungkinkan kita untuk membuat fungsi yang dapat memodifikasi variabel di luar scope-nya.

### 11.2.3 Deklarasi Pointer

Dalam C++, pointer dideklarasikan dengan menambahkan tanda asterisk (*) setelah tipe data. Sintaks umumnya adalah:

```cpp
tipe_data* nama_pointer;
```

Tanda asterisk dapat ditempatkan dekat dengan tipe data, dekat dengan nama variabel, atau di tengah-tengah, namun konvensi yang paling umum adalah menempatkannya dekat dengan tipe data. Berikut adalah beberapa contoh deklarasi pointer:

```cpp
#include <iostream>
using namespace std;

int main() {
    int* ptr1;        // Pointer ke integer
    double* ptr2;     // Pointer ke double
    char* ptr3;       // Pointer ke character
    float* ptr4;      // Pointer ke float
    
    // Deklarasi multiple pointer
    int *p1, *p2, *p3;  // Tiga pointer ke integer
    
    // Pointer yang belum diinisialisasi mengandung nilai random
    // Sebaiknya selalu inisialisasi pointer
    int* ptr_null = nullptr;  // C++11: pointer yang tidak menunjuk ke mana-mana
    int* ptr_zero = 0;        // Cara lama: pointer null
    
    cout << "Pointer dideklarasikan dengan aman!" << endl;
    
    return 0;
}
```

Perhatikan bahwa pointer yang baru dideklarasikan tanpa inisialisasi berisi nilai acak yang berbahaya. Menggunakan pointer yang tidak diinisialisasi dapat menyebabkan program crash. Oleh karena itu, praktik terbaik adalah selalu menginisialisasi pointer, minimal dengan `nullptr` jika belum siap untuk menunjuk ke variabel tertentu.

### 11.2.4 Visualisasi Pointer dan Alamat Memori

Untuk memudahkan pemahaman tentang konsep pointer, perhatikan diagram berikut yang menunjukkan hubungan antara variabel, pointer, dan alamat memori:

![Visualisasi Pointer dan Alamat Memori](images/pointer_visualization.svg)

*Gambar 11.1: Visualisasi Pointer dan Alamat Memori*

Diagram di atas menunjukkan:
- Variabel `x` dengan nilai 42 disimpan di alamat memori 0x1000
- Pointer `ptr` menyimpan alamat 0x1000 (alamat dari variabel `x`)
- Pointer `ptr` sendiri juga memiliki alamat memori yaitu 0x2000
- Operator `&x` menghasilkan alamat memori dari `x`
- Operator `*ptr` mengakses nilai yang ada di alamat yang ditunjuk oleh `ptr`

Dengan visualisasi ini, kita dapat melihat bahwa pointer sebenarnya adalah variabel yang "menunjuk" ke lokasi memori lain. Panah dalam diagram merepresentasikan hubungan "menunjuk ke" antara pointer dan variabel yang ditunjuknya.

## 11.3 Operator Pointer

### 11.3.1 Operator Address-of (&)

Operator ampersand (&) digunakan untuk mendapatkan alamat memori dari sebuah variabel. Ketika kita menuliskan `&variabel`, kita mendapatkan alamat dimana variabel tersebut disimpan di memori. Ini adalah cara utama untuk membuat pointer menunjuk ke variabel yang sudah ada.

```cpp
#include <iostream>
using namespace std;

int main() {
    int angka = 42;
    int* ptr;
    
    // Menggunakan operator & untuk mendapatkan alamat
    ptr = &angka;
    
    cout << "Nilai angka: " << angka << endl;
    cout << "Alamat angka: " << &angka << endl;
    cout << "Nilai ptr (alamat yang disimpan): " << ptr << endl;
    cout << "Alamat ptr sendiri: " << &ptr << endl;
    
    // Output contoh:
    // Nilai angka: 42
    // Alamat angka: 0x7ffd5ba4e8bc
    // Nilai ptr (alamat yang disimpan): 0x7ffd5ba4e8bc
    // Alamat ptr sendiri: 0x7ffd5ba4e8c0
    
    return 0;
}
```

Dalam contoh di atas, `&angka` memberikan alamat memori dimana variabel `angka` disimpan. Alamat ini kemudian disimpan dalam pointer `ptr`. Perhatikan bahwa `ptr` sendiri juga memiliki alamat memori karena pointer juga adalah variabel.

### 11.3.2 Operator Dereference (*)

Operator asterisk (*) ketika digunakan pada pointer yang sudah ada disebut operator dereference atau indirection. Operator ini digunakan untuk mengakses nilai yang disimpan di alamat memori yang ditunjuk oleh pointer. Dengan kata lain, dereference "mengikuti" pointer ke lokasi yang ditunjuk dan memberikan akses ke nilai di sana.

```cpp
#include <iostream>
using namespace std;

int main() {
    int nilai = 100;
    int* ptr = &nilai;
    
    cout << "=== Sebelum Modifikasi ===" << endl;
    cout << "Nilai variabel: " << nilai << endl;
    cout << "Alamat variabel: " << &nilai << endl;
    cout << "Nilai pointer (alamat): " << ptr << endl;
    cout << "Nilai yang ditunjuk (*ptr): " << *ptr << endl;
    
    // Mengubah nilai melalui pointer
    *ptr = 200;
    
    cout << "\n=== Setelah Modifikasi ===" << endl;
    cout << "Nilai variabel: " << nilai << endl;
    cout << "Nilai yang ditunjuk (*ptr): " << *ptr << endl;
    
    // Output:
    // === Sebelum Modifikasi ===
    // Nilai variabel: 100
    // Alamat variabel: 0x7ffd5ba4e8bc
    // Nilai pointer (alamat): 0x7ffd5ba4e8bc
    // Nilai yang ditunjuk (*ptr): 100
    //
    // === Setelah Modifikasi ===
    // Nilai variabel: 200
    // Nilai yang ditunjuk (*ptr): 200
    
    return 0;
}
```

Contoh di atas menunjukkan kekuatan pointer: dengan mengubah `*ptr`, kita sebenarnya mengubah nilai variabel `nilai`. Ini karena `ptr` menunjuk ke lokasi memori yang sama dengan `nilai`.

### 11.3.3 Ringkasan Notasi Pointer

```cpp
#include <iostream>
using namespace std;

int main() {
    int x = 10;
    int* ptr = &x;
    
    cout << "Notasi dan Maknanya:" << endl;
    cout << "x       = " << x << " (nilai variabel x)" << endl;
    cout << "&x      = " << &x << " (alamat variabel x)" << endl;
    cout << "ptr     = " << ptr << " (alamat yang disimpan di ptr)" << endl;
    cout << "*ptr    = " << *ptr << " (nilai di alamat yang ditunjuk ptr)" << endl;
    cout << "&ptr    = " & << &ptr << " (alamat pointer ptr sendiri)" << endl;
    
    // Verifikasi bahwa ptr dan &x sama
    if (ptr == &x) {
        cout << "\nptr dan &x menunjuk ke lokasi yang sama!" << endl;
    }
    
    // Verifikasi bahwa *ptr dan x sama
    if (*ptr == x) {
        cout << "*ptr dan x memiliki nilai yang sama!" << endl;
    }
    
    return 0;
}
```

## 11.4 Pointer dan Array

### 11.4.1 Hubungan Pointer dengan Array

Dalam C++, nama array sebenarnya adalah pointer konstan yang menunjuk ke elemen pertama array. Ini adalah salah satu konsep paling penting dalam memahami pointer: array dan pointer sangat erat kaitannya. Ketika kita mendeklarasikan array `int arr[5]`, nama `arr` sebenarnya berperilaku seperti pointer yang menunjuk ke `arr[0]`.

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[5] = {10, 20, 30, 40, 50};
    int* ptr = arr;  // arr otomatis menjadi alamat arr[0]
    
    cout << "=== Alamat Elemen Array ===" << endl;
    cout << "Alamat arr[0]: " << &arr[0] << endl;
    cout << "Nilai arr: " << arr << endl;
    cout << "Nilai ptr: " << ptr << endl;
    cout << "Semua alamat di atas sama!" << endl;
    
    cout << "\n=== Akses Menggunakan Pointer ===" << endl;
    cout << "*ptr = " << *ptr << " (sama dengan arr[0])" << endl;
    cout << "*(ptr+1) = " << *(ptr+1) << " (sama dengan arr[1])" << endl;
    cout << "*(ptr+2) = " << *(ptr+2) << " (sama dengan arr[2])" << endl;
    
    cout << "\n=== Akses Menggunakan Array Notation ===" << endl;
    cout << "ptr[0] = " << ptr[0] << " (sama dengan arr[0])" << endl;
    cout << "ptr[1] = " << ptr[1] << " (sama dengan arr[1])" << endl;
    cout << "ptr[2] = " << ptr[2] << " (sama dengan arr[2])" << endl;
    
    return 0;
}
```

Contoh di atas menunjukkan bahwa `arr` dan `&arr[0]` adalah sama. Lebih jauh lagi, kita dapat mengakses elemen array menggunakan notasi pointer atau notasi array, dan keduanya ekuivalen.

### 11.4.2 Pointer Arithmetic

Pointer arithmetic adalah kemampuan untuk melakukan operasi aritmatika pada pointer. Ketika kita menambahkan angka ke pointer, pointer akan bergerak sebanyak n kali ukuran tipe data yang ditunjuk. Misalnya, jika `ptr` adalah pointer ke integer (4 bytes), maka `ptr + 1` akan menunjuk ke alamat yang 4 bytes lebih tinggi.

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[5] = {100, 200, 300, 400, 500};
    int* ptr = arr;
    
    cout << "=== Pointer Arithmetic ===" << endl;
    cout << "Alamat ptr: " << ptr << endl;
    cout << "Alamat ptr+1: " << (ptr+1) << endl;
    cout << "Alamat ptr+2: " << (ptr+2) << endl;
    cout << "Perbedaan: " << (long long)(ptr+1) - (long long)ptr << " bytes" << endl;
    
    cout << "\n=== Traversal Array dengan Pointer ===" << endl;
    for (int i = 0; i < 5; i++) {
        cout << "Alamat: " << (ptr+i) << " | Nilai: " << *(ptr+i) << endl;
    }
    
    cout << "\n=== Increment Pointer ===" << endl;
    int* temp = arr;
    for (int i = 0; i < 5; i++) {
        cout << "Elemen ke-" << i << ": " << *temp << endl;
        temp++;  // Pindah ke elemen berikutnya
    }
    
    return 0;
}
```

Pointer arithmetic sangat berguna untuk iterasi melalui array tanpa menggunakan indeks. Operasi yang diperbolehkan pada pointer meliputi: penambahan konstanta (`ptr + n`), pengurangan konstanta (`ptr - n`), increment (`ptr++`), decrement (`ptr--`), dan pengurangan dua pointer (`ptr1 - ptr2`).

### 11.4.3 Passing Array ke Fungsi dengan Pointer

Ketika kita passing array ke fungsi, sebenarnya yang di-pass adalah pointer ke elemen pertama array. Ini membuat passing array sangat efisien karena tidak ada copying data yang terjadi. Namun ini juga berarti fungsi dapat memodifikasi array asli.

```cpp
#include <iostream>
using namespace std;

// Fungsi dengan parameter array (sebenarnya pointer)
void tampilkanArray(int* arr, int ukuran) {
    cout << "Isi array: ";
    for (int i = 0; i < ukuran; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

// Fungsi untuk mengalikan semua elemen dengan 2
void kalikanDua(int* arr, int ukuran) {
    for (int i = 0; i < ukuran; i++) {
        arr[i] *= 2;  // Memodifikasi array asli
    }
}

// Fungsi untuk mencari nilai maksimum
int cariMaks(int* arr, int ukuran) {
    int maks = arr[0];
    for (int i = 1; i < ukuran; i++) {
        if (arr[i] > maks) {
            maks = arr[i];
        }
    }
    return maks;
}

int main() {
    int data[5] = {3, 7, 2, 9, 4};
    
    cout << "Array awal:" << endl;
    tampilkanArray(data, 5);
    
    cout << "\nSetelah kalikan 2:" << endl;
    kalikanDua(data, 5);
    tampilkanArray(data, 5);
    
    cout << "\nNilai maksimum: " << cariMaks(data, 5) << endl;
    
    return 0;
}
```

## 11.5 Memori Dinamis

### 11.5.1 Konsep Alokasi Memori

Dalam pemrograman, ada dua jenis alokasi memori: statik dan dinamis. Alokasi memori statik terjadi pada compile time dimana ukuran dan lifetime variabel sudah ditentukan. Contohnya adalah variabel lokal dan array dengan ukuran tetap. Sebaliknya, alokasi memori dinamis terjadi pada runtime dimana kita dapat mengalokasikan dan membebaskan memori sesuai kebutuhan program.

Memori komputer dibagi menjadi beberapa segmen: stack dan heap. Stack digunakan untuk variabel lokal dan memiliki ukuran terbatas serta otomatis dibersihkan ketika fungsi selesai. Heap adalah area memori yang lebih besar dan digunakan untuk alokasi dinamis. Memori di heap harus di-manage secara manual oleh programmer: dialokasikan dengan `new` dan dibebaskan dengan `delete`.

![Memory Layout: Stack vs Heap](images/memory_layout.svg)

*Gambar 11.2: Memory Layout - Stack vs Heap*

Diagram di atas menunjukkan perbedaan mendasar antara stack dan heap memory:

**Stack Memory:**
- Ukuran terbatas (biasanya 1-8 MB)
- Akses sangat cepat
- Manajemen otomatis (automatic cleanup)
- Menggunakan struktur LIFO (Last In First Out)
- Digunakan untuk variabel lokal dan parameter fungsi
- Contoh: `int x = 10;`, `int arr[100];`

**Heap Memory:**
- Ukuran jauh lebih besar (hingga GB)
- Akses lebih lambat dibanding stack
- Manajemen manual (programmer bertanggung jawab)
- Tidak ada urutan khusus (fragmentasi mungkin terjadi)
- Digunakan untuk alokasi dinamis
- Contoh: `int* ptr = new int(42);`, `int* arr = new int[n];`

Pointer yang dideklarasikan di stack dapat menunjuk ke memori yang dialokasikan di heap. Ini memungkinkan fleksibilitas dalam pengelolaan memori sambil tetap mempertahankan referensi yang mudah diakses di stack.

### 11.5.2 Operator new dan delete

Operator `new` digunakan untuk mengalokasikan memori di heap dan mengembalikan pointer ke memori tersebut. Operator `delete` digunakan untuk membebaskan memori yang telah dialokasikan. Ini adalah pasangan yang harus selalu digunakan bersama: setiap `new` harus memiliki `delete` yang berkorespondensi untuk menghindari memory leak.

```cpp
#include <iostream>
using namespace std;

int main() {
    // Alokasi single variable
    int* ptr1 = new int;          // Alokasi integer
    *ptr1 = 42;
    cout << "Nilai: " << *ptr1 << endl;
    delete ptr1;                  // Jangan lupa dealokasi!
    ptr1 = nullptr;               // Good practice: set ke nullptr
    
    // Alokasi dengan inisialisasi
    double* ptr2 = new double(3.14159);
    cout << "Nilai PI: " << *ptr2 << endl;
    delete ptr2;
    ptr2 = nullptr;
    
    // Alokasi array dinamis
    int ukuran;
    cout << "\nMasukkan ukuran array: ";
    cin >> ukuran;
    
    int* arr = new int[ukuran];   // Alokasi array dinamis
    
    // Isi array
    for (int i = 0; i < ukuran; i++) {
        arr[i] = (i + 1) * 10;
    }
    
    // Tampilkan array
    cout << "Isi array: ";
    for (int i = 0; i < ukuran; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
    
    delete[] arr;                 // Untuk array, gunakan delete[]
    arr = nullptr;
    
    return 0;
}
```

Perbedaan penting: untuk single variable gunakan `delete ptr`, tapi untuk array gunakan `delete[] arr`. Menggunakan `delete` biasa untuk array atau `delete[]` untuk single variable dapat menyebabkan undefined behavior dan memory corruption.

### 11.5.3 Memory Leak dan Bahayanya

Memory leak terjadi ketika memori yang dialokasikan dengan `new` tidak pernah di-dealokasikan dengan `delete`. Seiring waktu, program akan menghabiskan semua memori yang tersedia dan bisa menyebabkan sistem crash. Memory leak adalah salah satu bug paling berbahaya karena efeknya mungkin tidak langsung terlihat.

```cpp
#include <iostream>
using namespace std;

// CONTOH BURUK: Memory leak
void contohMemoryLeak() {
    int* ptr = new int[1000];
    // Menggunakan array...
    // LUPA delete[] ptr;  ← MEMORY LEAK!
}

// CONTOH BAIK: Proper memory management
void contohMemoryManagementBaik() {
    int* ptr = new int[1000];
    // Menggunakan array...
    delete[] ptr;
    ptr = nullptr;
}

// CONTOH: Tracking memory leak
void demonstrasiMemoryLeak() {
    cout << "Melakukan alokasi berulang tanpa dealokasi..." << endl;
    for (int i = 0; i < 1000; i++) {
        int* leak = new int[10000];  // Alokasi 40KB per iterasi
        // Tidak ada delete[] ← Memory leak 40MB total!
    }
    cout << "Selesai. Memory leak terjadi!" << endl;
}

int main() {
    cout << "=== Demonstrasi Memory Management ===" << endl;
    
    // Good practice
    contohMemoryManagementBaik();
    cout << "Memory management baik: OK" << endl;
    
    // Uncomment untuk lihat memory leak (hati-hati!)
    // demonstrasiMemoryLeak();
    
    return 0;
}
```

### 11.5.4 Dangling Pointer

Dangling pointer adalah pointer yang menunjuk ke memori yang sudah di-dealokasikan atau tidak valid. Mengakses dangling pointer menyebabkan undefined behavior yang dapat berupa: program crash, data corruption, atau bahkan "terlihat bekerja" padahal sebenarnya error.

```cpp
#include <iostream>
using namespace std;

int main() {
    int* ptr1 = new int(100);
    cout << "Nilai awal: " << *ptr1 << endl;
    
    delete ptr1;
    // ptr1 sekarang adalah dangling pointer!
    
    // BAHAYA: Mengakses dangling pointer
    // cout << *ptr1 << endl;  ← Undefined behavior!
    
    // SOLUSI: Set ke nullptr setelah delete
    ptr1 = nullptr;
    
    // Sekarang aman untuk cek
    if (ptr1 != nullptr) {
        cout << *ptr1 << endl;
    } else {
        cout << "Pointer adalah null, aman!" << endl;
    }
    
    // Contoh lain: double delete
    int* ptr2 = new int(200);
    delete ptr2;
    // delete ptr2;  ← BAHAYA: Double delete!
    ptr2 = nullptr;
    delete ptr2;     // Aman: delete nullptr tidak bermasalah
    
    return 0;
}
```

Praktik terbaik untuk menghindari dangling pointer: selalu set pointer ke `nullptr` setelah `delete`, dan selalu cek apakah pointer bukan `nullptr` sebelum dereference.

## 11.6 Pointer ke Pointer

### 11.6.1 Multi-level Pointer

Pointer ke pointer adalah pointer yang menyimpan alamat pointer lain. Konsep ini mungkin terdengar rumit, namun sangat berguna untuk struktur data seperti matrix dinamis atau linked list dengan multiple levels.

```cpp
#include <iostream>
using namespace std;

int main() {
    int nilai = 42;
    int* ptr1 = &nilai;           // Pointer ke integer
    int** ptr2 = &ptr1;           // Pointer ke pointer
    int*** ptr3 = &ptr2;          // Pointer ke pointer ke pointer
    
    cout << "=== Multi-level Pointer ===" << endl;
    cout << "Nilai langsung: " << nilai << endl;
    cout << "Via ptr1: " << *ptr1 << endl;
    cout << "Via ptr2: " << **ptr2 << endl;
    cout << "Via ptr3: " << ***ptr3 << endl;
    
    cout << "\n=== Alamat dan Nilai ===" << endl;
    cout << "Alamat nilai: " << &nilai << endl;
    cout << "Nilai ptr1: " << ptr1 << endl;
    cout << "Alamat ptr1: " << &ptr1 << endl;
    cout << "Nilai ptr2: " << ptr2 << endl;
    
    // Modifikasi melalui double pointer
    **ptr2 = 100;
    cout << "\nSetelah **ptr2 = 100:" << endl;
    cout << "Nilai: " << nilai << endl;
    
    return 0;
}
```

### 11.6.2 Matrix Dinamis dengan Double Pointer

Salah satu aplikasi praktis dari pointer ke pointer adalah membuat matrix (array 2D) dinamis dimana ukurannya ditentukan saat runtime.

```cpp
#include <iostream>
using namespace std;

int main() {
    int baris, kolom;
    cout << "Masukkan jumlah baris: ";
    cin >> baris;
    cout << "Masukkan jumlah kolom: ";
    cin >> kolom;
    
    // Alokasi matrix dinamis
    int** matrix = new int*[baris];  // Array of pointers
    for (int i = 0; i < baris; i++) {
        matrix[i] = new int[kolom];   // Setiap baris adalah array
    }
    
    // Isi matrix
    cout << "\nMengisi matrix..." << endl;
    for (int i = 0; i < baris; i++) {
        for (int j = 0; j < kolom; j++) {
            matrix[i][j] = i * kolom + j + 1;
        }
    }
    
    // Tampilkan matrix
    cout << "\nIsi matrix:" << endl;
    for (int i = 0; i < baris; i++) {
        for (int j = 0; j < kolom; j++) {
            cout << matrix[i][j] << "\t";
        }
        cout << endl;
    }
    
    // Dealokasi matrix (penting!)
    for (int i = 0; i < baris; i++) {
        delete[] matrix[i];  // Hapus setiap baris
    }
    delete[] matrix;         // Hapus array of pointers
    matrix = nullptr;
    
    cout << "\nMatrix berhasil di-dealokasikan!" << endl;
    
    return 0;
}
```

Perhatikan urutan dealokasi: kita harus menghapus array-array internal terlebih dahulu, baru kemudian menghapus array of pointers. Urutan yang terbalik akan menyebabkan memory leak.

## 11.7 Const Pointer dan Pointer to Const

### 11.7.1 Pointer to Const

Pointer to const adalah pointer yang menunjuk ke nilai konstan. Kita tidak dapat mengubah nilai yang ditunjuk melalui pointer ini, tapi kita dapat mengubah kemana pointer menunjuk.

```cpp
#include <iostream>
using namespace std;

int main() {
    int nilai1 = 10;
    int nilai2 = 20;
    
    // Pointer to const int
    const int* ptr = &nilai1;
    
    cout << "Nilai awal: " << *ptr << endl;
    
    // ptr = &nilai2;  // OK: Bisa ubah kemana pointer menunjuk
    // *ptr = 30;      // ERROR: Tidak bisa ubah nilai melalui pointer
    
    // Tapi kita bisa ubah nilai langsung
    nilai1 = 15;
    cout << "Nilai setelah diubah langsung: " << *ptr << endl;
    
    // Ubah pointer ke nilai2
    ptr = &nilai2;
    cout << "Sekarang menunjuk ke nilai2: " << *ptr << endl;
    
    return 0;
}
```

### 11.7.2 Const Pointer

Const pointer adalah pointer yang alamatnya tidak dapat diubah setelah inisialisasi, tapi nilai yang ditunjuk dapat diubah melalui pointer.

```cpp
#include <iostream>
using namespace std;

int main() {
    int nilai1 = 10;
    int nilai2 = 20;
    
    // Const pointer to int
    int* const ptr = &nilai1;
    
    cout << "Nilai awal: " << *ptr << endl;
    
    *ptr = 30;      // OK: Bisa ubah nilai yang ditunjuk
    cout << "Nilai setelah diubah: " << *ptr << endl;
    
    // ptr = &nilai2;  // ERROR: Tidak bisa ubah kemana pointer menunjuk
    
    return 0;
}
```

### 11.7.3 Const Pointer to Const

Ini adalah kombinasi keduanya: pointer yang tidak dapat diubah dan nilai yang ditunjuk juga tidak dapat diubah melalui pointer tersebut.

```cpp
#include <iostream>
using namespace std;

int main() {
    int nilai1 = 10;
    int nilai2 = 20;
    
    // Const pointer to const int
    const int* const ptr = &nilai1;
    
    cout << "Nilai: " << *ptr << endl;
    
    // *ptr = 30;      // ERROR: Tidak bisa ubah nilai
    // ptr = &nilai2;  // ERROR: Tidak bisa ubah pointer
    
    // Hanya bisa baca
    cout << "Nilai tetap: " << *ptr << endl;
    
    return 0;
}
```

Ringkasan:
- `const int* ptr`: Pointer to const (nilai tidak bisa diubah via pointer)
- `int* const ptr`: Const pointer (pointer tidak bisa diubah)
- `const int* const ptr`: Const pointer to const (keduanya tidak bisa diubah)

## 11.8 Pointer dan Fungsi

### 11.8.1 Pointer sebagai Parameter Fungsi

Menggunakan pointer sebagai parameter fungsi memungkinkan fungsi untuk memodifikasi variabel di luar scope-nya. Ini adalah alternatif dari pass by reference.

```cpp
#include <iostream>
using namespace std;

// Fungsi swap menggunakan pointer
void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Fungsi untuk menambah nilai
void tambahNilai(int* ptr, int penambah) {
    *ptr += penambah;
}

// Fungsi untuk reset array
void resetArray(int* arr, int ukuran) {
    for (int i = 0; i < ukuran; i++) {
        arr[i] = 0;
    }
}

int main() {
    int x = 5, y = 10;
    cout << "Sebelum swap: x = " << x << ", y = " << y << endl;
    swap(&x, &y);
    cout << "Setelah swap: x = " << x << ", y = " << y << endl;
    
    int nilai = 100;
    cout << "\nNilai awal: " << nilai << endl;
    tambahNilai(&nilai, 50);
    cout << "Setelah tambah 50: " << nilai << endl;
    
    int data[5] = {1, 2, 3, 4, 5};
    cout << "\nArray sebelum reset: ";
    for (int i = 0; i < 5; i++) cout << data[i] << " ";
    cout << endl;
    
    resetArray(data, 5);
    cout << "Array setelah reset: ";
    for (int i = 0; i < 5; i++) cout << data[i] << " ";
    cout << endl;
    
    return 0;
}
```

### 11.8.2 Fungsi yang Mengembalikan Pointer

Fungsi dapat mengembalikan pointer, namun harus sangat hati-hati. Jangan pernah mengembalikan pointer ke variabel lokal karena variabel lokal akan dihapus setelah fungsi selesai.

```cpp
#include <iostream>
using namespace std;

// BAHAYA: Mengembalikan pointer ke variabel lokal
int* fungsiYangBerbahaya() {
    int x = 10;
    return &x;  // JANGAN LAKUKAN INI!
    // x akan dihapus setelah fungsi selesai
}

// AMAN: Mengembalikan pointer ke memori dinamis
int* buatArray(int ukuran) {
    int* arr = new int[ukuran];
    for (int i = 0; i < ukuran; i++) {
        arr[i] = i * 10;
    }
    return arr;  // Caller bertanggung jawab untuk delete
}

// AMAN: Mengembalikan pointer yang di-pass ke fungsi
int* cariMaks(int* arr, int ukuran) {
    if (ukuran == 0) return nullptr;
    
    int* maks = &arr[0];
    for (int i = 1; i < ukuran; i++) {
        if (arr[i] > *maks) {
            maks = &arr[i];
        }
    }
    return maks;
}

int main() {
    // Contoh aman: array dinamis
    int* dynamicArr = buatArray(5);
    cout << "Array dinamis: ";
    for (int i = 0; i < 5; i++) {
        cout << dynamicArr[i] << " ";
    }
    cout << endl;
    delete[] dynamicArr;
    
    // Contoh aman: pointer ke elemen array
    int data[5] = {3, 7, 2, 9, 4};
    int* ptrMaks = cariMaks(data, 5);
    if (ptrMaks != nullptr) {
        cout << "Nilai maksimum: " << *ptrMaks << endl;
        cout << "Alamat maksimum: " << ptrMaks << endl;
    }
    
    return 0;
}
```

## 11.9 Aplikasi Praktis Pointer

### 11.9.1 Dynamic Array Resizing

Salah satu kegunaan penting memori dinamis adalah kemampuan untuk membuat array yang ukurannya dapat berubah saat runtime.

```cpp
#include <iostream>
using namespace std;

// Fungsi untuk resize array
int* resizeArray(int* oldArr, int oldSize, int newSize) {
    // Alokasi array baru
    int* newArr = new int[newSize];
    
    // Copy data lama
    int copySize = (oldSize < newSize) ? oldSize : newSize;
    for (int i = 0; i < copySize; i++) {
        newArr[i] = oldArr[i];
    }
    
    // Inisialisasi elemen baru jika array membesar
    for (int i = oldSize; i < newSize; i++) {
        newArr[i] = 0;
    }
    
    // Hapus array lama
    delete[] oldArr;
    
    return newArr;
}

int main() {
    int kapasitas = 3;
    int* arr = new int[kapasitas];
    
    // Isi array awal
    for (int i = 0; i < kapasitas; i++) {
        arr[i] = (i + 1) * 10;
    }
    
    cout << "Array awal (kapasitas " << kapasitas << "): ";
    for (int i = 0; i < kapasitas; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
    
    // Perbesar array
    kapasitas = 6;
    arr = resizeArray(arr, 3, kapasitas);
    
    // Isi elemen baru
    for (int i = 3; i < kapasitas; i++) {
        arr[i] = (i + 1) * 10;
    }
    
    cout << "Array setelah resize (kapasitas " << kapasitas << "): ";
    for (int i = 0; i < kapasitas; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
    
    delete[] arr;
    return 0;
}
```

### 11.9.2 Linked List Sederhana

Linked list adalah struktur data dimana setiap elemen (node) menyimpan data dan pointer ke node berikutnya. Ini adalah aplikasi klasik dari pointer.

```cpp
#include <iostream>
using namespace std;

// Struktur Node
struct Node {
    int data;
    Node* next;
};

// Fungsi untuk menambah node di awal
void insertAwal(Node** head, int nilai) {
    Node* newNode = new Node();
    newNode->data = nilai;
    newNode->next = *head;
    *head = newNode;
}

// Fungsi untuk menampilkan linked list
void tampilkanList(Node* head) {
    Node* current = head;
    while (current != nullptr) {
        cout << current->data;
        if (current->next != nullptr) {
            cout << " -> ";
        }
        current = current->next;
    }
    cout << endl;
}

// Fungsi untuk menghitung panjang list
int hitungPanjang(Node* head) {
    int count = 0;
    Node* current = head;
    while (current != nullptr) {
        count++;
        current = current->next;
    }
    return count;
}

// Fungsi untuk membersihkan linked list
void hapusList(Node** head) {
    Node* current = *head;
    Node* next;
    
    while (current != nullptr) {
        next = current->next;
        delete current;
        current = next;
    }
    
    *head = nullptr;
}

int main() {
    Node* head = nullptr;
    
    // Tambah beberapa node
    insertAwal(&head, 30);
    insertAwal(&head, 20);
    insertAwal(&head, 10);
    
    cout << "Linked List: ";
    tampilkanList(head);
    
    cout << "Panjang list: " << hitungPanjang(head) << endl;
    
    // Bersihkan memori
    hapusList(&head);
    cout << "List telah dihapus." << endl;
    
    return 0;
}
```

### 11.9.3 String Manipulation dengan Pointer

Pointer sangat berguna untuk manipulasi string karena string dalam C++ (C-style) adalah array of characters.

```cpp
#include <iostream>
#include <cstring>
using namespace std;

// Fungsi untuk menghitung panjang string
int hitungPanjang(const char* str) {
    int len = 0;
    while (*str != '\0') {
        len++;
        str++;
    }
    return len;
}

// Fungsi untuk copy string
void copyString(char* dest, const char* src) {
    while (*src != '\0') {
        *dest = *src;
        dest++;
        src++;
    }
    *dest = '\0';  // Null terminator
}

// Fungsi untuk reverse string
void reverseString(char* str) {
    char* start = str;
    char* end = str;
    
    // Cari akhir string
    while (*end != '\0') {
        end++;
    }
    end--;  // Mundur dari null terminator
    
    // Swap karakter
    while (start < end) {
        char temp = *start;
        *start = *end;
        *end = temp;
        start++;
        end--;
    }
}

int main() {
    const char* original = "Hello World";
    
    // Copy string
    char* copy = new char[strlen(original) + 1];
    copyString(copy, original);
    cout << "Original: " << original << endl;
    cout << "Copy: " << copy << endl;
    
    // Reverse string
    reverseString(copy);
    cout << "Reversed: " << copy << endl;
    
    // Hitung panjang
    cout << "Panjang: " << hitungPanjang(original) << endl;
    
    delete[] copy;
    return 0;
}
```

## 11.10 Best Practices dan Debugging

### 11.10.1 Best Practices Penggunaan Pointer

Berikut adalah pedoman penting untuk menggunakan pointer dengan aman:

```cpp
#include <iostream>
using namespace std;

int main() {
    // 1. Selalu inisialisasi pointer
    int* ptr = nullptr;  // BAIK
    // int* bad_ptr;     // BURUK: Tidak diinisialisasi
    
    // 2. Cek nullptr sebelum dereference
    if (ptr != nullptr) {
        cout << *ptr << endl;
    } else {
        cout << "Pointer adalah null" << endl;
    }
    
    // 3. Set ke nullptr setelah delete
    int* temp = new int(42);
    delete temp;
    temp = nullptr;  // PENTING!
    
    // 4. Gunakan smart pointers (C++11+) untuk automatic memory management
    // #include <memory>
    // unique_ptr<int> smartPtr = make_unique<int>(100);
    // Tidak perlu delete, otomatis di-cleanup
    
    // 5. Hindari multiple pointer ke same memory (ownership problem)
    int* ptr1 = new int(10);
    // int* ptr2 = ptr1;  // Hati-hati: siapa yang bertanggung jawab delete?
    // delete ptr1;        // ptr2 sekarang dangling!
    
    // 6. Gunakan const untuk pointer yang tidak seharusnya diubah
    const int* safePtr = ptr1;
    // *safePtr = 20;  // Compile error: melindungi dari modifikasi
    
    delete ptr1;
    ptr1 = nullptr;
    
    return 0;
}
```

### 11.10.2 Common Pointer Errors

```cpp
#include <iostream>
using namespace std;

void demonstrasiErrors() {
    // ERROR 1: Uninitialized pointer
    // int* ptr;
    // cout << *ptr << endl;  // Undefined behavior!
    
    // ERROR 2: Memory leak
    for (int i = 0; i < 1000; i++) {
        int* leak = new int[100];
        // Tidak ada delete[]  ← MEMORY LEAK!
    }
    
    // ERROR 3: Dangling pointer
    int* ptr = new int(42);
    delete ptr;
    // cout << *ptr << endl;  // Undefined behavior!
    
    // ERROR 4: Double delete
    int* ptr2 = new int(100);
    delete ptr2;
    // delete ptr2;  // CRASH atau corruption!
    
    // ERROR 5: delete vs delete[]
    int* arr = new int[10];
    // delete arr;    // WRONG! Should be delete[]
    delete[] arr;     // CORRECT
    
    // ERROR 6: Returning pointer to local variable
    // int* getBadPointer() {
    //     int x = 10;
    //     return &x;  // DANGER: x will be destroyed!
    // }
}

int main() {
    cout << "Lihat komentar dalam kode untuk error examples" << endl;
    return 0;
}
```

### 11.10.3 Debugging Pointer dengan Tools

```cpp
#include <iostream>
using namespace std;

// Fungsi dengan potential bug
void demonstrasiDebugging() {
    int* arr = new int[5];
    
    // Fill array
    for (int i = 0; i < 5; i++) {
        arr[i] = i * 10;
    }
    
    // Print array
    cout << "Array: ";
    for (int i = 0; i < 5; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
    
    // Proper cleanup
    delete[] arr;
    arr = nullptr;
    
    // Technique: Print pointer values for debugging
    cout << "Pointer setelah delete: " << arr << endl;
}

int main() {
    cout << "=== Debugging Techniques ===" << endl;
    
    // 1. Print pointer addresses
    int x = 10;
    int* ptr = &x;
    cout << "Alamat variabel: " << &x << endl;
    cout << "Nilai pointer: " << ptr << endl;
    cout << "Nilai yang ditunjuk: " << *ptr << endl;
    
    // 2. Check for nullptr
    int* nullPtr = nullptr;
    if (nullPtr) {
        cout << "Pointer valid" << endl;
    } else {
        cout << "Pointer adalah null" << endl;
    }
    
    // 3. Use assertions (in debug mode)
    // #include <cassert>
    // assert(ptr != nullptr && "Pointer should not be null!");
    
    demonstrasiDebugging();
    
    cout << "\nTools untuk debugging pointer:" << endl;
    cout << "1. Valgrind (Linux): valgrind --leak-check=full ./program" << endl;
    cout << "2. AddressSanitizer (GCC/Clang): -fsanitize=address" << endl;
    cout << "3. Visual Studio: Memory leak detection" << endl;
    cout << "4. GDB: info locals, print *ptr, x/10x ptr" << endl;
    
    return 0;
}
```

## 11.11 Ringkasan

Pada bab ini, kita telah mempelajari konsep pointer dan manajemen memori dinamis dalam C++. Pointer adalah variabel yang menyimpan alamat memori dan memberikan kita kontrol langsung terhadap memori komputer. Kita telah membahas operator dasar pointer (& dan *), hubungan erat antara pointer dan array, serta pointer arithmetic yang memungkinkan navigasi melalui memori.

Manajemen memori dinamis menggunakan operator `new` dan `delete` memberikan fleksibilitas untuk mengalokasikan memori sesuai kebutuhan saat runtime. Namun dengan kekuatan ini datang tanggung jawab: kita harus memastikan setiap alokasi memori di-dealokasikan dengan benar untuk menghindari memory leak. Kita juga harus berhati-hati dengan dangling pointer dan double delete yang dapat menyebabkan program crash.

Pointer memiliki banyak aplikasi praktis seperti dynamic array resizing, implementasi struktur data seperti linked list, dan manipulasi string yang efisien. Dengan memahami pointer secara mendalam, pintu terbuka ke konsep pemrograman lanjutan dan struktur data yang lebih kompleks. Best practices seperti selalu menginisialisasi pointer, memeriksa nullptr sebelum dereference, dan menggunakan debugging tools akan membantu kita menulis kode yang lebih robust dan aman.

## 11.12 Referensi

1. Deitel, P. J., & Deitel, H. M. (2020). *C++ How to Program* (10th ed.). Pearson. Chapter 8: Pointers.

2. Savitch, W. (2017). *Problem Solving with C++* (10th ed.). Pearson. Chapter 9: Pointers and Dynamic Arrays.

3. Stroustrup, B. (2014). *Programming: Principles and Practice Using C++* (2nd ed.). Addison-Wesley. Chapter 17: Vector and Free Store.

4. Lippman, S. B., Lajoie, J., & Moo, B. E. (2012). *C++ Primer* (5th ed.). Addison-Wesley. Chapter 12: Dynamic Memory.

5. Meyers, S. (2014). *Effective Modern C++*. O'Reilly Media. Items 18-22: Smart Pointers.

## 11.13 Soal Latihan

### Latihan Dasar

1. Buatlah program yang mendeklarasikan sebuah variabel integer, kemudian buatlah pointer yang menunjuk ke variabel tersebut. Tampilkan nilai variabel, alamat variabel, nilai pointer, dan nilai yang ditunjuk pointer.

2. Tulislah fungsi `tukarNilai(int* a, int* b)` yang menukar nilai dua variabel menggunakan pointer. Test fungsi tersebut di `main()`.

3. Buatlah program yang mengalokasikan array dinamis berukuran n (input dari user), isi array dengan bilangan genap, tampilkan isinya, kemudian dealokasikan memory dengan benar.

### Latihan Menengah

4. Implementasikan fungsi `int* cariNilai(int* arr, int ukuran, int target)` yang mencari nilai dalam array dan mengembalikan pointer ke elemen pertama yang cocok, atau `nullptr` jika tidak ditemukan.

5. Buatlah program yang membuat matrix dinamis berukuran m x n, isi dengan bilangan random 1-100, tampilkan matrix, kemudian hitung dan tampilkan jumlah setiap baris dan setiap kolom.

6. Tulislah fungsi `char* gabungString(const char* str1, const char* str2)` yang menggabungkan dua string dan mengembalikan string baru yang dialokasikan secara dinamis.

### Latihan Lanjutan

7. Implementasikan struktur data linked list sederhana dengan fungsi-fungsi: `insertAwal()`, `insertAkhir()`, `hapusNode()`, `cariNode()`, dan `tampilkanList()`. Pastikan memory management yang proper.

8. Buatlah program yang mensimulasikan dynamic array (seperti `std::vector`). Implementasikan fungsi `push_back()` yang secara otomatis memperbesar kapasitas array ketika penuh (misalnya double kapasitas).

## 11.14 Soal Diskusi

1. Jelaskan perbedaan antara stack memory dan heap memory. Kapan sebaiknya kita menggunakan alokasi dinamis dibanding array statik?

2. Apa yang dimaksud dengan memory leak? Berikan contoh situasi dalam program yang dapat menyebabkan memory leak dan jelaskan cara mencegahnya.

3. Mengapa C++ memerlukan programmer untuk secara manual manage memory (new/delete), sementara bahasa seperti Java atau Python menggunakan garbage collection otomatis? Apa trade-off nya?

4. Jelaskan perbedaan antara `delete ptr` dan `delete[] ptr`. Apa yang terjadi jika kita salah menggunakan keduanya?

5. Dalam konteks modern C++, apakah kita masih perlu menggunakan raw pointer? Diskusikan alternatif yang lebih aman seperti smart pointers (`unique_ptr`, `shared_ptr`).

6. Bagaimana pointer dapat digunakan untuk membuat program yang lebih efisien? Berikan contoh kasus dimana passing pointer ke fungsi lebih baik daripada passing by value.

7. Apa bahaya dari dangling pointer dan bagaimana cara menghindarinya? Mengapa setting pointer ke `nullptr` setelah `delete` adalah good practice?

8. Diskusikan kenapa pemahaman tentang pointer penting untuk mempelajari struktur data lanjutan seperti tree dan graph. Bagaimana pointer memungkinkan implementasi struktur data ini?
