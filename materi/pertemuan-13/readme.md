# Pertemuan 13: C++ di Platform Lain dan Development Tools

## 📚 Deskripsi

Pertemuan 13 mengeksplorasi penggunaan C++ di berbagai platform dan domain aplikasi. Mahasiswa akan mempelajari bagaimana C++ digunakan dalam embedded systems (Arduino, ESP32), competitive programming, game development, dan cross-platform development. Pertemuan ini juga membahas berbagai debugging tools yang tersedia di platform yang berbeda.

**CPMK Terkait:**
- CPMK 1: Memahami konsep dasar pemrograman (Sub-CPMK 1.3: Penerapan C++ di berbagai platform)
- CPMK 4: Debugging dan error handling (Sub-CPMK 4.1: Debugging techniques)

**Durasi:** 3 x 50 menit

---

## 🎯 Capaian Pembelajaran

Setelah mengikuti pertemuan ini, mahasiswa diharapkan dapat:

1. **Embedded Systems:**
   - Memahami konsep embedded programming dan resource constraints
   - Mengimplementasikan program Arduino untuk digital I/O dan analog input
   - Menggunakan serial communication untuk debugging
   - Memahami WiFi connectivity dengan ESP32

2. **Competitive Programming:**
   - Mengoptimasi I/O untuk performance maksimal
   - Menggunakan STL data structures dan algorithms secara efektif
   - Memahami complexity analysis dan optimization techniques
   - Familiar dengan platform online judge

3. **Game Development:**
   - Memahami konsep game loop dan real-time programming
   - Mengimplementasikan sprite movement dan collision detection
   - Menggunakan multimedia library (SFML) untuk graphics dan input
   - Menerapkan delta time untuk smooth movement

4. **Cross-Platform Development:**
   - Memahami perbedaan compiler (GCC, Clang, MSVC)
   - Menggunakan preprocessor directives untuk platform-specific code
   - Menggunakan build systems (Makefile, CMake)
   - Menerapkan best practices untuk portability

5. **Debugging:**
   - Menggunakan command-line debuggers (GDB, LLDB)
   - Menggunakan GUI debuggers (Visual Studio, IDE)
   - Menerapkan debugging strategies yang efektif
   - Memahami berbagai jenis bugs dan cara mengatasinya

---

## 📖 Materi Pembelajaran

### 1. Bahan Ajar
📄 **[Bahan_Ajar_Pertemuan_13.md](Bahan_Ajar_Pertemuan_13.md)**

Bahan ajar komprehensif yang mencakup:

#### Bab 13.1: Pendahuluan
- Overview berbagai aplikasi C++
- Motivasi dan konteks praktis

#### Bab 13.2: C++ untuk Embedded Systems
- Pengenalan embedded systems dan karakteristiknya
- Arduino programming: setup, digital I/O, analog input
- Serial communication untuk debugging dan data transfer
- ESP32 dan WiFi connectivity
- Contoh projects: LED control, sensor reading, IoT applications

#### Bab 13.3: C++ untuk Competitive Programming
- Overview competitive programming dan platform populer
- Fast I/O techniques untuk performance optimal
- STL data structures: vector, set, map
- Common algorithms: sorting, binary search
- Template code dan best practices
- Online judge platforms dan verdict types

#### Bab 13.4: C++ untuk Game Development
- Mengapa C++ untuk game development
- Pengenalan SDL dan SFML
- Game loop concept dan implementation
- Sprite handling dan basic graphics
- Collision detection techniques
- Complete example: Pong game

#### Bab 13.5: Cross-Platform Development
- Compiler differences: GCC, Clang, MSVC
- Platform-specific code dengan preprocessor
- Build systems: Makefile basics
- CMake untuk cross-platform builds
- Handling platform-specific features
- Best practices untuk portability

#### Bab 13.6: Debugging Tools
- GDB untuk Linux/Unix
- LLDB untuk macOS
- Visual Studio Debugger
- IDE debugging (CLion, VSCode)
- Debugging embedded systems
- Best practices dan common bug categories

#### Bab 13.7: Ringkasan dan Referensi
- 10 Latihan Praktek dengan tingkat kesulitan bervariasi
- 8 Soal Diskusi untuk pemahaman mendalam
- Daftar referensi dan sumber belajar

---

### 2. Slide Presentasi
🎨 **[Slide_Pertemuan_13.md](Slide_Pertemuan_13.md)**



---

### 3. Worksheet Praktikum
✏️ **[Worksheet_Praktikum_Pertemuan_13.md](Worksheet_Praktikum_Pertemuan_13.md)**

Worksheet komprehensif dengan multiple tracks (150 menit):

**Struktur:**

1. **Persiapan (Setup)**
   - Track A: Arduino/Embedded
   - Track B: Competitive Programming
   - Track C: Game Development
   - Track D: Cross-Platform

2. **Warm-up (15 menit)**
   - Environment setup per track
   - Basic functionality testing

3. **Eksplorasi Dasar (30 menit)**
   - Track A: Multiple LED, Button debouncing
   - Track B: Fast I/O, Binary search
   - Track C: Movable character, Collision detection
   - Track D: CMake setup, Platform-specific code

4. **Problem Solving (45 menit)**
   - Problem A: Temperature Monitor System
   - Problem B: Array Manipulation Challenge
   - Problem C: Complete Pong Game
   - Problem D: File Processing Tool

5. **Debugging Challenge (30 menit)**
   - Find and fix multiple bugs
   - Debugger proficiency exercises
   - Call stack analysis

6. **Reflection dan Eksplorasi (30 menit)**
   - Platform comparison
   - Mini project planning

**Kriteria Penilaian:**
- Setup & Basic Exercises: 20%
- Problem Solving: 40%
- Debugging: 20%
- Reflection: 10%
- Code Quality: 10%
- Bonus: Extra features, multiple platforms, documentation

---

## 🛠️ Tools dan Resources

### Software Requirements

**General:**
- C++ Compiler (GCC 7+, Clang 5+, atau MSVC 2019+)
- Text editor atau IDE (VSCode, Visual Studio, CLion, Code::Blocks)

**Track-Specific:**

**Embedded Systems:**
- Arduino IDE (latest version)
- Arduino board atau Tinkercad Circuits (simulator online)
- Optional: Sensors, LEDs, breadboard

**Competitive Programming:**
- Online judge account (Codeforces, LeetCode, HackerRank)
- Fast compiler setup

**Game Development:**
- SFML 2.5+ (download dari sfml-dev.org)
- Graphics assets (optional)

**Cross-Platform:**
- CMake 3.10+
- Multiple OS access atau virtual machines (optional)

### Debugging Tools:
- GDB (Linux/Unix)
- LLDB (macOS)
- Visual Studio Debugger (Windows)
- IDE built-in debuggers

---

## 📚 Referensi Utama

### Books:

1. **Embedded Systems:**
   - Monk, S. (2023). *Programming Arduino: Getting Started with Sketches* (3rd ed.)
   - Banzi, M., & Shiloh, M. (2022). *Getting Started with Arduino* (4th ed.)

2. **Competitive Programming:**
   - Halim, S., & Halim, F. (2020). *Competitive Programming 4*
   - Laaksonen, A. (2020). *Guide to Competitive Programming* (2nd ed.)

3. **Game Development:**
   - Dawson, M. (2023). *Beginning C++ Through Game Programming* (5th ed.)
   - Gregory, J. (2018). *Game Engine Architecture* (3rd ed.)

4. **Cross-Platform:**
   - Martin, R. (2018). *Professional CMake: A Practical Guide*

5. **Debugging:**
   - Stallman, R. M., et al. (2023). *Debugging with GDB* (10th ed.)

### Online Resources:

**Embedded:**
- Arduino Official: https://arduino.cc
- Random Nerd Tutorials: https://randomnerdtutorials.com
- ESP32 Documentation: https://docs.espressif.com

**Competitive Programming:**
- Codeforces: https://codeforces.com
- LeetCode: https://leetcode.com
- CP Algorithms: https://cp-algorithms.com

**Game Development:**
- SFML Tutorials: https://sfml-dev.org/tutorials
- GameDev.net: https://gamedev.net

**General C++:**
- Learn C++: https://learncpp.com
- C++ Reference: https://cppreference.com

---

## 💡 Tips Pembelajaran

### Untuk Mahasiswa:

1. **Pilih Track yang Menarik:**
   - Tidak perlu mencoba semua track sekaligus
   - Focus pada satu domain yang paling menarik minat
   - Explore deeply daripada broadly

2. **Start Small:**
   - Mulai dengan contoh sederhana
   - Build gradually ke project yang lebih kompleks
   - Don't skip fundamentals

3. **Practice Debugging:**
   - Learn to use debugger, bukan hanya print statements
   - Understand error messages
   - Keep track of common mistakes

4. **Join Communities:**
   - Arduino forums untuk embedded
   - Codeforces discussion untuk competitive
   - Game development forums
   - Learn from others' code

5. **Build Projects:**
   - Apply knowledge ke real projects
   - Document your learning journey
   - Share dengan peers

### Untuk Pengajar:

1. **Flexible Approach:**
   - Let students choose their track
   - Provide guidance untuk each domain
   - Encourage exploration

2. **Demo-Driven:**
   - Live coding demonstrations
   - Show debugging process
   - Explain thought process

3. **Provide Resources:**
   - Curated list of tutorials
   - Sample projects
   - Debugging scenarios

4. **Encourage Sharing:**
   - Students present their projects
   - Share debugging experiences
   - Peer learning

---

## 🎓 Pathway Pembelajaran

### Beginner Level:
✅ Setup environment untuk chosen track  
✅ Complete basic exercises  
✅ Understand fundamental concepts  
✅ Use debugger for simple bugs

### Intermediate Level:
✅ Complete problem solving challenges  
✅ Optimize code untuk efficiency  
✅ Handle edge cases properly  
✅ Debug complex issues

### Advanced Level:
✅ Build complete mini project  
✅ Implement advanced features  
✅ Cross-platform compatibility  
✅ Contribute to open source

---

## 🔗 Quick Links

| Materi | Link | Deskripsi |
|--------|------|-----------|
| Bahan Ajar | [📄 Bahan_Ajar_Pertemuan_13.md](Bahan_Ajar_Pertemuan_13.md) | Textbook chapter lengkap |
| Slide | [🎨 Slide_Pertemuan_13.md](Slide_Pertemuan_13.md) | Presentasi Reveal.js |
| Worksheet | [✏️ Worksheet_Praktikum_Pertemuan_13.md](Worksheet_Praktikum_Pertemuan_13.md) | Latihan praktikum |

---

## 📝 Catatan Implementasi

### Timeline Pengajaran (3 x 50 menit):

**Pertemuan 1 (50 menit): Overview & Embedded Systems**
- 10 menit: Introduction dan motivasi
- 20 menit: Embedded systems dan Arduino
- 15 menit: Hands-on demo
- 5 menit: Q&A dan assignment

**Pertemuan 2 (50 menit): Competitive Programming & Game Dev**
- 10 menit: Review dan competitive programming intro
- 15 menit: Fast I/O dan algorithms
- 20 menit: Game development basics
- 5 menit: Discussion

**Pertemuan 3 (50 menit): Cross-Platform & Debugging**
- 15 menit: Cross-platform development
- 20 menit: Debugging tools hands-on
- 10 menit: Best practices
- 5 menit: Wrap-up dan next steps

**Alternatif:** Bisa juga focus pada satu atau dua track saja untuk depth.

### Assessment Options:

1. **Track-based:** Students pilih satu track dan complete all exercises
2. **Breadth:** Complete basic dari multiple tracks
3. **Project-based:** Build mini project dari chosen domain
4. **Portfolio:** Combine multiple small projects

---

## 🌟 Success Stories

Contoh project ideas untuk inspirasi:

**Embedded:**
- 🏠 Home automation system
- 🌡️ Weather station dengan data logging
- 🤖 Line-following robot
- 🔔 Smart doorbell dengan notifications

**Competitive:**
- 🏆 Reach certain rating di Codeforces
- 📊 Solve 100 problems milestone
- 🎯 Participate dalam online contest
- 📚 Create solution tutorial blog

**Game Development:**
- 🎮 Complete arcade game (Snake, Breakout)
- 🎯 Educational game untuk kids
- 🏃 Platformer game
- 🎲 Puzzle game

**Cross-Platform:**
- 🛠️ Command-line utility
- 📝 Text editor
- 📊 Data visualization tool
- 🔧 Build automation tool

---

## 📮 Feedback dan Kontribusi

Materi ini adalah living document. Feedback dan suggestions welcome untuk improvement:

- Bug reports dalam code examples
- Additional resources
- Student project showcases
- Teaching experiences

---

## 📄 Lisensi

Materi pembelajaran ini dibuat untuk keperluan pendidikan. Silakan digunakan dan dimodifikasi sesuai kebutuhan dengan tetap memberikan attribution.

---

**Selamat belajar dan selamat mengeksplorasi dunia C++ yang luas!** 🚀

*Last updated: 2024*  
*Mata Kuliah: Dasar-Dasar Pemrograman*  
*CPMK 1, CPMK 4*
