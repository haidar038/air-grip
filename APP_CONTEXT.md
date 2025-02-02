### **Konteks Terbaru: Gesture-Operated File Transfer Web App (Optimized & Mobile-Ready)**

#### **Deskripsi Proyek:**

Web app ini memungkinkan transfer file antar perangkat dengan menggunakan **gesture tangan** sebagai mekanisme utama untuk memilih dan mengirim file. Aplikasi ini didesain agar **ringan**, **responsif**, dan **mobile-friendly**, sehingga dapat berjalan dengan optimal pada perangkat dengan sumber daya terbatas, seperti smartphone dan tablet.

#### **Fitur Utama:**

1. **Deteksi Gesture Real-Time:**

   - **Gesture Grab:** Pengguna dapat melakukan gesture “grab” (mendekatkan ujung jari telunjuk dan ibu jari) untuk memulai proses pengiriman atau penerimaan file.
   - **Optimasi Deteksi:** Menggunakan [TensorFlow Handpose](https://github.com/tensorflow/tfjs-models/tree/master/handpose) untuk mendeteksi gesture dengan teknik **debouncing** guna mencegah pemicu berulang.

2. **Transfer File dengan Chunking:**

   - File dipecah menjadi potongan-potongan (chunk) berukuran 16KB untuk dikirim secara bertahap melalui **WebRTC Data Channel**.
   - Proses transfer dilengkapi dengan **progress bar** untuk memberikan informasi real-time tentang kemajuan pengiriman.

3. **Dukungan Mode Pengguna Ganda:**

   - **Sender Mode:** Pengguna memilih file dari perangkat melalui elemen input file yang telah dioptimalkan untuk mobile. Pengiriman file dimulai dengan gesture grab.
   - **Receiver Mode:** Pengguna menunggu koneksi dan mengonfirmasi penerimaan file dengan gesture grab.

4. **Signaling Manual:**

   - Untuk keperluan demo, proses signaling (pertukaran offer dan answer untuk WebRTC) dilakukan secara manual melalui textarea.
   - Di masa depan, signaling dapat diotomatisasi dengan backend server untuk mempercepat koneksi.

5. **Optimasi Performa untuk Mobile:**
   - **Struktur Responsif:** Penggunaan Bootstrap dan CSS responsif memastikan tampilan optimal di layar kecil.
   - **Atribut `defer` dan Penggunaan Cache DOM:** Mengurangi blocking pada render dan meningkatkan kecepatan loading di perangkat mobile.
   - **Optimasi Kamera dan Gesture:** Pemanfaatan `getUserMedia` dengan resolusi yang sesuai dan pemrosesan gesture menggunakan `requestAnimationFrame` agar penggunaan CPU minimal pada perangkat dengan sumber daya terbatas.

#### **Spesifikasi Teknis:**

- **Teknologi Front-End:**
  - **HTML, CSS, dan Vanilla JavaScript:** Untuk performa maksimal tanpa framework berat.
  - **Bootstrap 5:** Memastikan tampilan antarmuka yang responsif dan user-friendly.
- **Teknologi Machine Learning & Gesture:**

  - **TensorFlow.js & Handpose:** Untuk mendeteksi gesture secara real-time dengan akurasi tinggi.
  - **Debouncing dan Thresholding:** Mencegah pemicu gesture berulang dan memastikan hanya gesture yang valid yang diproses.

- **Transfer Data dan Konektivitas:**

  - **WebRTC Data Channel:** Untuk mentransfer file secara langsung antar perangkat.
  - **Chunking File:** Pengiriman file dalam potongan kecil untuk efisiensi dan monitoring progress.

- **Pengoptimalan Mobile:**
  - **Viewport Meta Tag & CSS Responsif:** Agar tampilan dan interaksi optimal pada berbagai ukuran layar.
  - **Optimasi Skrip:** Penggunaan atribut `defer` dan caching DOM untuk mempercepat loading halaman.

#### **Alur Kerja Aplikasi:**

1. **Halaman Utama:**
   - Pengguna memilih peran: **Sender** atau **Receiver**.
2. **Mode Pengirim (Sender):**
   - Pengguna memilih file melalui input file yang dioptimalkan untuk mobile.
   - File dipilih ditampilkan dengan detail (nama, ukuran) dan proses transfer dimulai setelah gesture grab terdeteksi.
   - File dikirim secara bertahap dengan progress bar yang menampilkan status pengiriman.
3. **Mode Penerima (Receiver):**
   - Pengguna menunggu koneksi dari sender dan siap menerima file setelah melakukan gesture grab.
   - File yang diterima disusun kembali dan link unduhan disediakan setelah transfer selesai.
4. **Pertukaran Signaling:**
   - Pertukaran offer dan answer dilakukan secara manual melalui textarea.
   - Status koneksi ditampilkan secara real-time.
5. **Penyelesaian Transfer:**
   - Setelah transfer selesai, pengguna dapat mendownload file dan kembali ke halaman utama untuk memulai proses baru.
