# Bot Auto Komen Facebook v1.0

Bot Auto Komen Facebook adalah sebuah skrip otomatisasi cerdas yang dirancang untuk meningkatkan interaksi dan mengarahkan lalu lintas (traffic) dari Facebook ke website Anda secara otomatis. Dijalankan sepenuhnya di cloud menggunakan **GitHub Actions**, bot ini dapat beroperasi 24/7 tanpa perlu menyalakan komputer Anda.

Bot ini sangat ideal untuk para blogger, digital marketer, atau siapa pun yang ingin meningkatkan jangkauan dan potensi monetisasi website mereka melalui Facebook.

---

## 📜 Aturan Lisensi (PENTING!)

Sebelum menggunakan, harap pahami dan setujui aturan lisensi berikut:

* **Aktivasi Lisensi**: Lisensi Anda adalah **email** yang Anda gunakan saat melakukan pembelian.
* **Masa Aktif**: Satu kali pembelian lisensi berlaku selama **3 (tiga) bulan**.
* **Penggunaan Akun**: Satu lisensi dapat digunakan untuk **banyak akun Facebook** tanpa batas. Cukup ganti *cookies* di GitHub Secrets.
* **Larangan**: Dilarang keras **membagikan, menjual kembali, atau mendistribusikan ulang** kode bot ini kepada orang lain. Lisensi terikat pada pembeli.

➡️ **Link Pembelian Lisensi Resmi:** **[http://lynk.id/botxautomation/34kvz08g6oz1](http://lynk.id/botxautomation/34kvz08g6oz1)**

---

## ✨ Fitur Unggulan

Bot ini terbagi menjadi dua mode utama yang bisa Anda pilih, masing-masing dengan fungsionalitasnya sendiri.

### **`index.js` (Bot Video Feed)**
Mode ini dirancang untuk berinteraksi dengan postingan video di **Facebook Watch (`facebook.com/watch/`)**.

* **Navigasi Otomatis**: Bot akan menelusuri feed Facebook Watch, menemukan video, dan secara otomatis pindah ke halaman video tersebut.
* **Anti-Duplikat Cerdas**: Menggunakan **URL video** sebagai ID unik yang disimpan dalam file `ceklink.txt`. Bot tidak akan pernah mengomentari video yang sama dua kali.
* **Kembali Otomatis**: Setelah berhasil berkomentar, bot akan secara otomatis kembali ke halaman Facebook Watch untuk mencari target video berikutnya.

### **`group.js` (Bot Grup Feed)**
Mode ini dioptimalkan untuk berinteraksi dengan postingan di **Feed Grup (`facebook.com/groups/feed/`)**, menjangkau audiens yang lebih tertarget.

* **Identifikasi Postingan Stabil**: Menggunakan atribut unik sebagai penanda posisi postingan di dalam feed.
* **Anti-Duplikat Sesi**: Bot menandai postingan yang sudah dikomentari **dalam satu sesi eksekusi** untuk memastikan ia terus bergerak ke bawah feed dan tidak terjebak di postingan yang sama.
* **Interaksi Langsung**: Berkomentar langsung dari halaman feed tanpa perlu navigasi ke halaman postingan tunggal, membuat interaksi lebih cepat dan efisien.

### **Fitur Umum (Berlaku untuk Kedua Bot)**
* **Otomatisasi Penuh di Cloud**: Berjalan 100% gratis di **GitHub Actions** dengan jadwal yang bisa diatur (Cron Job).
* **Login Aman via Cookies**: Tidak perlu menyimpan username dan password. Cukup gunakan *cookies* browser yang diekspor.
* **Komentar Dinamis & Multi-baris**: Ambil komentar dari file `comments.txt`. Mendukung **emoji, karakter UTF-8, dan komentar dengan beberapa baris (Enter)** untuk tampilan yang lebih natural.
* **Perilaku Mirip Manusia**: Dilengkapi **jeda waktu acak** antar komentar untuk menghindari deteksi spam.
* **Fitur Stop Otomatis**: Bot akan berhenti secara otomatis jika tidak menemukan postingan baru setelah 5 kali *scroll* berturut-turut.
* **Konfigurasi Mudah**: Semua pengaturan penting (jumlah komentar, jeda waktu, URL target) diatur melalui file `config.json` & `configgroup.json`.

---

## 🚀 Panduan Menjalankan Bot di GitHub Actions

Panduan ini akan memandu Anda untuk mengatur dan menjalankan bot sepenuhnya di cloud menggunakan GitHub Actions, tanpa perlu menjalankan apa pun di komputer pribadi Anda.

---

### **Langkah 1: Pengaturan GitHub Secrets (Paling Penting)**

Bot ini memerlukan dua "kunci rahasia" (Secrets) untuk bisa login dan tervalidasi. Anda harus menyimpannya di pengaturan repository GitHub Anda.

1.  Buka repository Anda di GitHub, lalu pergi ke tab **`Settings`**.
2.  Di menu sebelah kiri, navigasi ke **`Secrets and variables`** > **`Actions`**.
3.  Klik tombol **`New repository secret`** dan buat dua *secret* berikut satu per satu:

#### **Secret #1: Cookies Akun Facebook**
* **Nama**: `FACEBOOK_COOKIES`
* **Value**:
    1.  Di komputer Anda, buka browser Chrome dan **login ke akun Facebook** yang ingin Anda gunakan.
    2.  Klik ikon ekstensi **Cookie-Editor**.
    3.  Pilih **`Export`**, lalu pilih **`Export as JSON`**.
    4.  Klik **`Copy to Clipboard`**.
    5.  Tempelkan semua teks yang sudah disalin ke dalam kolom *Value* di GitHub.

#### **Secret #2: Lisensi Bot**
* **Nama**: `BOT_LICENSE_EMAIL`
* **Value**: Masukkan **email** yang Anda gunakan saat membeli lisensi bot.

---

### **Langkah 2: Konfigurasi Bot (`config.json`) Untuk Auto Komen Video dan (`configgroup.json`) untuk Auto Komen Group**

Sebelum menjalankan bot, Anda bisa menyesuaikan perilakunya dengan mengedit file `config.json` & `configgroup.json` di repository Anda.

* `"postsToComment"`: Atur berapa banyak komentar yang ingin dikirim bot dalam satu kali jalan.
* `"minIntervalSeconds"` & `"maxIntervalSeconds"`: Atur jeda waktu acak (dalam detik) antar komentar untuk meniru perilaku manusia.

---

### **Langkah 3: Atur Daftar Komentar (`comments.txt`)**

Edit file `comments.txt` untuk mengatur variasi komentar yang akan digunakan oleh bot.

* Gunakan `---` (tiga tanda hubung) pada baris baru untuk **memisahkan antar komentar**.
* Anda bisa menekan `Enter` untuk membuat baris baru di dalam satu blok komentar untuk memberikan jarak.
* File ini mendukung penuh karakter **UTF-8**, termasuk emoji 😎.

---

### **Langkah 4: Pilih Bot yang Akan Dijalankan (`main.yml`)**

Anda bisa memilih untuk menjalankan bot video atau bot grup.

1.  Buka file `.github/workflows/main.yml`.
2.  Cari bagian **`cron: '0 */6 * * *'`**.
3.  Ubah baris `/6` sesuai kebutuhan:
    * '0 */6 * * *': `bot di eksekusi setiap 6 jam sekali`
    * '0 */2 * * *': `bot di eksekusi setiap 2 jam sekali`

---

### **Langkah 5: Menjalankan Bot Secara Manual**

Bot akan berjalan otomatis sesuai jadwal yang ditentukan. Namun, Anda bisa menjalankannya secara manual kapan saja.

1.  Buka tab **`Actions`** di repository GitHub Anda.
2.  Di daftar workflow sebelah kiri, klik nama workflow Anda (misalnya, **"Facebook Group Comment Bot"**).
3.  Di sebelah kanan, akan muncul tombol **`Run workflow`**. Klik tombol tersebut, lalu klik tombol hijau **`Run workflow`** lagi untuk memulai.

Bot akan mulai berjalan, dan Anda bisa melihat lognya secara *real-time*.
