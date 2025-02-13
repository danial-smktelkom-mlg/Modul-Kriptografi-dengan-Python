
<h1 id="modul-kriptografi-dengan-python">Modul Kriptografi dengan Python</h1>
<p><em>(Lingkungan: Kali Linux &amp; Visual Studio Code)</em></p>
<p>Modul ini bertujuan agar kalian memahami dasar-dasar kriptografi melalui teori dan praktik. Materi yang disampaikan mencakup:</p>
<ul>
<li><strong>Definisi &amp; Terminologi Kriptografi</strong></li>
<li><strong>Double Strength Encryption</strong></li>
<li><strong>Pengenalan Python &amp; Instalasi Paket Kriptografi</strong></li>
<li><strong>Implementasi Teknik Enkripsi:</strong> Reverse Cipher, Caesar Cipher (beserta metode brute force), ROT13, dan ROT18.</li>
</ul>
<hr>
<h2 id="bab-i-konsep-dasar-kriptografi">Bab I: Konsep Dasar Kriptografi</h2>
<h3 id="overview-dan-terminologi">1.1 Overview dan Terminologi</h3>
<p><strong>Kriptografi</strong> adalah seni dan ilmu menyembunyikan pesan dengan cara mengubah pesan asli (plain text) menjadi pesan yang tidak bisa dibaca (cipher text) agar hanya pihak yang dituju yang dapat mengerti isinya.<br>
Terminologi penting:</p>
<ul>
<li><strong>Plain Text:</strong> Pesan asli yang dapat dibaca oleh siapa saja.</li>
<li><strong>Cipher Text:</strong> Pesan yang telah diubah melalui proses enkripsi sehingga tidak dapat langsung dipahami.</li>
<li><strong>Enkripsi (Encoding):</strong> Proses mengubah plain text menjadi cipher text.</li>
<li><strong>Dekripsi (Decoding):</strong> Proses mengembalikan cipher text ke bentuk plain text.</li>
</ul>
<h3 id="double-strength-encryption">1.2 Double Strength Encryption</h3>
<p>Double Strength Encryption (atau multiple/cascade encryption) adalah proses mengenkripsi pesan yang sudah dienkripsi sekali lagi—menggunakan algoritma yang sama atau berbeda.<br>
<strong>Contoh tingkatannya:</strong></p>
<ul>
<li>
<p><strong>Lapisan Pertama:</strong><br>
Cipher text dihasilkan dari pesan asli menggunakan algoritma hash dan kunci simetris. Selanjutnya, kunci simetris tersebut dienkripsi dengan kunci asimetris untuk memastikan integritas pesan.</p>
</li>
<li>
<p><strong>Lapisan Kedua:</strong><br>
Menambahkan lapisan enkripsi lagi ke cipher text dengan algoritma yang sama atau berbeda, biasanya menggunakan kunci simetris (misalnya, password 32-bit).</p>
</li>
<li>
<p><strong>Lapisan Ketiga:</strong><br>
Mengirimkan kapsul enkripsi melalui koneksi aman (SSL/TLS) untuk menjaga keamanan selama transmisi.</p>
</li>
</ul>
<hr>
<h2 id="bab-ii-pengenalan-python-dan-instalasi">Bab II: Pengenalan Python dan Instalasi</h2>
<h3 id="overview-python">2.1 Overview Python</h3>
<p>Python adalah bahasa pemrograman open source yang mudah dipahami, bersifat high-level, dan mendukung pemrograman berorientasi objek.<br>
<strong>Fitur utama Python:</strong></p>
<ul>
<li><strong>Interpreted:</strong> Tidak perlu proses kompilasi sebelum eksekusi.</li>
<li><strong>Object-Oriented:</strong> Mendukung konsep kelas, enkapsulasi, dan polimorfisme.</li>
<li><strong>Fleksibel:</strong> Dapat digunakan sebagai bahasa scripting maupun pemrograman penuh.</li>
<li><strong>Garbage Collection:</strong> Mengelola memori secara otomatis.</li>
<li><strong>Integrasi dengan Bahasa Lain:</strong> Bisa diintegrasikan dengan C, C++, dan Java.</li>
</ul>
<p><em>Unduh Python dari:</em> <a href="https://www.python.org/downloads">www.python.org/downloads</a></p>
<h3 id="instalasi-python-di-kali-linux-melalui-terminal">2.2 Instalasi Python di Kali Linux melalui Terminal</h3>
<p>Untuk menginstal Python di Kali Linux, buka terminal dan ikuti langkah berikut:</p>
<ol>
<li>
<p><strong>Perbarui Daftar Paket dan Sistem:</strong></p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> apt update <span class="token operator">&amp;&amp;</span> <span class="token function">sudo</span> apt upgrade -y
</code></pre>
</li>
<li>
<p><strong>Pasang Python 3 (jika belum terinstal):</strong></p>
<pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> apt <span class="token function">install</span> python3 python3-pip -y
</code></pre>
</li>
<li>
<p><strong>Verifikasi Instalasi Python:</strong></p>
<pre class=" language-bash"><code class="prism  language-bash">python3 --version
</code></pre>
<p>Pastikan versi yang terinstal sesuai dengan kebutuhan (misalnya, Python 3.8 atau yang lebih baru).</p>
</li>
</ol>
<h3 id="instalasi-visual-studio-code-di-kali-linux">2.3 Instalasi Visual Studio Code di Kali Linux</h3>
<ol>
<li><strong>Unduh Paket VS Code (.deb) dari <a href="https://code.visualstudio.com/">situs resmi VS Code</a>.</strong></li>
<li><strong>Install Paket dengan Perintah:</strong><pre class=" language-bash"><code class="prism  language-bash"><span class="token function">sudo</span> dpkg -i code_*.deb
<span class="token function">sudo</span> apt --fix-broken <span class="token function">install</span>
</code></pre>
</li>
<li><strong>Buka VS Code dengan Perintah:</strong><pre class=" language-bash"><code class="prism  language-bash">code
</code></pre>
</li>
</ol>
<h3 id="instalasi-paket-kriptografi">2.4 Instalasi Paket Kriptografi</h3>
<p>Untuk menggunakan paket kriptografi di Python, jalankan perintah berikut di terminal:</p>
<pre class=" language-bash"><code class="prism  language-bash">pip3 <span class="token function">install</span> cryptography
</code></pre>
<hr>
<h2 id="bab-iii-implementasi-teknik-kriptografi">Bab III: Implementasi Teknik Kriptografi</h2>
<p>Pada bab ini, kita akan mempraktikkan empat teknik enkripsi sederhana. Setiap teknik dijelaskan dengan algoritma, contoh kode, penjelasan, serta disertai latihan terpandu dan tugas praktik.</p>
<hr>
<h3 id="reverse-cipher">3.1 Reverse Cipher</h3>
<h4 id="konsep-dan-algoritma">Konsep dan Algoritma</h4>
<p>Reverse Cipher adalah teknik paling sederhana dengan cara membalik urutan karakter pesan.</p>
<ul>
<li><strong>Proses Enkripsi &amp; Dekripsi:</strong><br>
Karena membalik string adalah proses yang sama, dekripsi dilakukan dengan membalik kembali cipher text.</li>
</ul>
<h4 id="contoh-kode">Contoh Kode</h4>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">def</span> <span class="token function">reverse_cipher</span><span class="token punctuation">(</span>pesan<span class="token punctuation">)</span><span class="token punctuation">:</span>
    cipher_text <span class="token operator">=</span> <span class="token string">""</span>
    i <span class="token operator">=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>pesan<span class="token punctuation">)</span> <span class="token operator">-</span> <span class="token number">1</span>
    <span class="token keyword">while</span> i <span class="token operator">&gt;=</span> <span class="token number">0</span><span class="token punctuation">:</span>
        cipher_text <span class="token operator">+=</span> pesan<span class="token punctuation">[</span>i<span class="token punctuation">]</span>
        i <span class="token operator">-=</span> <span class="token number">1</span>
    <span class="token keyword">return</span> cipher_text

<span class="token comment"># Contoh penggunaan</span>
pesan_asli <span class="token operator">=</span> <span class="token string">"This is program to explain reverse cipher."</span>
cipher <span class="token operator">=</span> reverse_cipher<span class="token punctuation">(</span>pesan_asli<span class="token punctuation">)</span>
<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Pesan Asli   :"</span><span class="token punctuation">,</span> pesan_asli<span class="token punctuation">)</span>
<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Cipher Text  :"</span><span class="token punctuation">,</span> cipher<span class="token punctuation">)</span>
</code></pre>
<h4 id="latihan-reverse-cipher-latihan-terpandu">Latihan Reverse Cipher (Latihan Terpandu)</h4>
<ol>
<li>
<p><strong>Latihan 1:</strong><br>
<em>Tugas:</em> Ubah kode agar menerima input dari pengguna.<br>
<em>Petunjuk:</em><br>
Gantikan nilai <code>pesan_asli</code> dengan:</p>
<pre class=" language-python"><code class="prism  language-python">pesan_asli <span class="token operator">=</span> <span class="token builtin">input</span><span class="token punctuation">(</span><span class="token string">"Masukkan pesan untuk enkripsi: "</span><span class="token punctuation">)</span>
</code></pre>
</li>
<li>
<p><strong>Latihan 2:</strong><br>
<em>Tugas:</em> Tambahkan validasi agar hanya input string yang diterima.<br>
<em>Petunjuk:</em><br>
Tambahkan pengecekan:</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">if</span> <span class="token operator">not</span> <span class="token builtin">isinstance</span><span class="token punctuation">(</span>pesan_asli<span class="token punctuation">,</span> <span class="token builtin">str</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
    <span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Input harus berupa teks!"</span><span class="token punctuation">)</span>
    exit<span class="token punctuation">(</span><span class="token punctuation">)</span>
</code></pre>
</li>
<li>
<p><strong>Latihan 3:</strong><br>
<em>Tugas:</em> Buat versi fungsi yang menggunakan slicing (<code>pesan[::-1]</code>).<br>
<em>Petunjuk:</em><br>
Definisikan:</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">def</span> <span class="token function">reverse_cipher_slicing</span><span class="token punctuation">(</span>pesan<span class="token punctuation">)</span><span class="token punctuation">:</span>
    <span class="token keyword">return</span> pesan<span class="token punctuation">[</span><span class="token punctuation">:</span><span class="token punctuation">:</span><span class="token operator">-</span><span class="token number">1</span><span class="token punctuation">]</span>
</code></pre>
</li>
<li>
<p><strong>Latihan 4:</strong><br>
<em>Tugas:</em> Tambahkan fitur untuk menampilkan indeks dan karakter yang diproses selama pembalikan.<br>
<em>Petunjuk:</em><br>
Di dalam loop, tambahkan:</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Index:"</span><span class="token punctuation">,</span> i<span class="token punctuation">,</span> <span class="token string">"-&gt;"</span><span class="token punctuation">,</span> pesan<span class="token punctuation">[</span>i<span class="token punctuation">]</span><span class="token punctuation">)</span>
</code></pre>
</li>
<li>
<p><strong>Latihan 5:</strong><br>
<em>Tugas:</em> Catat waktu proses enkripsi menggunakan modul <code>time</code>.<br>
<em>Petunjuk:</em><br>
Gunakan:</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">import</span> time
mulai <span class="token operator">=</span> time<span class="token punctuation">.</span>time<span class="token punctuation">(</span><span class="token punctuation">)</span>
<span class="token comment"># proses enkripsi</span>
selesai <span class="token operator">=</span> time<span class="token punctuation">.</span>time<span class="token punctuation">(</span><span class="token punctuation">)</span>
<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Waktu eksekusi:"</span><span class="token punctuation">,</span> selesai <span class="token operator">-</span> mulai<span class="token punctuation">,</span> <span class="token string">"detik"</span><span class="token punctuation">)</span>
</code></pre>
</li>
</ol>
<h4 id="instruksi-tugas-reverse-cipher">Instruksi Tugas Reverse Cipher</h4>
<ol>
<li>Buat program lengkap dengan pilihan mode enkripsi/dekripsi menggunakan Reverse Cipher.</li>
<li>Tambahkan opsi untuk menyimpan hasil enkripsi ke file teks.</li>
<li>Buat unit test dengan modul <code>unittest</code> untuk menguji fungsi reverse cipher.</li>
<li>Implementasikan versi Reverse Cipher dengan pendekatan rekursif.</li>
<li>Susun dokumentasi (dalam format Markdown) yang menjelaskan cara kerja dan penggunaan modul Reverse Cipher.</li>
</ol>
<hr>
<h3 id="caesar-cipher">3.2 Caesar Cipher</h3>
<h4 id="konsep-dan-algoritma-1">Konsep dan Algoritma</h4>
<p>Caesar Cipher adalah teknik substitusi dengan menggeser setiap huruf pada pesan sebanyak nilai pergeseran tertentu.</p>
<ul>
<li><strong>Proses:</strong><br>
Untuk setiap huruf, geser posisinya di alfabet. Karakter non-huruf tidak berubah.</li>
</ul>
<h4 id="contoh-kode-1">Contoh Kode</h4>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">def</span> <span class="token function">caesar_encrypt</span><span class="token punctuation">(</span>teks<span class="token punctuation">,</span> pergeseran<span class="token punctuation">)</span><span class="token punctuation">:</span>
    hasil <span class="token operator">=</span> <span class="token string">""</span>
    <span class="token keyword">for</span> char <span class="token keyword">in</span> teks<span class="token punctuation">:</span>
        <span class="token keyword">if</span> char<span class="token punctuation">.</span>isalpha<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
            basis <span class="token operator">=</span> <span class="token number">65</span> <span class="token keyword">if</span> char<span class="token punctuation">.</span>isupper<span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token keyword">else</span> <span class="token number">97</span>
            hasil <span class="token operator">+=</span> <span class="token builtin">chr</span><span class="token punctuation">(</span><span class="token punctuation">(</span><span class="token builtin">ord</span><span class="token punctuation">(</span>char<span class="token punctuation">)</span> <span class="token operator">-</span> basis <span class="token operator">+</span> pergeseran<span class="token punctuation">)</span> <span class="token operator">%</span> <span class="token number">26</span> <span class="token operator">+</span> basis<span class="token punctuation">)</span>
        <span class="token keyword">else</span><span class="token punctuation">:</span>
            hasil <span class="token operator">+=</span> char
    <span class="token keyword">return</span> hasil

<span class="token keyword">def</span> <span class="token function">caesar_decrypt</span><span class="token punctuation">(</span>teks<span class="token punctuation">,</span> pergeseran<span class="token punctuation">)</span><span class="token punctuation">:</span>
    <span class="token keyword">return</span> caesar_encrypt<span class="token punctuation">(</span>teks<span class="token punctuation">,</span> <span class="token operator">-</span>pergeseran<span class="token punctuation">)</span>

<span class="token comment"># Contoh penggunaan</span>
pesan_asli <span class="token operator">=</span> <span class="token string">"CEASER CIPHER DEMO"</span>
pergeseran <span class="token operator">=</span> <span class="token number">4</span>
cipher <span class="token operator">=</span> caesar_encrypt<span class="token punctuation">(</span>pesan_asli<span class="token punctuation">,</span> pergeseran<span class="token punctuation">)</span>
plain <span class="token operator">=</span> caesar_decrypt<span class="token punctuation">(</span>cipher<span class="token punctuation">,</span> pergeseran<span class="token punctuation">)</span>

<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Pesan Asli    :"</span><span class="token punctuation">,</span> pesan_asli<span class="token punctuation">)</span>
<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Cipher Text   :"</span><span class="token punctuation">,</span> cipher<span class="token punctuation">)</span>
<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Dekripsi Hasil:"</span><span class="token punctuation">,</span> plain<span class="token punctuation">)</span>
</code></pre>
<h4 id="contoh-hacking-caesar-cipher-brute-force">Contoh Hacking Caesar Cipher (Brute Force)</h4>
<pre class=" language-python"><code class="prism  language-python">message <span class="token operator">=</span> <span class="token string">'GIEWIVrGMTLIVrHIQS'</span>  <span class="token comment"># pesan terenkripsi</span>
LETTERS <span class="token operator">=</span> <span class="token string">'ABCDEFGHIJKLMNOPQRSTUVWXYZ'</span>

<span class="token keyword">for</span> key <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span><span class="token builtin">len</span><span class="token punctuation">(</span>LETTERS<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">:</span>
    translated <span class="token operator">=</span> <span class="token string">''</span>
    <span class="token keyword">for</span> symbol <span class="token keyword">in</span> message<span class="token punctuation">:</span>
        <span class="token keyword">if</span> symbol <span class="token keyword">in</span> LETTERS<span class="token punctuation">:</span>
            num <span class="token operator">=</span> LETTERS<span class="token punctuation">.</span>find<span class="token punctuation">(</span>symbol<span class="token punctuation">)</span>
            num <span class="token operator">=</span> num <span class="token operator">-</span> key
            <span class="token keyword">if</span> num <span class="token operator">&lt;</span> <span class="token number">0</span><span class="token punctuation">:</span>
                num <span class="token operator">+=</span> <span class="token builtin">len</span><span class="token punctuation">(</span>LETTERS<span class="token punctuation">)</span>
            translated <span class="token operator">+=</span> LETTERS<span class="token punctuation">[</span>num<span class="token punctuation">]</span>
        <span class="token keyword">else</span><span class="token punctuation">:</span>
            translated <span class="token operator">+=</span> symbol
    <span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Hacking key #%s: %s"</span> <span class="token operator">%</span> <span class="token punctuation">(</span>key<span class="token punctuation">,</span> translated<span class="token punctuation">)</span><span class="token punctuation">)</span>
</code></pre>
<p><em>Penjelasan:</em> Kode di atas mencoba setiap nilai pergeseran (0–25) untuk menemukan kemungkinan dekripsi pesan.</p>
<h4 id="latihan-caesar-cipher-latihan-terpandu">Latihan Caesar Cipher (Latihan Terpandu)</h4>
<ol>
<li>
<p><strong>Latihan 1:</strong><br>
<em>Tugas:</em> Pastikan fungsi hanya mengubah huruf, sedangkan angka dan simbol tetap tidak berubah.<br>
<em>Petunjuk:</em><br>
Verifikasi bahwa pengecekan <code>if char.isalpha()</code> sudah tepat.</p>
</li>
<li>
<p><strong>Latihan 2:</strong><br>
<em>Tugas:</em> Buat antarmuka CLI yang menanyakan apakah pengguna ingin enkripsi atau dekripsi.<br>
<em>Petunjuk:</em><br>
Gunakan:</p>
<pre class=" language-python"><code class="prism  language-python">mode <span class="token operator">=</span> <span class="token builtin">input</span><span class="token punctuation">(</span><span class="token string">"Ketik 'e' untuk enkripsi atau 'd' untuk dekripsi: "</span><span class="token punctuation">)</span>
</code></pre>
</li>
<li>
<p><strong>Latihan 3:</strong><br>
<em>Tugas:</em> Tambahkan validasi bahwa nilai pergeseran tidak boleh melebihi 25.<br>
<em>Petunjuk:</em><br>
Tambahkan:</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">if</span> pergeseran <span class="token operator">&gt;</span> <span class="token number">25</span><span class="token punctuation">:</span>
    <span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Nilai pergeseran maksimal adalah 25."</span><span class="token punctuation">)</span>
    exit<span class="token punctuation">(</span><span class="token punctuation">)</span>
</code></pre>
</li>
<li>
<p><strong>Latihan 4:</strong><br>
<em>Tugas:</em> Buat fungsi yang menampilkan langkah pergeseran tiap karakter (misalnya, nilai ASCII sebelum dan sesudah pergeseran).<br>
<em>Petunjuk:</em><br>
Di dalam loop, cetak:</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">print</span><span class="token punctuation">(</span>f<span class="token string">"{char} ({ord(char)}) -&gt; {chr((ord(char) - basis + pergeseran) % 26 + basis)}"</span><span class="token punctuation">)</span>
</code></pre>
</li>
<li>
<p><strong>Latihan 5:</strong><br>
<em>Tugas:</em> Uji fungsi dengan pesan yang seluruhnya huruf kapital dan pesan yang seluruhnya huruf kecil.<br>
<em>Petunjuk:</em><br>
Gunakan contoh seperti <code>"SMK"</code> dan <code>"smk"</code>.</p>
</li>
</ol>
<h4 id="instruksi-tugas-caesar-cipher">Instruksi Tugas Caesar Cipher</h4>
<ol>
<li>Kembangkan program menu interaktif dengan pilihan mode: enkripsi, dekripsi, dan analisis teks terenkripsi.</li>
<li>Buat unit test untuk memastikan fungsi enkripsi dan dekripsi bekerja dengan benar.</li>
<li>Implementasikan fitur brute force yang mencoba semua pergeseran (0–25) dan menampilkan hasil dekripsi.</li>
<li>Tambahkan opsi untuk menyimpan hasil enkripsi/dekripsi ke file.</li>
<li>Susun laporan singkat mengenai kelemahan Caesar Cipher dan cara meningkatkan keamanannya.</li>
</ol>
<hr>
<h3 id="rot13">3.3 ROT13</h3>
<h4 id="konsep-dan-algoritma-2">Konsep dan Algoritma</h4>
<p>ROT13 adalah kasus khusus dari Caesar Cipher dengan pergeseran tetap 13. Karena alfabet terdiri atas 26 huruf, penerapan ROT13 dua kali akan mengembalikan pesan asli.</p>
<h4 id="contoh-kode-2">Contoh Kode</h4>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">import</span> string

<span class="token keyword">def</span> <span class="token function">rot13</span><span class="token punctuation">(</span>teks<span class="token punctuation">)</span><span class="token punctuation">:</span>
    tabel_trans <span class="token operator">=</span> <span class="token builtin">str</span><span class="token punctuation">.</span>maketrans<span class="token punctuation">(</span>
        string<span class="token punctuation">.</span>ascii_uppercase <span class="token operator">+</span> string<span class="token punctuation">.</span>ascii_lowercase<span class="token punctuation">,</span>
        string<span class="token punctuation">.</span>ascii_uppercase<span class="token punctuation">[</span><span class="token number">13</span><span class="token punctuation">:</span><span class="token punctuation">]</span> <span class="token operator">+</span> string<span class="token punctuation">.</span>ascii_uppercase<span class="token punctuation">[</span><span class="token punctuation">:</span><span class="token number">13</span><span class="token punctuation">]</span> <span class="token operator">+</span>
        string<span class="token punctuation">.</span>ascii_lowercase<span class="token punctuation">[</span><span class="token number">13</span><span class="token punctuation">:</span><span class="token punctuation">]</span> <span class="token operator">+</span> string<span class="token punctuation">.</span>ascii_lowercase<span class="token punctuation">[</span><span class="token punctuation">:</span><span class="token number">13</span><span class="token punctuation">]</span>
    <span class="token punctuation">)</span>
    <span class="token keyword">return</span> teks<span class="token punctuation">.</span>translate<span class="token punctuation">(</span>tabel_trans<span class="token punctuation">)</span>

<span class="token comment"># Contoh penggunaan</span>
pesan_asli <span class="token operator">=</span> <span class="token string">"ROT13 Algorithm"</span>
cipher <span class="token operator">=</span> rot13<span class="token punctuation">(</span>pesan_asli<span class="token punctuation">)</span>
plain <span class="token operator">=</span> rot13<span class="token punctuation">(</span>cipher<span class="token punctuation">)</span>  <span class="token comment"># Penerapan kedua mengembalikan pesan asli</span>

<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Pesan Asli   :"</span><span class="token punctuation">,</span> pesan_asli<span class="token punctuation">)</span>
<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Cipher Text  :"</span><span class="token punctuation">,</span> cipher<span class="token punctuation">)</span>
<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Dekripsi Hasil:"</span><span class="token punctuation">,</span> plain<span class="token punctuation">)</span>
</code></pre>
<h4 id="latihan-rot13-latihan-terpandu">Latihan ROT13 (Latihan Terpandu)</h4>
<ol>
<li>
<p><strong>Latihan 1:</strong><br>
<em>Tugas:</em> Pastikan fungsi ROT13 hanya mengubah huruf, sedangkan angka dan simbol tidak berubah.<br>
<em>Petunjuk:</em><br>
Verifikasi bahwa tabel translasi hanya mencakup huruf.</p>
</li>
<li>
<p><strong>Latihan 2:</strong><br>
<em>Tugas:</em> Buat antarmuka CLI untuk menerima input teks yang akan dienkripsi/dekripsi dengan ROT13.<br>
<em>Petunjuk:</em><br>
Gunakan:</p>
<pre class=" language-python"><code class="prism  language-python">teks <span class="token operator">=</span> <span class="token builtin">input</span><span class="token punctuation">(</span><span class="token string">"Masukkan teks untuk ROT13: "</span><span class="token punctuation">)</span>
</code></pre>
</li>
<li>
<p><strong>Latihan 3:</strong><br>
<em>Tugas:</em> Tambahkan validasi agar input tidak kosong.<br>
<em>Petunjuk:</em><br>
Periksa:</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">if</span> teks<span class="token punctuation">.</span>strip<span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">==</span> <span class="token string">""</span><span class="token punctuation">:</span>
    <span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Input tidak boleh kosong!"</span><span class="token punctuation">)</span>
    exit<span class="token punctuation">(</span><span class="token punctuation">)</span>
</code></pre>
</li>
<li>
<p><strong>Latihan 4:</strong><br>
<em>Tugas:</em> Buat fungsi tambahan untuk menampilkan perbandingan tiap huruf sebelum dan sesudah ROT13 (misalnya, “A -&gt; N”).<br>
<em>Petunjuk:</em><br>
Iterasi tiap karakter dan tampilkan perbandingan jika karakter merupakan huruf.</p>
</li>
<li>
<p><strong>Latihan 5:</strong><br>
<em>Tugas:</em> Uji fungsi ROT13 dengan contoh teks seluruhnya huruf kapital.<br>
<em>Petunjuk:</em><br>
Contoh: <code>"SMK"</code>.</p>
</li>
</ol>
<h4 id="instruksi-tugas-rot13">Instruksi Tugas ROT13</h4>
<ol>
<li>Kembangkan antarmuka CLI untuk memilih mode ROT13 (enkripsi atau dekripsi).</li>
<li>Buat unit test untuk menguji fungsi ROT13 dengan berbagai jenis input.</li>
<li>Integrasikan fungsi ROT13 ke dalam aplikasi sederhana, misalnya simulasi pengiriman pesan terenkripsi.</li>
<li>Tambahkan opsi untuk menyimpan hasil enkripsi/dekripsi ke file.</li>
<li>Susun laporan yang menjelaskan kelebihan dan kekurangan ROT13 sebagai metode enkripsi.</li>
</ol>
<hr>
<h3 id="rot18">3.4 ROT18</h3>
<h4 id="konsep-dan-algoritma-3">Konsep dan Algoritma</h4>
<p>ROT18 adalah variasi dari ROT13 yang juga mengubah angka dengan menggunakan ROT5.</p>
<ul>
<li><strong>Proses:</strong>
<ul>
<li>Untuk huruf (kapital dan kecil), ROT18 melakukan ROT13 (geser 13 posisi).</li>
<li>Untuk digit (0-9), ROT18 melakukan ROT5 (geser 5 posisi, dengan modulus 10).</li>
<li>Karakter lain (simbol, spasi) tetap tidak berubah.</li>
</ul>
</li>
</ul>
<h4 id="contoh-kode-3">Contoh Kode</h4>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">import</span> string

<span class="token keyword">def</span> <span class="token function">rot18</span><span class="token punctuation">(</span>teks<span class="token punctuation">)</span><span class="token punctuation">:</span>
    <span class="token comment"># Tabel translasi untuk huruf dengan ROT13</span>
    rot13_table <span class="token operator">=</span> <span class="token builtin">str</span><span class="token punctuation">.</span>maketrans<span class="token punctuation">(</span>
        string<span class="token punctuation">.</span>ascii_uppercase <span class="token operator">+</span> string<span class="token punctuation">.</span>ascii_lowercase<span class="token punctuation">,</span>
        string<span class="token punctuation">.</span>ascii_uppercase<span class="token punctuation">[</span><span class="token number">13</span><span class="token punctuation">:</span><span class="token punctuation">]</span> <span class="token operator">+</span> string<span class="token punctuation">.</span>ascii_uppercase<span class="token punctuation">[</span><span class="token punctuation">:</span><span class="token number">13</span><span class="token punctuation">]</span> <span class="token operator">+</span>
        string<span class="token punctuation">.</span>ascii_lowercase<span class="token punctuation">[</span><span class="token number">13</span><span class="token punctuation">:</span><span class="token punctuation">]</span> <span class="token operator">+</span> string<span class="token punctuation">.</span>ascii_lowercase<span class="token punctuation">[</span><span class="token punctuation">:</span><span class="token number">13</span><span class="token punctuation">]</span>
    <span class="token punctuation">)</span>
    <span class="token comment"># Tabel translasi untuk digit dengan ROT5</span>
    rot5_table <span class="token operator">=</span> <span class="token builtin">str</span><span class="token punctuation">.</span>maketrans<span class="token punctuation">(</span><span class="token string">"0123456789"</span><span class="token punctuation">,</span> <span class="token string">"5678901234"</span><span class="token punctuation">)</span>
    <span class="token comment"># Terapkan ROT13 untuk huruf</span>
    hasil <span class="token operator">=</span> teks<span class="token punctuation">.</span>translate<span class="token punctuation">(</span>rot13_table<span class="token punctuation">)</span>
    <span class="token comment"># Terapkan ROT5 untuk digit</span>
    hasil <span class="token operator">=</span> hasil<span class="token punctuation">.</span>translate<span class="token punctuation">(</span>rot5_table<span class="token punctuation">)</span>
    <span class="token keyword">return</span> hasil

<span class="token comment"># Contoh penggunaan</span>
pesan_asli <span class="token operator">=</span> <span class="token string">"ROT18 Test 12345!"</span>
cipher <span class="token operator">=</span> rot18<span class="token punctuation">(</span>pesan_asli<span class="token punctuation">)</span>
plain <span class="token operator">=</span> rot18<span class="token punctuation">(</span>cipher<span class="token punctuation">)</span>  <span class="token comment"># Penerapan kedua mengembalikan pesan asli</span>

<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Pesan Asli   :"</span><span class="token punctuation">,</span> pesan_asli<span class="token punctuation">)</span>
<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Cipher Text  :"</span><span class="token punctuation">,</span> cipher<span class="token punctuation">)</span>
<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Dekripsi Hasil:"</span><span class="token punctuation">,</span> plain<span class="token punctuation">)</span>
</code></pre>
<h4 id="latihan-rot18-latihan-terpandu">Latihan ROT18 (Latihan Terpandu)</h4>
<ol>
<li>
<p><strong>Latihan 1:</strong><br>
<em>Tugas:</em> Pastikan fungsi ROT18 hanya memproses huruf dan digit, sedangkan simbol serta spasi tetap tidak berubah.<br>
<em>Petunjuk:</em><br>
Verifikasi bahwa kedua tabel translasi (huruf dan digit) sudah benar.</p>
</li>
<li>
<p><strong>Latihan 2:</strong><br>
<em>Tugas:</em> Buat antarmuka CLI untuk menerima input teks yang akan dienkripsi/dekripsi dengan ROT18.<br>
<em>Petunjuk:</em><br>
Gunakan:</p>
<pre class=" language-python"><code class="prism  language-python">teks <span class="token operator">=</span> <span class="token builtin">input</span><span class="token punctuation">(</span><span class="token string">"Masukkan teks untuk ROT18: "</span><span class="token punctuation">)</span>
</code></pre>
</li>
<li>
<p><strong>Latihan 3:</strong><br>
<em>Tugas:</em> Tambahkan validasi agar input tidak kosong.<br>
<em>Petunjuk:</em><br>
Periksa apakah:</p>
<pre class=" language-python"><code class="prism  language-python"><span class="token keyword">if</span> teks<span class="token punctuation">.</span>strip<span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">==</span> <span class="token string">""</span><span class="token punctuation">:</span>
    <span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Input tidak boleh kosong!"</span><span class="token punctuation">)</span>
    exit<span class="token punctuation">(</span><span class="token punctuation">)</span>
</code></pre>
</li>
<li>
<p><strong>Latihan 4:</strong><br>
<em>Tugas:</em> Buat fungsi tambahan untuk menampilkan perbandingan tiap karakter sebelum dan sesudah ROT18 (misalnya, “A -&gt; N” untuk huruf, “2 -&gt; 7” untuk digit).<br>
<em>Petunjuk:</em><br>
Iterasi setiap karakter dan tampilkan perbandingan jika karakter merupakan huruf atau digit.</p>
</li>
<li>
<p><strong>Latihan 5:</strong><br>
<em>Tugas:</em> Uji fungsi ROT18 dengan contoh teks yang mengandung huruf kapital, huruf kecil, dan angka.<br>
<em>Petunjuk:</em><br>
Contoh: <code>"SMK 2023!"</code>.</p>
</li>
</ol>
<h4 id="instruksi-tugas-rot18">Instruksi Tugas ROT18</h4>
<ol>
<li>Kembangkan antarmuka CLI untuk memilih mode ROT18 (enkripsi atau dekripsi).</li>
<li>Buat unit test untuk menguji fungsi ROT18 dengan berbagai jenis input (campuran huruf, angka, dan simbol).</li>
<li>Integrasikan fungsi ROT18 ke dalam aplikasi sederhana, misalnya simulasi pengiriman pesan terenkripsi yang juga memproses data numerik.</li>
<li>Tambahkan opsi untuk menyimpan hasil enkripsi/dekripsi ke file.</li>
<li>Susun laporan yang menjelaskan kelebihan dan kekurangan ROT18 sebagai metode enkripsi, serta perbandingannya dengan ROT13.</li>
</ol>
<hr>
<h2 id="kesimpulan">Kesimpulan</h2>
<p>Modul ini telah menggabungkan semua informasi penting dari referensi, sehingga kalian dapat memahami:</p>
<ul>
<li>Dasar-dasar kriptografi, terminologi, dan konsep Double Strength Encryption.</li>
<li>Pengenalan Python, termasuk instalasi melalui terminal di Kali Linux, tipe data dasar, dan instalasi paket kriptografi.</li>
<li>Implementasi teknik enkripsi sederhana: Reverse Cipher, Caesar Cipher, ROT13, dan ROT18—lengkap dengan contoh kode, penjelasan, latihan terpandu, serta tugas praktik.</li>
</ul>

