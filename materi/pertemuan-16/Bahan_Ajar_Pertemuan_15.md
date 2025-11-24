# BAB 15: C++ DI PLATFORM LAIN DAN DEVELOPMENT TOOLS

## 15.1 Pendahuluan

Selamat datang di pertemuan ketigabelas mata kuliah Dasar-Dasar Pemrograman. Sejauh ini, kita telah mempelajari berbagai konsep fundamental pemrograman C++ mulai dari struktur kontrol, fungsi, array, pointer, hingga struct. Pada pertemuan ini, kita akan melangkah keluar dari lingkungan pembelajaran konvensional dan mengeksplorasi bagaimana C++ digunakan di berbagai platform dan domain aplikasi yang berbeda.

C++ bukan hanya bahasa pemrograman untuk membuat aplikasi desktop atau program konsol sederhana. Bahasa ini memiliki jangkauan yang sangat luas dan telah terbukti menjadi tulang punggung dari berbagai sistem dan aplikasi yang kita gunakan setiap hari. Dari perangkat Internet of Things (IoT) yang sangat kecil seperti Arduino, hingga game AAA yang kompleks, dari sistem operasi hingga aplikasi high-performance computing, C++ hadir di mana-mana.

Pada bab ini, kita akan menjelajahi empat domain utama penggunaan C++. Pertama, kita akan melihat bagaimana C++ digunakan dalam embedded systems dan mikrokontroler seperti Arduino dan ESP32. Kedua, kita akan membahas penggunaan C++ dalam competitive programming, di mana efisiensi dan kecepatan eksekusi menjadi sangat penting. Ketiga, kita akan mengenal dunia game development menggunakan C++. Terakhir, kita akan memahami bagaimana mengembangkan aplikasi C++ yang cross-platform dan berbagai tools yang mendukung proses development.

Pemahaman tentang berbagai aplikasi C++ ini tidak hanya akan memperluas wawasan kita, tetapi juga memberikan motivasi dan konteks praktis mengapa konsep-konsep yang telah kita pelajari sangat penting. Mari kita mulai perjalanan eksplorasi ini!

## 13.2 C++ untuk Embedded Systems

### 13.2.1 Pengenalan Embedded Systems

Embedded system adalah sistem komputer yang dirancang untuk melakukan fungsi-fungsi spesifik sebagai bagian dari sistem yang lebih besar. Berbeda dengan komputer general-purpose yang kita gunakan sehari-hari, embedded system biasanya memiliki sumber daya yang terbatas (memori, processing power, dan energi) namun dioptimalkan untuk tugas tertentu. Contoh embedded system ada di sekitar kita: mesin cuci, kulkas, kamera digital, printer, bahkan di dalam mobil modern terdapat puluhan embedded system yang mengontrol berbagai fungsi.

C++ menjadi pilihan populer untuk embedded programming karena beberapa alasan. Pertama, C++ memberikan kontrol tingkat rendah terhadap hardware, memungkinkan programmer untuk mengakses register, pin, dan sumber daya hardware secara langsung. Kedua, C++ efisien dalam penggunaan memori dan CPU, yang sangat penting mengingat keterbatasan resource pada embedded system. Ketiga, C++ mendukung paradigma object-oriented yang membantu mengorganisir kode yang kompleks dengan lebih baik. Keempat, C++ kompatibel dengan C, sehingga dapat menggunakan library dan driver yang ditulis dalam C.

Arduino adalah salah satu platform embedded yang paling populer untuk pembelajaran dan prototyping. Arduino menggunakan bahasa pemrograman yang berbasis C++, meskipun dengan beberapa abstraksi dan library khusus untuk memudahkan penggunaan. Platform ini terdiri dari board mikrokontroler (seperti Arduino Uno, Nano, Mega) dan Integrated Development Environment (IDE) yang memudahkan proses penulisan, kompilasi, dan upload program ke board.

### 13.2.2 Setup Development Environment untuk Arduino

Untuk memulai pemrograman Arduino, kita perlu menginstall Arduino IDE yang dapat diunduh gratis dari website resmi Arduino (arduino.cc). Proses instalasi cukup straightforward di berbagai sistem operasi, baik Windows, macOS, maupun Linux. Setelah instalasi selesai, kita perlu melakukan beberapa konfigurasi dasar.

Langkah pertama adalah memilih board yang akan digunakan melalui menu Tools > Board. Misalnya, jika kita menggunakan Arduino Uno, kita pilih "Arduino Uno" dari daftar board yang tersedia. Langkah kedua adalah memilih port komunikasi yang benar melalui menu Tools > Port. Ini adalah port USB di mana Arduino terhubung ke komputer. Di Windows, biasanya terlihat sebagai "COM3", "COM4", dan seterusnya, sedangkan di macOS dan Linux biasanya "/dev/ttyUSB0" atau "/dev/cu.usbmodem".

Arduino IDE memiliki struktur program yang sedikit berbeda dari program C++ standar yang kita pelajari sebelumnya. Setiap program Arduino (disebut "sketch") harus memiliki dua fungsi utama: `setup()` dan `loop()`. Fungsi `setup()` dipanggil sekali saat Arduino pertama kali dinyalakan atau direset, biasanya digunakan untuk inisialisasi pin, variable, atau library. Fungsi `loop()` dipanggil berulang-ulang selama Arduino menyala, di sinilah logika utama program berjalan.

```cpp
// Program Arduino Dasar - Struktur Minimal
void setup() {
  // Kode inisialisasi di sini
  // Dijalankan sekali saat startup
}

void loop() {
  // Kode program utama di sini
  // Dijalankan berulang-ulang
}
```

**Gambar 13.1:** [Struktur dasar program Arduino menunjukkan flow eksekusi dari setup() yang dipanggil sekali, kemudian loop() yang dipanggil berulang-ulang]

### 13.2.3 Digital I/O dan Program Blink LED

Salah satu hal paling fundamental dalam embedded programming adalah kemampuan untuk mengontrol pin digital. Pin digital dapat berada dalam dua state: HIGH (biasanya 5V atau 3.3V) atau LOW (0V). Kita dapat menggunakan pin digital sebagai output untuk mengontrol LED, relay, motor, atau komponen lain. Kita juga dapat menggunakannya sebagai input untuk membaca state dari tombol, sensor digital, atau sinyal dari perangkat lain.

Untuk menggunakan pin digital sebagai output, kita perlu mengkonfigurasinya terlebih dahulu dalam fungsi `setup()` menggunakan fungsi `pinMode()`. Fungsi ini menerima dua parameter: nomor pin dan mode (INPUT atau OUTPUT). Setelah dikonfigurasi, kita dapat mengatur state pin menggunakan fungsi `digitalWrite()` yang menerima nomor pin dan value (HIGH atau LOW).

Mari kita lihat program klasik "Blink" yang merupakan equivalent dari "Hello World" dalam dunia embedded programming. Program ini akan membuat LED berkedip dengan interval tertentu. Kebanyakan board Arduino memiliki LED built-in yang terhubung ke pin 13, sehingga kita tidak perlu menambahkan komponen eksternal.

```cpp
// Program Blink LED - Program Klasik Arduino
const int LED_PIN = 13;  // Pin LED built-in pada Arduino Uno
const int DELAY_MS = 1000;  // Delay 1 detik

void setup() {
  // Set pin LED sebagai output
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_PIN, HIGH);  // Nyalakan LED
  delay(DELAY_MS);               // Tunggu 1 detik
  digitalWrite(LED_PIN, LOW);   // Matikan LED
  delay(DELAY_MS);               // Tunggu 1 detik
}
```

**Gambar 13.2:** [Diagram timing menunjukkan sinyal HIGH dan LOW yang bergantian pada pin LED dengan interval delay]

Program di atas sangat sederhana namun mendemonstrasikan konsep penting. Kita menggunakan konstanta untuk mendefinisikan pin dan delay, yang merupakan good practice karena memudahkan maintenance dan perubahan. Fungsi `delay()` menghentikan eksekusi program untuk waktu tertentu (dalam milidetik), sehingga kita dapat melihat LED berkedip.

Kita dapat mengembangkan program ini lebih lanjut untuk membuat pola kedipan yang lebih kompleks. Misalnya, kita bisa membuat pola Morse code atau membuat LED berkedip dengan kecepatan yang berbeda. Kita juga bisa menggunakan multiple LED untuk membuat pola cahaya yang menarik.

```cpp
// Program Blink dengan Pola Berbeda
const int LED_PIN = 13;

void setup() {
  pinMode(LED_PIN, OUTPUT);
}

void loop() {
  // Pola: kedip cepat 3 kali
  for(int i = 0; i < 3; i++) {
    digitalWrite(LED_PIN, HIGH);
    delay(200);
    digitalWrite(LED_PIN, LOW);
    delay(200);
  }
  
  // Pause
  delay(1000);
  
  // Pola: kedip lambat 2 kali
  for(int i = 0; i < 2; i++) {
    digitalWrite(LED_PIN, HIGH);
    delay(500);
    digitalWrite(LED_PIN, LOW);
    delay(500);
  }
  
  // Pause
  delay(1000);
}
```

**Gambar 13.3:** [Diagram timing menunjukkan pola kedipan yang berbeda: cepat 3x, pause, lambat 2x, pause, kemudian repeat]

### 13.2.4 Membaca Input Digital

Selain mengontrol output, kita juga perlu bisa membaca input dari berbagai sumber. Input digital yang paling sederhana adalah tombol push button. Ketika tombol ditekan, pin akan membaca HIGH atau LOW tergantung pada konfigurasi circuit (pull-up atau pull-down).

Arduino memiliki fitur internal pull-up resistor yang dapat diaktifkan dengan menggunakan mode `INPUT_PULLUP`. Ini sangat memudahkan karena kita tidak perlu menambahkan resistor eksternal. Dengan konfigurasi pull-up, pin akan membaca HIGH saat tombol tidak ditekan, dan LOW saat tombol ditekan.

```cpp
// Program Membaca Tombol dan Kontrol LED
const int BUTTON_PIN = 2;  // Pin untuk tombol
const int LED_PIN = 13;     // Pin untuk LED

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT_PULLUP);  // Aktifkan internal pull-up
}

void loop() {
  // Baca state tombol
  int buttonState = digitalRead(BUTTON_PIN);
  
  // Jika tombol ditekan (LOW karena pull-up)
  if (buttonState == LOW) {
    digitalWrite(LED_PIN, HIGH);  // Nyalakan LED
  } else {
    digitalWrite(LED_PIN, LOW);   // Matikan LED
  }
}
```

**Gambar 13.4:** [Diagram circuit menunjukkan tombol terhubung ke pin 2 dengan internal pull-up, dan LED terhubung ke pin 13]

Program di atas membuat LED menyala selama tombol ditekan. Ini adalah contoh interaksi dasar antara input dan output. Kita dapat mengembangkan ini lebih lanjut untuk membuat aplikasi yang lebih kompleks, seperti toggle LED (LED berubah state setiap kali tombol ditekan) atau menghitung jumlah penekanan tombol.

### 13.2.5 Analog Input dan Sensor Reading

Selain pin digital, Arduino juga memiliki pin analog input yang dapat membaca nilai antara 0 hingga 1023, merepresentasikan voltage antara 0V hingga reference voltage (biasanya 5V atau 3.3V). Ini sangat berguna untuk membaca sensor analog seperti sensor suhu, sensor cahaya (LDR), potensiometer, dan banyak sensor lainnya.

Untuk membaca nilai analog, kita menggunakan fungsi `analogRead()` yang mengembalikan integer antara 0-1023. Nilai ini kemudian dapat kita konversi atau mapping sesuai kebutuhan. Misalnya, jika kita membaca sensor suhu, kita perlu mengkonversi nilai ADC (Analog to Digital Converter) menjadi derajat Celsius.

```cpp
// Program Membaca Sensor Suhu LM35
const int TEMP_PIN = A0;  // Pin analog untuk sensor

void setup() {
  Serial.begin(9600);  // Inisialisasi komunikasi serial
}

void loop() {
  // Baca nilai dari sensor
  int sensorValue = analogRead(TEMP_PIN);
  
  // Konversi ke voltage (0-5V menjadi 0-1023)
  float voltage = sensorValue * (5.0 / 1023.0);
  
  // LM35 menghasilkan 10mV per derajat Celsius
  float temperatureC = voltage * 100.0;
  
  // Tampilkan hasil ke serial monitor
  Serial.print("Sensor Value: ");
  Serial.print(sensorValue);
  Serial.print(" | Voltage: ");
  Serial.print(voltage);
  Serial.print("V | Temperature: ");
  Serial.print(temperatureC);
  Serial.println(" C");
  
  delay(1000);  // Baca setiap 1 detik
}
```

**Gambar 13.5:** [Diagram menunjukkan konversi dari nilai ADC (0-1023) ke voltage (0-5V) ke suhu (°C)]

### 13.2.6 Serial Communication

Serial communication adalah cara Arduino berkomunikasi dengan komputer atau perangkat lain. Ini sangat berguna untuk debugging, logging data, atau mengirim command ke Arduino. Arduino menggunakan UART (Universal Asynchronous Receiver-Transmitter) untuk serial communication melalui USB.

Untuk menggunakan serial communication, kita perlu menginisialisasi dengan `Serial.begin()` yang menerima parameter baud rate (kecepatan komunikasi dalam bits per second). Baud rate yang umum digunakan adalah 9600, 115200, atau nilai lainnya. Pastikan baud rate di Arduino sketch sama dengan yang diset di Serial Monitor.

```cpp
// Program Demonstrasi Serial Communication
void setup() {
  Serial.begin(9600);  // Mulai serial dengan baud rate 9600
  
  // Kirim pesan awal
  Serial.println("=== Arduino Serial Demo ===");
  Serial.println("Ketik sesuatu dan tekan Enter");
}

void loop() {
  // Cek apakah ada data yang diterima
  if (Serial.available() > 0) {
    // Baca string sampai newline
    String input = Serial.readStringUntil('\n');
    
    // Echo kembali dengan tambahan informasi
    Serial.print("Anda mengetik: ");
    Serial.println(input);
    Serial.print("Panjang string: ");
    Serial.println(input.length());
    
    // Konversi ke uppercase dan kirim
    input.toUpperCase();
    Serial.print("Uppercase: ");
    Serial.println(input);
  }
}
```

**Gambar 13.6:** [Diagram menunjukkan aliran data bidirectional antara Arduino dan komputer melalui USB serial]

Serial communication juga dapat digunakan untuk mengirim data sensor ke komputer untuk diproses lebih lanjut atau divisualisasikan. Kita juga dapat mengirim perintah dari komputer ke Arduino untuk mengontrol berbagai komponen.

### 13.2.7 ESP32 dan WiFi Connectivity

ESP32 adalah mikrokontroler yang lebih powerful dibanding Arduino tradisional. ESP32 memiliki processor dual-core, WiFi dan Bluetooth built-in, lebih banyak memory, dan lebih banyak pin I/O. Ini membuat ESP32 sangat cocok untuk aplikasi IoT (Internet of Things).

Programming ESP32 menggunakan Arduino IDE dengan menambahkan board manager untuk ESP32. Struktur program sama dengan Arduino, namun ESP32 memiliki library tambahan untuk WiFi, Bluetooth, dan fitur-fitur lain. Mari kita lihat contoh koneksi ESP32 ke WiFi:

```cpp
// Program ESP32 WiFi Connection
#include <WiFi.h>

const char* ssid = "NamaWiFi";  // Ganti dengan nama WiFi Anda
const char* password = "PasswordWiFi";  // Ganti dengan password WiFi

void setup() {
  Serial.begin(115200);
  delay(1000);
  
  Serial.println();
  Serial.print("Connecting to ");
  Serial.println(ssid);
  
  // Mulai koneksi WiFi
  WiFi.begin(ssid, password);
  
  // Tunggu sampai terkoneksi
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  
  Serial.println();
  Serial.println("WiFi connected!");
  Serial.print("IP address: ");
  Serial.println(WiFi.localIP());
}

void loop() {
  // Cek status koneksi
  if (WiFi.status() == WL_CONNECTED) {
    Serial.println("Still connected to WiFi");
  } else {
    Serial.println("WiFi disconnected!");
  }
  
  delay(5000);
}
```

**Gambar 13.7:** [Diagram menunjukkan ESP32 terhubung ke WiFi router dan dapat berkomunikasi dengan server di internet]

Dengan koneksi WiFi, ESP32 dapat mengirim data sensor ke cloud, menerima perintah dari aplikasi smartphone, atau berkomunikasi dengan perangkat IoT lainnya. Ini membuka kemungkinan untuk membuat aplikasi home automation, monitoring system, atau berbagai project IoT lainnya.

## 13.3 C++ untuk Competitive Programming

### 13.3.1 Pengenalan Competitive Programming

Competitive programming adalah sport mental di mana peserta menyelesaikan masalah algoritma dalam waktu terbatas. Platform populer untuk competitive programming termasuk Codeforces, CodeChef, AtCoder, HackerRank, dan LeetCode. C++ adalah bahasa yang paling populer di competitive programming karena kecepatannya dan library STL (Standard Template Library) yang powerful.

Dalam competitive programming, kecepatan eksekusi program sangat penting karena ada time limit untuk setiap problem. Algoritma yang efisien dan implementasi yang optimal dapat membuat perbedaan antara "Accepted" dan "Time Limit Exceeded". C++ memberikan kontrol yang baik terhadap performance dan memiliki compiler yang menghasilkan kode yang sangat cepat.

Selain kecepatan eksekusi, kecepatan coding juga penting dalam competitive programming. Peserta perlu menulis kode dengan cepat namun tetap akurat. Ini memerlukan pemahaman mendalam tentang algoritma dan data struktur, serta kemampuan untuk mengimplementasikannya dengan cepat. Banyak competitive programmer menggunakan template code dan macro untuk mempercepat proses coding.

### 13.3.2 Fast Input/Output Techniques

Dalam competitive programming, I/O (Input/Output) bisa menjadi bottleneck jika tidak dioptimasi. C++ standard I/O (`cin` dan `cout`) biasanya lebih lambat dibanding C-style I/O (`scanf` dan `printf`) karena sinkronisasi dengan C stream dan format checking yang lebih kompleks.

Ada beberapa teknik untuk mempercepat I/O dalam C++. Pertama, kita dapat menonaktifkan sinkronisasi antara C++ stream dan C stream menggunakan `ios_base::sync_with_stdio(false)`. Kedua, kita dapat memutuskan tie antara `cin` dan `cout` menggunakan `cin.tie(NULL)`. Ketiga, untuk input yang sangat besar, kita dapat menggunakan `scanf` dan `printf` atau bahkan implementasi custom I/O.

```cpp
// Template Fast I/O untuk Competitive Programming
#include <iostream>
#include <cstdio>
using namespace std;

int main() {
    // Optimasi I/O
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
    
    int n;
    cin >> n;
    
    for(int i = 0; i < n; i++) {
        int x;
        cin >> x;
        // Process x
        cout << x * 2 << "\n";  // Gunakan "\n" bukan endl
    }
    
    return 0;
}
```

**Gambar 13.8:** [Perbandingan waktu eksekusi antara standard I/O, optimized I/O, dan C-style I/O untuk input besar]

Perhatikan bahwa kita menggunakan `"\n"` instead of `endl`. Ini karena `endl` melakukan flush buffer setiap kali dipanggil, yang memperlambat output. Untuk output yang besar, perbedaan ini bisa sangat significant.

### 13.3.3 Common Data Structures dalam Competitive Programming

STL (Standard Template Library) menyediakan berbagai data struktur yang sangat berguna dalam competitive programming. Memahami kapan dan bagaimana menggunakan data struktur yang tepat adalah kunci untuk menyelesaikan problem dengan efisien.

Vector adalah dynamic array yang sangat sering digunakan. Berbeda dengan array biasa yang ukurannya fixed, vector dapat bertumbuh secara dinamis. Vector juga menyediakan berbagai fungsi helper seperti `push_back()`, `pop_back()`, `size()`, dan lainnya.

```cpp
// Penggunaan Vector dalam Competitive Programming
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
    int n;
    cin >> n;
    
    vector<int> arr(n);  // Vector dengan ukuran n
    
    // Input
    for(int i = 0; i < n; i++) {
        cin >> arr[i];
    }
    
    // Sort array
    sort(arr.begin(), arr.end());
    
    // Find maximum dan minimum
    int maxVal = *max_element(arr.begin(), arr.end());
    int minVal = *min_element(arr.begin(), arr.end());
    
    // Output
    cout << "Max: " << maxVal << "\n";
    cout << "Min: " << minVal << "\n";
    
    return 0;
}
```

**Gambar 13.9:** [Diagram menunjukkan operasi-operasi umum pada vector: push_back, pop_back, sort, find]

Set dan map adalah data struktur berbasis tree yang sangat berguna. Set menyimpan element unik dalam sorted order, sedangkan map menyimpan key-value pairs. Keduanya memiliki complexity O(log n) untuk insert, delete, dan search.

```cpp
// Penggunaan Set dan Map
#include <iostream>
#include <set>
#include <map>
using namespace std;

int main() {
    // Set untuk menyimpan element unik
    set<int> uniqueNumbers;
    uniqueNumbers.insert(5);
    uniqueNumbers.insert(3);
    uniqueNumbers.insert(5);  // Duplicate, tidak akan diinsert
    uniqueNumbers.insert(1);
    
    // Set otomatis sorted
    for(int num : uniqueNumbers) {
        cout << num << " ";  // Output: 1 3 5
    }
    cout << "\n";
    
    // Map untuk frequency counting
    map<char, int> frequency;
    string text = "hello world";
    
    for(char c : text) {
        frequency[c]++;
    }
    
    // Tampilkan frequency
    for(auto pair : frequency) {
        cout << pair.first << ": " << pair.second << "\n";
    }
    
    return 0;
}
```

**Gambar 13.10:** [Visualisasi struktur internal set (balanced BST) dan map (key-value pairs dalam BST)]

### 13.3.4 Common Algorithms

Competitive programming sering melibatkan algoritma klasik seperti sorting, searching, dan graph traversal. STL menyediakan implementasi yang sudah dioptimasi untuk algoritma-algoritma ini.

Sorting adalah salah satu operasi paling umum. STL menyediakan fungsi `sort()` yang menggunakan Introsort (hybrid dari Quicksort, Heapsort, dan Insertion sort) dengan average complexity O(n log n).

```cpp
// Berbagai Teknik Sorting
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

// Custom comparator untuk sorting descending
bool descending(int a, int b) {
    return a > b;
}

// Struct dengan custom comparator
struct Student {
    string name;
    int score;
};

bool compareByScore(Student a, Student b) {
    return a.score > b.score;  // Sort by score descending
}

int main() {
    vector<int> arr = {5, 2, 8, 1, 9};
    
    // Sort ascending (default)
    sort(arr.begin(), arr.end());
    
    // Sort descending
    sort(arr.begin(), arr.end(), descending);
    // Atau: sort(arr.begin(), arr.end(), greater<int>());
    
    // Sort struct
    vector<Student> students = {
        {"Alice", 85},
        {"Bob", 92},
        {"Charlie", 78}
    };
    
    sort(students.begin(), students.end(), compareByScore);
    
    for(Student s : students) {
        cout << s.name << ": " << s.score << "\n";
    }
    
    return 0;
}
```

**Gambar 13.11:** [Flowchart menunjukkan proses Introsort: mulai dengan Quicksort, switch ke Heapsort jika rekursi terlalu dalam, gunakan Insertion sort untuk subarray kecil]

Binary search adalah algoritma pencarian yang sangat efisien dengan complexity O(log n), namun memerlukan array yang sudah sorted. STL menyediakan fungsi `binary_search()`, `lower_bound()`, dan `upper_bound()`.

```cpp
// Binary Search dan Variasinya
#include <iostream>
#include <algorithm>
#include <vector>
using namespace std;

int main() {
    vector<int> arr = {1, 3, 3, 3, 5, 7, 9};
    
    // Binary search - return true/false
    bool found = binary_search(arr.begin(), arr.end(), 3);
    cout << "3 found: " << (found ? "Yes" : "No") << "\n";
    
    // Lower bound - iterator ke element pertama >= value
    auto lb = lower_bound(arr.begin(), arr.end(), 3);
    cout << "Lower bound of 3: index " << (lb - arr.begin()) << "\n";
    
    // Upper bound - iterator ke element pertama > value
    auto ub = upper_bound(arr.begin(), arr.end(), 3);
    cout << "Upper bound of 3: index " << (ub - arr.begin()) << "\n";
    
    // Count occurrences menggunakan bound
    int count = ub - lb;
    cout << "Count of 3: " << count << "\n";
    
    return 0;
}
```

**Gambar 13.12:** [Visualisasi array sorted dengan penanda lower_bound dan upper_bound untuk nilai 3]

### 13.3.5 Template Code untuk Competitive Programming

Banyak competitive programmer menggunakan template code untuk mempercepat setup awal. Template ini biasanya berisi macro untuk shortcut, fast I/O setup, dan common includes.

```cpp
// Template Competitive Programming
#include <bits/stdc++.h>  // Include semua STL headers
using namespace std;

// Type aliases
typedef long long ll;
typedef vector<int> vi;
typedef vector<ll> vll;
typedef pair<int, int> pii;

// Macros
#define pb push_back
#define mp make_pair
#define F first
#define S second
#define all(x) x.begin(), x.end()
#define REP(i, a, b) for(int i = a; i < b; i++)
#define REPR(i, a, b) for(int i = a; i >= b; i--)

// Fast I/O
void fastIO() {
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);
}

int main() {
    fastIO();
    
    int t;
    cin >> t;
    
    while(t--) {
        int n;
        cin >> n;
        
        vi arr(n);
        REP(i, 0, n) {
            cin >> arr[i];
        }
        
        sort(all(arr));
        
        // Process...
        
        cout << arr[0] << "\n";
    }
    
    return 0;
}
```

**Gambar 13.13:** [Diagram menunjukkan komponen-komponen template: includes, type aliases, macros, fast I/O, dan main function structure]

Perhatikan bahwa `#include <bits/stdc++.h>` adalah non-standard header yang include semua STL headers. Ini sangat convenient untuk competitive programming namun tidak direkomendasikan untuk production code karena memperlambat compilation time dan tidak portable.

### 13.3.6 Online Judge Platforms

Terdapat berbagai platform online judge untuk berlatih competitive programming. Setiap platform memiliki karakteristik dan fokus yang sedikit berbeda.

**Codeforces** adalah salah satu platform paling populer dengan contest regular (biasanya 2-3 kali seminggu). Problem di Codeforces berkisar dari yang sangat mudah hingga sangat sulit, dengan rating system yang menunjukkan difficulty level. Codeforces juga memiliki community yang aktif dengan editorial (solution explanation) yang berkualitas.

**LeetCode** fokus pada interview preparation dengan problem yang sering muncul di technical interview perusahaan tech besar. Platform ini sangat populer untuk persiapan job interview. LeetCode juga menyediakan solution discussion dan complexity analysis.

**AtCoder** adalah platform dari Jepang yang terkenal dengan problem berkualitas tinggi dan editorial yang sangat jelas. AtCoder Beginner Contest (ABC) adalah contest mingguan yang cocok untuk pemula.

**CodeChef** memiliki berbagai jenis contest dari easy hingga hard, dengan Long Challenge yang berlangsung 10 hari, cocok untuk yang baru mulai karena ada banyak waktu untuk learning.

Ketika submit solution ke online judge, pastikan memahami beberapa verdict yang umum:

- **Accepted (AC)**: Solution benar untuk semua test case
- **Wrong Answer (WA)**: Output tidak sesuai expected output
- **Time Limit Exceeded (TLE)**: Program terlalu lama running
- **Memory Limit Exceeded (MLE)**: Program menggunakan terlalu banyak memory
- **Runtime Error (RE)**: Program crash (segmentation fault, array out of bound, dll)
- **Compilation Error (CE)**: Code tidak bisa di-compile

```cpp
// Contoh Problem: Sum of Two Numbers
// Input: dua integer a dan b
// Output: sum dari a dan b

#include <iostream>
using namespace std;

int main() {
    int a, b;
    cin >> a >> b;
    cout << a + b << endl;
    return 0;
}
```

**Gambar 13.14:** [Flowchart proses submission di online judge: write code → submit → compile → run test cases → verdict]

## 13.4 C++ untuk Game Development

### 13.4.1 Mengapa C++ untuk Game Development?

C++ telah menjadi bahasa dominan dalam game development, terutama untuk AAA games dan game engines. Beberapa game engine terkenal seperti Unreal Engine menggunakan C++ sebagai bahasa utama. Bahkan Unity, yang menggunakan C# untuk scripting, memiliki core engine yang ditulis dalam C++.

Ada beberapa alasan mengapa C++ sangat cocok untuk game development. Pertama, performance adalah crucial dalam game development. Game modern perlu merender ribuan objek per frame dengan rate 60 fps atau lebih. C++ memberikan performance yang diperlukan untuk mencapai ini. Kedua, C++ memberikan low-level control terhadap memory management, yang penting untuk optimasi. Ketiga, C++ memiliki ekosistem library game development yang sangat rich.

Namun, C++ untuk game development juga memiliki learning curve yang steep. Selain memahami bahasa C++ itu sendiri, game programmer perlu memahami konsep seperti game loop, rendering pipeline, physics simulation, collision detection, dan banyak lagi. Untuk pembelajaran awal, kita dapat menggunakan library yang lebih simple seperti SDL (Simple DirectMedia Layer) atau SFML (Simple and Fast Multimedia Library).

### 13.4.2 Pengenalan SDL dan SFML

SDL dan SFML adalah multimedia library yang menyediakan abstraksi untuk graphics, audio, input handling, dan fungsi-fungsi lain yang diperlukan untuk game development. SDL adalah library dalam C yang juga dapat digunakan dengan C++, sedangkan SFML adalah library C++ yang lebih modern dan object-oriented.

Untuk menggunakan SDL atau SFML, kita perlu menginstall library dan mengkonfigurasi project untuk link dengan library tersebut. Process ini berbeda tergantung pada IDE dan operating system yang digunakan. Setelah setup, kita dapat mulai membuat game sederhana.

Mari kita lihat struktur dasar program menggunakan SFML. Program game pada dasarnya adalah infinite loop yang terus berjalan hingga user menutup window atau game over. Loop ini disebut "game loop" dan biasanya terdiri dari tiga fase: handle input, update game state, dan render graphics.

```cpp
// Basic Game Loop dengan SFML
#include <SFML/Graphics.hpp>

int main() {
    // Create window
    sf::RenderWindow window(sf::VideoMode(800, 600), "My First Game");
    
    // Game loop
    while (window.isOpen()) {
        // --- 1. Handle Events (Input) ---
        sf::Event event;
        while (window.pollEvent(event)) {
            if (event.type == sf::Event::Closed)
                window.close();
        }
        
        // --- 2. Update Game State ---
        // Update positions, check collisions, etc.
        
        // --- 3. Render ---
        window.clear(sf::Color::Black);  // Clear screen
        
        // Draw game objects here
        
        window.display();  // Display what was drawn
    }
    
    return 0;
}
```

**Gambar 13.15:** [Diagram game loop menunjukkan siklus berulang: Handle Input → Update State → Render → Repeat]

### 13.4.3 Game Loop Concept

Game loop adalah jantung dari setiap game. Konsepnya sederhana: loop terus berjalan, mengupdate state game, dan merender frame baru sebanyak mungkin hingga game berakhir. Namun, implementasinya bisa kompleks untuk memastikan game berjalan smooth dengan frame rate yang consistent.

Ada beberapa jenis game loop. Yang paling sederhana adalah unlimited frame rate loop seperti contoh di atas, di mana game berjalan secepat mungkin. Ini bisa menyebabkan masalah seperti inconsistent frame rate dan high CPU usage. Untuk game yang lebih polished, kita perlu mengimplementasikan frame rate limiting atau time-based movement.

Fixed timestep adalah teknik di mana update logic game berjalan dengan interval yang fixed (misalnya 60 times per second), terlepas dari rendering frame rate. Ini membuat game behavior lebih predictable dan consistent.

```cpp
// Game Loop dengan Fixed Timestep
#include <SFML/Graphics.hpp>
#include <chrono>

int main() {
    sf::RenderWindow window(sf::VideoMode(800, 600), "Fixed Timestep Game");
    
    // Game state variables
    float playerX = 400.0f;
    float playerY = 300.0f;
    float velocityX = 0.0f;
    float velocityY = 0.0f;
    
    // Timing variables
    const double dt = 1.0 / 60.0;  // 60 updates per second
    double accumulator = 0.0;
    
    auto currentTime = std::chrono::high_resolution_clock::now();
    
    while (window.isOpen()) {
        // Calculate time delta
        auto newTime = std::chrono::high_resolution_clock::now();
        double frameTime = std::chrono::duration<double>(newTime - currentTime).count();
        currentTime = newTime;
        
        accumulator += frameTime;
        
        // Handle events
        sf::Event event;
        while (window.pollEvent(event)) {
            if (event.type == sf::Event::Closed)
                window.close();
        }
        
        // Fixed timestep update
        while (accumulator >= dt) {
            // Update game logic here with fixed dt
            playerX += velocityX * dt;
            playerY += velocityY * dt;
            
            accumulator -= dt;
        }
        
        // Render
        window.clear();
        // Draw game
        window.display();
    }
    
    return 0;
}
```

**Gambar 13.16:** [Timeline diagram menunjukkan fixed timestep updates yang independent dari variable rendering frame rate]

### 13.4.4 Sprite dan Basic Graphics

Dalam game development, sprite adalah 2D image atau animation yang merepresentasikan game object seperti player, enemy, atau item. SFML menyediakan class `sf::Sprite` untuk menangani sprite dengan mudah.

Untuk menggunakan sprite, kita perlu load texture dari file image, kemudian create sprite object yang menggunakan texture tersebut. Kita dapat mengatur position, scale, rotation, dan properties lain dari sprite.

```cpp
// Program dengan Sprite Movement
#include <SFML/Graphics.hpp>

int main() {
    sf::RenderWindow window(sf::VideoMode(800, 600), "Sprite Demo");
    
    // Load texture
    sf::Texture playerTexture;
    if (!playerTexture.loadFromFile("player.png")) {
        return -1;  // Error loading texture
    }
    
    // Create sprite
    sf::Sprite playerSprite;
    playerSprite.setTexture(playerTexture);
    playerSprite.setPosition(400, 300);  // Center of screen
    
    // Movement speed
    float speed = 200.0f;  // pixels per second
    
    sf::Clock clock;  // For delta time
    
    while (window.isOpen()) {
        float dt = clock.restart().asSeconds();
        
        // Handle events
        sf::Event event;
        while (window.pollEvent(event)) {
            if (event.type == sf::Event::Closed)
                window.close();
        }
        
        // Handle input and movement
        sf::Vector2f movement(0.0f, 0.0f);
        
        if (sf::Keyboard::isKeyPressed(sf::Keyboard::W))
            movement.y -= speed * dt;
        if (sf::Keyboard::isKeyPressed(sf::Keyboard::S))
            movement.y += speed * dt;
        if (sf::Keyboard::isKeyPressed(sf::Keyboard::A))
            movement.x -= speed * dt;
        if (sf::Keyboard::isKeyPressed(sf::Keyboard::D))
            movement.x += speed * dt;
        
        playerSprite.move(movement);
        
        // Render
        window.clear(sf::Color::White);
        window.draw(playerSprite);
        window.display();
    }
    
    return 0;
}
```

**Gambar 13.17:** [Screenshot game window menunjukkan sprite player yang dapat digerakkan dengan WASD keys]

### 13.4.5 Collision Detection

Collision detection adalah fundamental concept dalam game development. Kita perlu detect ketika objects bersentuhan untuk implement game mechanics seperti player collecting items, bullets hitting enemies, atau player hitting walls.

Untuk collision detection sederhana, kita dapat menggunakan bounding box collision. Setiap object memiliki rectangular bounding box, dan kita check apakah rectangles overlap. SFML menyediakan method `getGlobalBounds()` yang return bounding box dari sprite.

```cpp
// Simple Collision Detection
#include <SFML/Graphics.hpp>
#include <iostream>

int main() {
    sf::RenderWindow window(sf::VideoMode(800, 600), "Collision Demo");
    
    // Player sprite (represented as circle for simplicity)
    sf::CircleShape player(30);
    player.setFillColor(sf::Color::Green);
    player.setPosition(400, 300);
    
    // Coin sprite
    sf::CircleShape coin(20);
    coin.setFillColor(sf::Color::Yellow);
    coin.setPosition(200, 200);
    
    bool coinCollected = false;
    int score = 0;
    
    // Font for text
    sf::Font font;
    if (!font.loadFromFile("arial.ttf")) {
        std::cout << "Error loading font\n";
    }
    
    sf::Text scoreText;
    scoreText.setFont(font);
    scoreText.setCharacterSize(24);
    scoreText.setFillColor(sf::Color::Black);
    scoreText.setPosition(10, 10);
    
    float speed = 200.0f;
    sf::Clock clock;
    
    while (window.isOpen()) {
        float dt = clock.restart().asSeconds();
        
        sf::Event event;
        while (window.pollEvent(event)) {
            if (event.type == sf::Event::Closed)
                window.close();
        }
        
        // Player movement
        sf::Vector2f movement(0.0f, 0.0f);
        if (sf::Keyboard::isKeyPressed(sf::Keyboard::W))
            movement.y -= speed * dt;
        if (sf::Keyboard::isKeyPressed(sf::Keyboard::S))
            movement.y += speed * dt;
        if (sf::Keyboard::isKeyPressed(sf::Keyboard::A))
            movement.x -= speed * dt;
        if (sf::Keyboard::isKeyPressed(sf::Keyboard::D))
            movement.x += speed * dt;
        
        player.move(movement);
        
        // Check collision with coin
        if (!coinCollected && player.getGlobalBounds().intersects(coin.getGlobalBounds())) {
            coinCollected = true;
            score += 10;
            std::cout << "Coin collected! Score: " << score << "\n";
        }
        
        scoreText.setString("Score: " + std::to_string(score));
        
        // Render
        window.clear(sf::Color::White);
        window.draw(player);
        if (!coinCollected) {
            window.draw(coin);
        }
        window.draw(scoreText);
        window.display();
    }
    
    return 0;
}
```

**Gambar 13.18:** [Diagram menunjukkan bounding box collision: dua rectangles overlap = collision detected]

### 13.4.6 Simple Game: Pong

Mari kita aplikasikan semua konsep yang sudah kita pelajari untuk membuat game sederhana: Pong. Pong adalah game klasik di mana dua paddle mencoba memantulkan ball bolak-balik.

```cpp
// Simple Pong Game
#include <SFML/Graphics.hpp>
#include <cmath>

int main() {
    sf::RenderWindow window(sf::VideoMode(800, 600), "Pong");
    
    // Paddles
    sf::RectangleShape leftPaddle(sf::Vector2f(20, 100));
    leftPaddle.setFillColor(sf::Color::White);
    leftPaddle.setPosition(20, 250);
    
    sf::RectangleShape rightPaddle(sf::Vector2f(20, 100));
    rightPaddle.setFillColor(sf::Color::White);
    rightPaddle.setPosition(760, 250);
    
    // Ball
    sf::CircleShape ball(10);
    ball.setFillColor(sf::Color::White);
    ball.setPosition(400, 300);
    
    // Ball velocity
    float ballVelocityX = 300.0f;
    float ballVelocityY = 200.0f;
    
    // Paddle speed
    float paddleSpeed = 400.0f;
    
    sf::Clock clock;
    
    while (window.isOpen()) {
        float dt = clock.restart().asSeconds();
        
        // Handle events
        sf::Event event;
        while (window.pollEvent(event)) {
            if (event.type == sf::Event::Closed)
                window.close();
        }
        
        // Left paddle movement (W and S keys)
        if (sf::Keyboard::isKeyPressed(sf::Keyboard::W) && leftPaddle.getPosition().y > 0)
            leftPaddle.move(0, -paddleSpeed * dt);
        if (sf::Keyboard::isKeyPressed(sf::Keyboard::S) && leftPaddle.getPosition().y < 500)
            leftPaddle.move(0, paddleSpeed * dt);
        
        // Right paddle movement (Up and Down arrows)
        if (sf::Keyboard::isKeyPressed(sf::Keyboard::Up) && rightPaddle.getPosition().y > 0)
            rightPaddle.move(0, -paddleSpeed * dt);
        if (sf::Keyboard::isKeyPressed(sf::Keyboard::Down) && rightPaddle.getPosition().y < 500)
            rightPaddle.move(0, paddleSpeed * dt);
        
        // Ball movement
        ball.move(ballVelocityX * dt, ballVelocityY * dt);
        
        // Ball collision with top and bottom walls
        if (ball.getPosition().y <= 0 || ball.getPosition().y >= 580) {
            ballVelocityY = -ballVelocityY;
        }
        
        // Ball collision with paddles
        if (ball.getGlobalBounds().intersects(leftPaddle.getGlobalBounds()) ||
            ball.getGlobalBounds().intersects(rightPaddle.getGlobalBounds())) {
            ballVelocityX = -ballVelocityX;
        }
        
        // Reset ball if it goes out of bounds
        if (ball.getPosition().x < 0 || ball.getPosition().x > 800) {
            ball.setPosition(400, 300);
            ballVelocityX = -ballVelocityX;
        }
        
        // Render
        window.clear(sf::Color::Black);
        window.draw(leftPaddle);
        window.draw(rightPaddle);
        window.draw(ball);
        window.display();
    }
    
    return 0;
}
```

**Gambar 13.19:** [Screenshot Pong game menunjukkan dua paddles di kiri-kanan dan ball di tengah]

Game Pong ini sederhana namun mendemonstrasikan banyak konsep penting: game loop, input handling, sprite movement, collision detection, dan basic game logic. Dari sini, kita dapat expand game dengan menambahkan score system, AI untuk single player mode, sound effects, dan berbagai enhancement lainnya.

## 13.5 Cross-Platform Development

### 13.5.1 Compiler Differences

Ketika mengembangkan aplikasi C++ yang cross-platform (berjalan di Windows, macOS, dan Linux), kita perlu aware tentang perbedaan antara compiler yang berbeda. Tiga compiler utama yang commonly used adalah GCC (GNU Compiler Collection), Clang, dan MSVC (Microsoft Visual C++).

GCC adalah compiler open-source yang paling widely used, terutama di Linux. GCC memiliki support yang sangat baik untuk C++ standard terbaru dan menghasilkan code yang efficient. Clang adalah compiler yang dikembangkan oleh LLVM project, terkenal dengan error messages yang sangat clear dan helpful. Clang menjadi default compiler di macOS. MSVC adalah compiler dari Microsoft yang terintegrasi dengan Visual Studio, optimized untuk Windows platform.

Meskipun semua compiler ini mengikuti C++ standard, terdapat beberapa perbedaan dalam implementasi dan extension yang mereka support. Beberapa perbedaan penting:

```cpp
// Platform-specific code example
#ifdef _MSC_VER
    // MSVC specific code
    #include <windows.h>
    #define EXPORT __declspec(dllexport)
#elif defined(__GNUC__) || defined(__clang__)
    // GCC or Clang specific code
    #include <unistd.h>
    #define EXPORT __attribute__((visibility("default")))
#endif

// Cross-platform sleep function
void sleep_ms(int milliseconds) {
    #ifdef _WIN32
        Sleep(milliseconds);
    #else
        usleep(milliseconds * 1000);
    #endif
}
```

**Gambar 13.20:** [Tabel perbandingan GCC, Clang, dan MSVC: platform support, C++ standard compliance, optimization capabilities]

### 13.5.2 Preprocessor untuk Platform-Specific Code

Preprocessor directives sangat penting dalam cross-platform development. Kita dapat menggunakan conditional compilation untuk include atau exclude code berdasarkan platform atau compiler yang digunakan.

Beberapa macro yang commonly used untuk detect platform:
- `_WIN32` atau `_WIN64`: Windows (32-bit atau 64-bit)
- `__linux__`: Linux
- `__APPLE__`: macOS atau iOS
- `__unix__`: Unix-like systems (Linux, macOS, BSD)

```cpp
// Cross-platform File Path Handling
#include <iostream>
#include <string>

#ifdef _WIN32
    const char PATH_SEPARATOR = '\\';
    #include <direct.h>
    #define getcwd _getcwd
#else
    const char PATH_SEPARATOR = '/';
    #include <unistd.h>
#endif

std::string getCurrentDirectory() {
    char buffer[FILENAME_MAX];
    getcwd(buffer, FILENAME_MAX);
    return std::string(buffer);
}

std::string joinPath(const std::string& path1, const std::string& path2) {
    return path1 + PATH_SEPARATOR + path2;
}

int main() {
    std::string currentDir = getCurrentDirectory();
    std::cout << "Current directory: " << currentDir << "\n";
    
    std::string filePath = joinPath(currentDir, "data.txt");
    std::cout << "File path: " << filePath << "\n";
    
    return 0;
}
```

**Gambar 13.21:** [Diagram menunjukkan bagaimana preprocessor directives memilih code yang sesuai untuk setiap platform]

### 13.5.3 Build Systems: Makefile Basics

Build system membantu mengautomasi proses compilation, especially untuk project besar dengan banyak source files. Makefile adalah build system tradisional yang widely used di Unix-like systems.

Makefile berisi rules yang menjelaskan bagaimana build executable dari source files. Setiap rule memiliki target, dependencies, dan commands.

```makefile
# Simple Makefile Example
CXX = g++
CXXFLAGS = -std=c++17 -Wall -Wextra
TARGET = myprogram

# Source files
SRCS = main.cpp utils.cpp game.cpp
OBJS = $(SRCS:.cpp=.o)

# Default target
all: $(TARGET)

# Link object files to create executable
$(TARGET): $(OBJS)
	$(CXX) $(CXXFLAGS) -o $(TARGET) $(OBJS)

# Compile source files to object files
%.o: %.cpp
	$(CXX) $(CXXFLAGS) -c $< -o $@

# Clean build artifacts
clean:
	rm -f $(OBJS) $(TARGET)

# Rebuild everything
rebuild: clean all

.PHONY: all clean rebuild
```

**Gambar 13.22:** [Diagram dependency graph showing how source files compile to object files, then link to executable]

Untuk menggunakan Makefile, kita simply run command `make` di terminal. Make tool akan read Makefile, check dependencies, dan compile only files yang berubah. Ini much lebih efficient daripada recompile semua files setiap kali.

### 13.5.4 CMake untuk Cross-Platform Build

CMake adalah modern build system generator yang support multiple platforms dan compilers. Berbeda dengan Makefile yang platform-specific, CMake generate build files yang sesuai dengan platform (Makefile untuk Unix, Visual Studio project untuk Windows, Xcode project untuk macOS).

CMake menggunakan file konfigurasi bernama `CMakeLists.txt` yang describe project structure, dependencies, dan build options. CMake syntax lebih readable dan maintainable dibanding Makefile.

```cmake
# CMakeLists.txt Example
cmake_minimum_required(VERSION 3.10)

# Project name and version
project(MyGame VERSION 1.0)

# Specify C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Add compiler warnings
if(MSVC)
    add_compile_options(/W4)
else()
    add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Source files
set(SOURCES
    src/main.cpp
    src/game.cpp
    src/player.cpp
    src/enemy.cpp
)

# Create executable
add_executable(${PROJECT_NAME} ${SOURCES})

# Link libraries (e.g., SFML)
find_package(SFML 2.5 COMPONENTS graphics window system REQUIRED)
target_link_libraries(${PROJECT_NAME} sfml-graphics sfml-window sfml-system)

# Include directories
target_include_directories(${PROJECT_NAME} PRIVATE include)
```

**Gambar 13.23:** [Flowchart CMake workflow: CMakeLists.txt → CMake → Platform-specific build files → Compiler → Executable]

Untuk build project dengan CMake:

```bash
# Create build directory
mkdir build
cd build

# Generate build files
cmake ..

# Build project
cmake --build .

# Run executable
./MyGame
```

Keuntungan CMake:
- Cross-platform: same CMakeLists.txt works on Windows, macOS, dan Linux
- IDE integration: dapat generate Visual Studio, Xcode, atau Eclipse projects
- Dependency management: mudah integrate external libraries
- Out-of-source build: build files terpisah dari source code

### 13.5.5 Handling Platform-Specific Features

Beberapa features atau libraries hanya available di platform tertentu. Kita perlu handle ini dengan gracefully, baik dengan conditional compilation atau dengan providing alternative implementation.

```cpp
// Cross-platform Console Color Example
#include <iostream>
#include <string>

#ifdef _WIN32
    #include <windows.h>
    
    void setColor(int color) {
        HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
        SetConsoleTextAttribute(hConsole, color);
    }
    
    const int COLOR_RED = 12;
    const int COLOR_GREEN = 10;
    const int COLOR_BLUE = 9;
    const int COLOR_RESET = 7;
#else
    // ANSI color codes for Unix-like systems
    void setColor(const std::string& color) {
        std::cout << color;
    }
    
    const std::string COLOR_RED = "\033[31m";
    const std::string COLOR_GREEN = "\033[32m";
    const std::string COLOR_BLUE = "\033[34m";
    const std::string COLOR_RESET = "\033[0m";
#endif

int main() {
    #ifdef _WIN32
        setColor(COLOR_RED);
        std::cout << "This is red text\n";
        
        setColor(COLOR_GREEN);
        std::cout << "This is green text\n";
        
        setColor(COLOR_BLUE);
        std::cout << "This is blue text\n";
        
        setColor(COLOR_RESET);
    #else
        setColor(COLOR_RED);
        std::cout << "This is red text\n";
        
        setColor(COLOR_GREEN);
        std::cout << "This is green text\n";
        
        setColor(COLOR_BLUE);
        std::cout << "This is blue text\n";
        
        setColor(COLOR_RESET);
    #endif
    
    std::cout << "Back to normal\n";
    
    return 0;
}
```

**Gambar 13.24:** [Screenshot menunjukkan colored output di terminal Windows dan Unix]

### 13.5.6 Best Practices untuk Cross-Platform Development

Beberapa best practices yang perlu diperhatikan dalam cross-platform development:

**Gunakan Standard C++ sebisa mungkin.** Hindari compiler-specific extensions atau non-standard features. Stick to C++ standard (C++11, C++14, C++17, dll) yang widely supported.

**Test di semua target platforms.** Jangan assume code yang berjalan di satu platform akan berjalan identik di platform lain. Selalu test di Windows, macOS, dan Linux jika target multiple platforms.

**Gunakan abstraction untuk platform-specific code.** Create wrapper functions atau classes yang menyembunyikan platform-specific implementation details. Ini membuat code lebih clean dan maintainable.

```cpp
// Platform abstraction example
class FileSystem {
public:
    static std::string getExecutablePath();
    static bool fileExists(const std::string& path);
    static std::vector<std::string> listDirectory(const std::string& path);
    static bool createDirectory(const std::string& path);
    
private:
    // Platform-specific implementations hidden in .cpp file
};
```

**Gunakan portable libraries.** Pilih libraries yang cross-platform seperti Boost, SDL, SFML, atau Qt. Ini mengurangi kebutuhan untuk menulis platform-specific code.

**Consistent naming dan path handling.** Perhatikan case sensitivity (Unix file systems case-sensitive, Windows tidak) dan path separators (Unix menggunakan `/`, Windows menggunakan `\`).

**Documentation.** Document platform-specific behavior atau requirements dengan jelas, termasuk dependencies, build instructions, dan known limitations di setiap platform.

## 13.6 Debugging Tools di Berbagai Platform

### 13.6.1 Debugging di Command Line dengan GDB

GDB (GNU Debugger) adalah debugger powerful untuk C++ yang available di Linux dan macOS. GDB memungkinkan kita untuk set breakpoints, step through code, inspect variables, dan analyze program behavior.

Basic GDB workflow:
1. Compile program dengan debug symbols (`-g` flag)
2. Run program dalam GDB
3. Set breakpoints
4. Run program dan debug

```bash
# Compile dengan debug symbols
g++ -g -o myprogram main.cpp

# Run GDB
gdb ./myprogram

# Di dalam GDB:
# Set breakpoint di function main
(gdb) break main

# Set breakpoint di line 25
(gdb) break main.cpp:25

# Run program
(gdb) run

# Step to next line
(gdb) next

# Step into function
(gdb) step

# Continue execution
(gdb) continue

# Print variable value
(gdb) print variableName

# Print all local variables
(gdb) info locals

# Show backtrace
(gdb) backtrace

# Quit GDB
(gdb) quit
```

**Gambar 13.25:** [Screenshot GDB session menunjukkan breakpoint, variable inspection, dan code stepping]

### 13.6.2 Visual Studio Debugger

Visual Studio menyediakan salah satu debugger paling powerful dengan GUI yang intuitive. Features include breakpoints, watches, call stack visualization, memory inspection, dan banyak lagi.

Key features Visual Studio debugger:
- **Breakpoints**: Click di gutter sebelah line number untuk set breakpoint
- **Watch window**: Monitor specific variables
- **Locals window**: Show semua local variables
- **Call Stack**: See function call hierarchy
- **Immediate window**: Execute code during debugging
- **Memory window**: Inspect raw memory
- **Diagnostic Tools**: CPU usage, memory usage, events timeline

Debugging workflow di Visual Studio:
1. Set breakpoints dengan click di gutter atau press F9
2. Start debugging dengan F5 atau click "Start Debugging"
3. Program akan pause di breakpoint
4. Use F10 (Step Over), F11 (Step Into), Shift+F11 (Step Out) untuk navigate
5. Inspect variables dengan hover mouse atau menggunakan Watch/Locals windows
6. Continue dengan F5 atau Stop dengan Shift+F5

**Gambar 13.26:** [Screenshot Visual Studio debugger showing breakpoint, locals window, call stack, dan code editor]

### 13.6.3 LLDB Debugger untuk macOS

LLDB adalah debugger yang dikembangkan sebagai part of LLVM project dan menjadi default debugger di Xcode untuk macOS development. LLDB memiliki syntax yang mirip dengan GDB namun dengan beberapa improvements.

```bash
# Compile dengan debug symbols
clang++ -g -o myprogram main.cpp

# Run LLDB
lldb ./myprogram

# Di dalam LLDB:
# Set breakpoint
(lldb) breakpoint set --name main
(lldb) b main.cpp:25

# Run program
(lldb) run

# Step over
(lldb) next

# Step into
(lldb) step

# Continue
(lldb) continue

# Print variable
(lldb) print variableName
(lldb) p variableName

# Frame variable (show all local variables)
(lldb) frame variable

# Backtrace
(lldb) bt

# Quit
(lldb) quit
```

**Gambar 13.27:** [Comparison table GDB vs LLDB commands showing equivalent operations]

### 13.6.4 Debugging dengan IDE

Modern IDEs seperti CLion, Code::Blocks, atau VSCode dengan C++ extension menyediakan integrated debugging experience yang powerful. Mereka menggunakan GDB atau LLDB di backend namun provide user-friendly GUI.

CLion debugging features:
- Visual breakpoints dengan conditions
- Inline variable values
- Expression evaluation
- Memory view
- Thread debugging
- Attach to process

VSCode dengan C++ extension:
- IntelliSense untuk autocomplete
- Integrated debugger
- CMake integration
- Multi-platform support

**Gambar 13.28:** [Screenshot CLion debugger interface menunjukkan integrated debugging tools]

### 13.6.5 Debugging Embedded Systems

Debugging embedded systems memiliki challenges unik karena limited resources dan hardware access. Untuk Arduino, debugging bisa dilakukan dengan serial communication dan LED indicators.

```cpp
// Debugging Arduino dengan Serial
void setup() {
  Serial.begin(9600);
  Serial.println("=== Program Started ===");
}

void loop() {
  int sensorValue = analogRead(A0);
  
  // Debug print
  Serial.print("Sensor value: ");
  Serial.println(sensorValue);
  
  if (sensorValue > 500) {
    Serial.println("WARNING: Sensor value high!");
  }
  
  delay(1000);
}
```

Untuk debugging yang lebih advanced pada embedded systems, tools seperti JTAG debugger atau SWD (Serial Wire Debug) dapat digunakan untuk set breakpoints dan step through code pada actual hardware.

**Gambar 13.29:** [Diagram menunjukkan debugging flow pada embedded system menggunakan JTAG debugger]

## 13.7 Ringkasan

Pada bab ini, kita telah menjelajahi berbagai aplikasi C++ di platform dan domain yang berbeda. Kita memulai dengan embedded systems programming menggunakan Arduino dan ESP32, di mana kita belajar tentang digital I/O, analog input, serial communication, dan WiFi connectivity. Embedded programming mengajarkan kita pentingnya efisiensi dan resource management.

Selanjutnya, kita mengeksplorasi competitive programming, di mana C++ menjadi bahasa favorit karena performance-nya. Kita mempelajari teknik fast I/O, penggunaan STL untuk algorithms dan data structures, serta berbagai online judge platforms untuk berlatih. Competitive programming membantu mengasah kemampuan problem solving dan algoritma.

Dalam game development, kita mengenal konsep game loop, sprite handling, collision detection, dan membuat game sederhana menggunakan SFML. Game development mendemonstrasikan aplikasi praktis dari berbagai konsep programming yang telah kita pelajari.

Terakhir, kita membahas cross-platform development, termasuk perbedaan compiler (GCC, Clang, MSVC), penggunaan preprocessor directives, build systems (Makefile dan CMake), dan debugging tools di berbagai platform (GDB, LLDB, Visual Studio Debugger).

Pemahaman tentang berbagai aplikasi C++ ini memberikan perspektif yang lebih luas tentang kemampuan bahasa dan membuka berbagai jalur karir dalam software development, dari embedded systems engineer, competitive programmer, game developer, hingga systems programmer.

## Latihan

### Latihan 1: Arduino LED Control
Buatlah program Arduino yang mengontrol 3 LED dengan pola berikut:
- LED 1 berkedip dengan interval 500ms
- LED 2 berkedip dengan interval 1000ms  
- LED 3 berkedip dengan interval 1500ms
- Semua LED harus berjalan concurrent (bersamaan)

Hint: Gunakan teknik "millis()" instead of "delay()" agar LED dapat berjalan independent.

### Latihan 2: Arduino Button Control
Buatlah program Arduino yang:
- Menggunakan 1 tombol dan 1 LED
- LED toggle (nyala/mati bergantian) setiap kali tombol ditekan
- Implementasikan debouncing untuk mencegah multiple triggering
- Tampilkan state LED melalui serial monitor

### Latihan 3: Temperature Logger
Buatlah program Arduino dengan sensor suhu yang:
- Membaca suhu setiap 5 detik
- Menyimpan 10 reading terakhir dalam array
- Menghitung average temperature
- Menampilkan current temp, average temp, min temp, dan max temp ke serial monitor
- Nyalakan LED warning jika suhu > 30°C

### Latihan 4: Competitive Programming - Array Processing
Diberikan array dengan N integers. Implementasikan program yang:
- Membaca N dan array elements
- Menghitung sum dari semua elements
- Menemukan maximum dan minimum value
- Menghitung berapa kali maximum value muncul
- Output harus efficient (O(n) time complexity)

Input format:
```
5
3 7 2 7 5
```

Output format:
```
Sum: 24
Max: 7
Min: 2
Max count: 2
```

### Latihan 5: Competitive Programming - String Manipulation
Buatlah program yang:
- Membaca sebuah string (max 1000 characters)
- Menghitung frequency setiap character
- Menampilkan characters yang appear lebih dari 1 kali, sorted alphabetically
- Implementasikan dengan efficient menggunakan map atau array

### Latihan 6: Game Development - Moving Square
Menggunakan SFML, buatlah program dengan:
- Square yang dapat digerakkan dengan arrow keys
- Square tidak boleh keluar dari window boundaries
- Tampilkan position (x, y) dari square di window title atau dengan text
- Implementasikan smooth movement dengan delta time

### Latihan 7: Game Development - Catch the Coin
Buatlah simple game dengan SFML:
- Player (circle) yang dapat digerakkan dengan WASD
- Coins (smaller circles) yang spawn di random positions
- Ketika player collides dengan coin, coin disappears dan score increases
- Spawn coin baru setelah coin dikumpulkan
- Tampilkan score di screen
- Game over setelah collect 10 coins, tampilkan "You Win!"

### Latihan 8: Cross-Platform File Reader
Buatlah program cross-platform yang:
- Membaca file text
- Menghitung jumlah lines, words, dan characters
- Implementasikan dengan cara yang work di Windows, macOS, dan Linux
- Handle different line endings (\n, \r\n)
- Error handling jika file tidak ditemukan

### Latihan 9: CMake Project Setup
Setup sebuah C++ project dengan structure berikut:
```
project/
├── CMakeLists.txt
├── src/
│   ├── main.cpp
│   ├── calculator.cpp
│   └── calculator.h
└── build/
```

Buatlah CMakeLists.txt yang:
- Support C++17
- Compile source files menjadi executable "calculator"
- Enable compiler warnings
- Support debug dan release builds

Implementasikan simple calculator dengan functions: add, subtract, multiply, divide.

### Latihan 10: Debugging Challenge
Diberikan program dengan bugs. Gunakan debugger untuk menemukan dan fix bugs:

```cpp
#include <iostream>
#include <vector>
using namespace std;

int findMax(vector<int>& arr) {
    int max = arr[0];
    for(int i = 1; i <= arr.size(); i++) {
        if(arr[i] > max) {
            max = arr[i];
        }
    }
    return max;
}

int main() {
    vector<int> numbers = {5, 2, 8, 1, 9};
    
    int maximum = findMax(numbers);
    cout << "Maximum: " << maximum << endl;
    
    // Calculate average
    int sum = 0;
    for(int i = 0; i < numbers.size(); i++) {
        sum += numbers[i];
    }
    
    int average = sum / numbers.size();
    cout << "Average: " << average << endl;
    
    return 0;
}
```

Gunakan breakpoints dan step-through debugging untuk identify dan fix semua bugs.

## Soal Diskusi

### Diskusi 1: Embedded vs Desktop Programming
Diskusikan perbedaan fundamental antara programming untuk embedded systems (seperti Arduino) dan desktop applications:
- Resource constraints dan implikasinya
- Memory management considerations
- Real-time requirements
- Debugging challenges
- Trade-offs dalam design decisions

Berikan contoh specific scenarios di mana approach berbeda diperlukan.

### Diskusi 2: Language Choice in Competitive Programming
Mengapa C++ menjadi bahasa dominan dalam competitive programming? Bandingkan dengan bahasa lain seperti Python, Java, atau C:
- Performance considerations
- Standard library features
- Ease of implementation
- Common pitfalls
- When might another language be preferable?

### Diskusi 3: Game Engine Selection
Diskusikan considerations dalam memilih game engine atau library untuk project:
- SDL vs SFML vs full engine (Unity, Unreal)
- Learning curve vs capabilities
- Performance requirements
- Platform support
- Community dan documentation
- Project scale dan complexity

Kapan appropriate menggunakan low-level library vs high-level engine?

### Diskusi 4: Cross-Platform Development Challenges
Apa challenges terbesar dalam cross-platform C++ development dan bagaimana mengatasinya:
- Compiler differences dan non-standard features
- Platform-specific APIs
- Build system complexity
- Testing across platforms
- Maintenance overhead
- User expectations per platform

Diskusikan tools dan practices yang membantu mitigate these challenges.

### Diskusi 5: Modern C++ Features
C++11, C++14, C++17, dan C++20 introduce banyak features baru. Diskusikan:
- Apakah new features selalu worth menggunakan?
- Backward compatibility concerns
- Impact pada code readability
- Performance implications
- Adoption di different domains (embedded vs game vs systems)

Berikan examples of features yang valuable vs yang mungkin over-engineering.

### Diskusi 6: IoT Security
Dengan ESP32 dan connectivity, security menjadi concern. Diskusikan:
- Common security vulnerabilities di IoT devices
- Best practices untuk secure communication
- Trade-offs antara security dan performance di embedded
- Importance of updates dan patch management
- Privacy considerations dengan data collection

### Diskusi 7: Debugging Strategies
Bandingkan different debugging approaches:
- Print debugging vs interactive debuggers
- When is each approach more appropriate?
- Debugging in production environments
- Remote debugging challenges
- Automated testing vs manual debugging
- Prevention vs detection strategies

### Diskusi 8: Career Paths dengan C++
Diskusikan berbagai career paths yang menggunakan C++:
- Embedded systems engineer
- Game developer
- Systems programmer
- Financial software (HFT)
- Competitive programmer / Olympiad
- Which domains most appealing dan why?
- Skills overlap dan transferability
- Future trends dan opportunities

## Referensi

1. Monk, S. (2023). *Programming Arduino: Getting Started with Sketches* (3rd ed.). McGraw-Hill Education.

2. Banzi, M., & Shiloh, M. (2022). *Getting Started with Arduino* (4th ed.). Make Community.

3. Halim, S., & Halim, F. (2020). *Competitive Programming 4* (1st ed.). Self-published.

4. Laaksonen, A. (2020). *Guide to Competitive Programming: Learning and Improving Algorithms Through Contests* (2nd ed.). Springer.

5. Dawson, M. (2023). *Beginning C++ Through Game Programming* (5th ed.). Cengage Learning.

6. Gregory, J. (2018). *Game Engine Architecture* (3rd ed.). A K Peters/CRC Press.

7. Martin, R. (2018). *Professional CMake: A Practical Guide* (6th ed.). Self-published.

8. Beningo, J. (2020). *Embedded Software Design: A Practical Approach to Architecture, Processes and Coding Techniques* (1st ed.). Newnes.

9. Stallman, R. M., Pesch, R., Shebs, S., et al. (2023). *Debugging with GDB: The GNU Source-Level Debugger* (10th ed.). Free Software Foundation.

10. ESP32 Documentation. (2024). *ESP32 Programming Guide*. Retrieved from https://docs.espressif.com/

11. SFML Documentation. (2024). *SFML 2.6 Tutorials and Documentation*. Retrieved from https://www.sfml-dev.org/

12. Codeforces. (2024). *Competitive Programming Platform*. Retrieved from https://codeforces.com/

---

*Bahan Ajar Pertemuan 13: C++ di Platform Lain dan Development Tools*  
*Mata Kuliah: Dasar-Dasar Pemrograman*  
*CPMK 1 (Sub-CPMK 1.3), CPMK 4 (Sub-CPMK 4.1)*
