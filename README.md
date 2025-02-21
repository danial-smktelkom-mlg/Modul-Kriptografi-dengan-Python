# Modul Kriptografi dengan Python  
*(Lingkungan: Kali Linux & Visual Studio Code)*

Modul ini bertujuan agar kalian memahami dasar-dasar kriptografi melalui teori dan praktik. Materi yang disampaikan mencakup:

- **Definisi & Terminologi Kriptografi**
- **Double Strength Encryption**
- **Pengenalan Python & Instalasi Paket Kriptografi**
- **Implementasi Teknik Enkripsi:**  
  - Reverse Cipher  
  - Caesar Cipher (beserta metode brute force)  
  - ROT13  
  - ROT18

---

## Bab I: Konsep Dasar Kriptografi

### 1.1 Overview dan Terminologi

**Kriptografi** adalah seni dan ilmu menyembunyikan pesan dengan cara mengubah pesan asli (plain text) menjadi pesan yang tidak bisa dibaca (cipher text), sehingga hanya pihak yang dituju yang dapat mengerti isinya.

**Terminologi penting:**

- **Plain Text:**  
  Pesan asli yang dapat dibaca oleh siapa saja.

- **Cipher Text:**  
  Pesan yang telah diubah melalui proses enkripsi sehingga tidak dapat langsung dipahami.

- **Enkripsi (Encoding):**  
  Proses mengubah plain text menjadi cipher text.

- **Dekripsi (Decoding):**  
  Proses mengembalikan cipher text ke bentuk plain text.

### 1.2 Double Strength Encryption

Double Strength Encryption (atau multiple/cascade encryption) adalah proses mengenkripsi pesan yang sudah dienkripsi sekali lagi—menggunakan algoritma yang sama atau berbeda.  
Contoh tingkatannya:

- **Lapisan Pertama:**  
  Cipher text dihasilkan dari pesan asli menggunakan algoritma hash dan kunci simetris. Selanjutnya, kunci simetris tersebut dienkripsi dengan kunci asimetris untuk memastikan integritas pesan.

- **Lapisan Kedua:**  
  Menambahkan lapisan enkripsi lagi ke cipher text dengan algoritma yang sama atau berbeda, biasanya menggunakan kunci simetris (misalnya, password 32-bit).

- **Lapisan Ketiga:**  
  Mengirimkan kapsul enkripsi melalui koneksi aman (SSL/TLS) untuk menjaga keamanan selama transmisi.

---

## Bab II: Pengenalan Python dan Instalasi

### 2.1 Overview Python

Python adalah bahasa pemrograman open source yang mudah dipahami, bersifat high-level, dan mendukung pemrograman berorientasi objek.

**Fitur utama Python:**

- **Interpreted:**  
  Tidak perlu proses kompilasi sebelum eksekusi.

- **Object-Oriented:**  
  Mendukung konsep kelas, enkapsulasi, dan polimorfisme.

- **Fleksibel:**  
  Dapat digunakan sebagai bahasa scripting maupun pemrograman penuh.

- **Garbage Collection:**  
  Mengelola memori secara otomatis.

- **Integrasi dengan Bahasa Lain:**  
  Bisa diintegrasikan dengan C, C++, dan Java.

Unduh Python dari: [www.python.org/downloads](https://www.python.org/downloads)

### 2.2 Instalasi Python di Kali Linux melalui Terminal

Buka terminal dan ikuti langkah-langkah berikut:

1. **Perbarui Daftar Paket dan Sistem:**
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

2. **Pasang Python 3 (jika belum terinstal):**
   ```bash
   sudo apt install python3 python3-pip -y
   ```

3. **Verifikasi Instalasi Python:**
   ```bash
   python3 --version
   ```
   Pastikan versi yang terinstal sesuai kebutuhan (misalnya, Python 3.8 atau lebih baru).

### 2.3 Instalasi Visual Studio Code di Kali Linux

1. **Unduh Paket VS Code (.deb)**  
   Kunjungi situs resmi [Visual Studio Code](https://code.visualstudio.com/) dan unduh file .deb untuk Linux.

2. **Instal Paket dengan Perintah:**
   ```bash
   sudo dpkg -i code_*.deb
   sudo apt --fix-broken install
   ```

3. **Buka VS Code:**
   ```bash
   code
   ```

### 2.4 Instalasi Paket Kriptografi

Untuk menggunakan paket kriptografi di Python, jalankan perintah berikut di terminal:
```bash
pip3 install cryptography
```

---

## Bab III: Implementasi Teknik Kriptografi

Pada bab ini, kita akan mempraktikkan empat teknik enkripsi sederhana. Setiap teknik dijelaskan dengan algoritma, contoh kode, penjelasan, serta disertai latihan terpandu dan tugas praktik.

### 3.1 Reverse Cipher

#### Konsep dan Algoritma

Reverse Cipher adalah teknik paling sederhana dengan cara membalik urutan karakter pada pesan.  
**Proses Enkripsi & Dekripsi:**  
Karena membalik string adalah proses yang sama, dekripsi dilakukan dengan membalik kembali cipher text.

#### Contoh Kode
```python
def reverse_cipher(pesan):
    cipher_text = ""
    i = len(pesan) - 1
    while i >= 0:
        cipher_text += pesan[i]
        i -= 1
    return cipher_text

# Contoh penggunaan
pesan_asli = "This is program to explain reverse cipher."
cipher = reverse_cipher(pesan_asli)
print("Pesan Asli   :", pesan_asli)
print("Cipher Text  :", cipher)
```

#### Latihan Reverse Cipher (Latihan Terpandu)

1. **Latihan 1:**  
   *Tugas:* Ubah kode agar menerima input dari pengguna.  
   *Petunjuk:*  
   Gantikan nilai `pesan_asli` dengan:
   ```python
   pesan_asli = input("Masukkan pesan untuk enkripsi: ")
   ```

2. **Latihan 2:**  
   *Tugas:* Tambahkan validasi agar hanya input bertipe string yang diterima.  
   *Petunjuk:*  
   Tambahkan pengecekan:
   ```python
   if not isinstance(pesan_asli, str):
       print("Input harus berupa teks!")
       exit()
   ```

3. **Latihan 3:**  
   *Tugas:* Buat versi fungsi yang menggunakan slicing (misalnya, `pesan[::-1]`).  
   *Petunjuk:*  
   Definisikan:
   ```python
   def reverse_cipher_slicing(pesan):
       return pesan[::-1]
   ```

4. **Latihan 4:**  
   *Tugas:* Tambahkan fitur untuk menampilkan indeks dan karakter yang diproses selama pembalikan.  
   *Petunjuk:*  
   Di dalam loop, tambahkan:
   ```python
   print("Index:", i, "->", pesan[i])
   ```

5. **Latihan 5:**  
   *Tugas:* Catat waktu proses enkripsi menggunakan modul `time`.  
   *Petunjuk:*  
   Gunakan:
   ```python
   import time
   mulai = time.time()
   # Proses enkripsi di sini
   cipher = reverse_cipher(pesan_asli)
   selesai = time.time()
   print("Waktu eksekusi: {:.6f} detik".format(selesai - mulai))
   ```

#### Instruksi Tugas Reverse Cipher

- Buat program lengkap dengan pilihan mode enkripsi/dekripsi menggunakan Reverse Cipher.  
- Tambahkan opsi untuk menyimpan hasil enkripsi ke file teks.  
- Buat unit test dengan modul `unittest` untuk menguji fungsi reverse cipher.  
- Implementasikan versi Reverse Cipher dengan pendekatan rekursif.  
- Susun dokumentasi (dalam format Markdown) yang menjelaskan cara kerja dan penggunaan modul Reverse Cipher.

---

### 3.2 Caesar Cipher

#### Konsep dan Algoritma

Caesar Cipher adalah teknik substitusi dengan menggeser setiap huruf pada pesan sebanyak nilai pergeseran tertentu.  
**Proses:**  
Untuk setiap huruf, geser posisinya di alfabet; karakter non-huruf tetap tidak berubah.

#### Contoh Kode
```python
def caesar_encrypt(teks, pergeseran):
    hasil = ""
    for char in teks:
        if char.isalpha():
            basis = 65 if char.isupper() else 97
            hasil += chr((ord(char) - basis + pergeseran) % 26 + basis)
        else:
            hasil += char
    return hasil

def caesar_decrypt(teks, pergeseran):
    return caesar_encrypt(teks, -pergeseran)

# Contoh penggunaan
pesan_asli = "Contoh"
pergeseran = 13
cipher = caesar_encrypt(pesan_asli, pergeseran)
plain = caesar_decrypt(cipher, pergeseran)

print("Pesan Asli    :", pesan_asli)
print("Cipher Text   :", cipher)
print("Dekripsi Hasil:", plain)
```

#### Contoh Hacking Caesar Cipher (Brute Force)
```python
message = 'Ykjpkd'  # Pesan terenkripsi
LETTERS = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'

# Ubah pesan menjadi huruf kapital
message = message.upper()

for key in range(len(LETTERS)):
    translated = ''
    for symbol in message:
        if symbol in LETTERS:
            num = LETTERS.find(symbol) - key  # Geser ke belakang
            if num < 0:
                num += len(LETTERS)  # Lakukan wrap around
            translated += LETTERS[num]
        else:
            translated += symbol
    print(f"Hacking key #{key}: {translated}")
```
*Penjelasan:* Kode di atas mencoba setiap nilai pergeseran (0–25) untuk menemukan kemungkinan dekripsi pesan.

#### Latihan Caesar Cipher (Latihan Terpandu)

1. **Latihan 1:**  
   *Tugas:* Pastikan fungsi hanya mengubah huruf, sedangkan angka dan simbol tetap tidak berubah.  
   *Petunjuk:*  
   Verifikasi pengecekan `if char.isalpha()`.

2. **Latihan 2:**  
   *Tugas:* Buat antarmuka CLI yang menanyakan apakah pengguna ingin enkripsi atau dekripsi.  
   *Petunjuk:*  
   Gunakan:
   ```python
   mode = input("Ketik 'e' untuk enkripsi atau 'd' untuk dekripsi: ")
   ```

3. **Latihan 3:**  
   *Tugas:* Tambahkan validasi bahwa nilai pergeseran tidak boleh melebihi 25.  
   *Petunjuk:*  
   Tambahkan:
   ```python
   if pergeseran > 25:
       print("Nilai pergeseran maksimal adalah 25.")
       exit()
   ```

4. **Latihan 4:**  
   *Tugas:* Buat fungsi yang menampilkan langkah pergeseran tiap karakter (misalnya, nilai ASCII sebelum dan sesudah pergeseran).  
   *Petunjuk:*  
   Di dalam loop, cetak:
   ```python
   print(f"{char} ({ord(char)}) -> {chr((ord(char) - basis + pergeseran) % 26 + basis)}")
   ```

5. **Latihan 5:**  
   *Tugas:* Uji fungsi dengan pesan yang seluruhnya huruf kapital dan pesan yang seluruhnya huruf kecil.  
   *Petunjuk:*  
   Gunakan contoh seperti `"SMK"` dan `"smk"`.

#### Instruksi Tugas Caesar Cipher

- Kembangkan program menu interaktif dengan pilihan mode: enkripsi, dekripsi, dan analisis teks terenkripsi.  
- Buat unit test untuk memastikan fungsi enkripsi dan dekripsi bekerja dengan benar.  
- Implementasikan fitur brute force yang mencoba semua pergeseran (0–25) dan menampilkan hasil dekripsi.  
- Tambahkan opsi untuk menyimpan hasil enkripsi/dekripsi ke file.  
- Susun laporan singkat mengenai kelemahan Caesar Cipher dan cara meningkatkan keamanannya.

---

### 3.3 ROT13

#### Konsep dan Algoritma

ROT13 adalah kasus khusus dari Caesar Cipher dengan pergeseran tetap 13. Karena alfabet terdiri atas 26 huruf, penerapan ROT13 dua kali akan mengembalikan pesan asli.

#### Contoh Kode
```python
import string

def rot13(teks):
    tabel_trans = str.maketrans(
        string.ascii_uppercase + string.ascii_lowercase,
        string.ascii_uppercase[13:] + string.ascii_uppercase[:13] +
        string.ascii_lowercase[13:] + string.ascii_lowercase[:13]
    )
    return teks.translate(tabel_trans)

# Contoh penggunaan
pesan_asli = "Contoh"
cipher = rot13(pesan_asli)
plain = rot13(cipher)  # Penerapan kedua mengembalikan pesan asli

print("Pesan Asli   :", pesan_asli)
print("Cipher Text  :", cipher)
print("Dekripsi Hasil:", plain)
```

#### Latihan ROT13 (Latihan Terpandu)

1. **Latihan 1:**  
   *Tugas:* Pastikan fungsi ROT13 hanya mengubah huruf, sedangkan angka dan simbol tetap tidak berubah.  
   *Petunjuk:*  
   Verifikasi bahwa tabel translasi hanya mencakup huruf.

2. **Latihan 2:**  
   *Tugas:* Buat antarmuka CLI untuk menerima input teks yang akan dienkripsi/dekripsi dengan ROT13.  
   *Petunjuk:*  
   Gunakan:
   ```python
   teks = input("Masukkan teks untuk ROT13: ")
   ```

3. **Latihan 3:**  
   *Tugas:* Tambahkan validasi agar input tidak kosong.  
   *Petunjuk:*  
   Periksa:
   ```python
   if teks.strip() == "":
       print("Input tidak boleh kosong!")
       exit()
   ```

4. **Latihan 4:**  
   *Tugas:* Buat fungsi tambahan untuk menampilkan perbandingan tiap huruf sebelum dan sesudah ROT13 (misalnya, "A -> N").  
   *Petunjuk:*  
   Iterasi tiap karakter dan tampilkan perbandingan jika karakter merupakan huruf.

5. **Latihan 5:**  
   *Tugas:* Uji fungsi ROT13 dengan contoh teks seluruhnya huruf kapital.  
   *Petunjuk:*  
   Contoh: `"SMK"`.

#### Instruksi Tugas ROT13

- Kembangkan antarmuka CLI untuk memilih mode ROT13 (enkripsi atau dekripsi).  
- Buat unit test untuk menguji fungsi ROT13 dengan berbagai jenis input.  
- Integrasikan fungsi ROT13 ke dalam aplikasi sederhana (misalnya, simulasi pengiriman pesan terenkripsi).  
- Tambahkan opsi untuk menyimpan hasil enkripsi/dekripsi ke file.  
- Susun laporan yang menjelaskan kelebihan dan kekurangan ROT13 sebagai metode enkripsi.

---

### 3.4 ROT18

#### Konsep dan Algoritma

ROT18 adalah variasi dari ROT13 yang juga mengubah angka dengan menggunakan ROT5.

**Proses:**

- Untuk huruf (kapital dan kecil), ROT18 melakukan ROT13 (geser 13 posisi).
- Untuk digit (0–9), ROT18 melakukan ROT5 (geser 5 posisi dengan modulus 10).
- Karakter lain (simbol, spasi) tetap tidak berubah.

#### Contoh Kode
```python
import string

def rot18(teks):
    # Tabel translasi untuk huruf dengan ROT13
    rot13_table = str.maketrans(
        string.ascii_uppercase + string.ascii_lowercase,
        string.ascii_uppercase[13:] + string.ascii_uppercase[:13] +
        string.ascii_lowercase[13:] + string.ascii_lowercase[:13]
    )
    # Tabel translasi untuk digit dengan ROT5
    rot5_table = str.maketrans("0123456789", "5678901234")
    
    # Terapkan ROT13 untuk huruf
    hasil = teks.translate(rot13_table)
    # Terapkan ROT5 untuk digit
    hasil = hasil.translate(rot5_table)
    return hasil

# Contoh penggunaan
pesan_asli = "ROT18 Test 12345!"
cipher = rot18(pesan_asli)
plain = rot18(cipher)  # Penerapan kedua mengembalikan pesan asli

print("Pesan Asli    :", pesan_asli)
print("Cipher Text   :", cipher)
print("Dekripsi Hasil:", plain)
```

#### Latihan ROT18 (Latihan Terpandu)

1. **Latihan 1:**  
   *Tugas:* Pastikan fungsi ROT18 hanya memproses huruf dan digit, sedangkan simbol serta spasi tetap tidak berubah.  
   *Petunjuk:*  
   Verifikasi bahwa kedua tabel translasi (huruf dan digit) sudah benar.

2. **Latihan 2:**  
   *Tugas:* Buat antarmuka CLI untuk menerima input teks yang akan dienkripsi/dekripsi dengan ROT18.  
   *Petunjuk:*  
   Gunakan:
   ```python
   teks = input("Masukkan teks untuk ROT18: ")
   ```

3. **Latihan 3:**  
   *Tugas:* Tambahkan validasi agar input tidak kosong.  
   *Petunjuk:*  
   Periksa:
   ```python
   if teks.strip() == "":
       print("Input tidak boleh kosong!")
       exit()
   ```

4. **Latihan 4:**  
   *Tugas:* Buat fungsi tambahan untuk menampilkan perbandingan tiap karakter sebelum dan sesudah ROT18 (misalnya, "A -> N" untuk huruf, "2 -> 7" untuk digit).  
   *Petunjuk:*  
   Iterasi setiap karakter dan tampilkan perbandingan jika karakter merupakan huruf atau digit.

5. **Latihan 5:**  
   *Tugas:* Uji fungsi ROT18 dengan contoh teks yang mengandung huruf kapital, huruf kecil, dan angka.  
   *Petunjuk:*  
   Contoh: `"SMK 2023!"`.

#### Instruksi Tugas ROT18

- Kembangkan antarmuka CLI untuk memilih mode ROT18 (enkripsi atau dekripsi).  
- Buat unit test untuk menguji fungsi ROT18 dengan berbagai jenis input (campuran huruf, angka, dan simbol).  
- Integrasikan fungsi ROT18 ke dalam aplikasi sederhana, misalnya simulasi pengiriman pesan terenkripsi yang juga memproses data numerik.  
- Tambahkan opsi untuk menyimpan hasil enkripsi/dekripsi ke file.  
- Susun laporan yang menjelaskan kelebihan dan kekurangan ROT18 sebagai metode enkripsi, serta perbandingannya dengan ROT13.

---

## Kesimpulan

Modul ini telah menggabungkan semua informasi penting sehingga kalian dapat memahami:

- Dasar-dasar kriptografi, terminologi, dan konsep Double Strength Encryption.
- Pengenalan Python, termasuk instalasi melalui terminal di Kali Linux, tipe data dasar, dan instalasi paket kriptografi.
- Implementasi teknik enkripsi sederhana: Reverse Cipher, Caesar Cipher, ROT13, dan ROT18—lengkap dengan contoh kode, penjelasan, latihan terpandu, serta tugas praktik.
