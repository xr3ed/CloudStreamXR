# CloudStreamXR 🚀

Repositori resmi untuk distribusi, metadata rilis, dan pembaruan otomatis aplikasi klon **CloudStreamXR**. Aplikasi ini dikustomisasi secara khusus menggunakan pipeline Android App Cloner dengan integrasi keamanan tingkat lanjut dan alur pembaruan in-app yang mulus.

---

## 🌟 Fitur Unggulan CloudStreamXR

Aplikasi klon ini dilengkapi dengan fitur premium berikut:

### 1. 🛡️ Proteksi Keamanan Tingkat Tinggi
* **Self-Locking Signature**: Mengunci sidik jari enkripsi (signature) APK pada instalasi pertama di perangkat pengguna. Jika APK dimodifikasi atau ditandatangani ulang oleh pihak ketiga, aplikasi akan mendeteksinya dan otomatis menolak berjalan.
* **Anti-Tamper & Anti-Debugger**: Proteksi agresif terhadap percobaan rekayasa balik (reverse engineering) atau debugging. Aplikasi akan langsung mematikan prosesnya (`android.os.Process.killProcess`) jika mendeteksi debugger aktif atau bendera debug dinyalakan di manifes.

### 2. 🔄 In-App Auto Update (Pembaruan Otomatis)
* **Pengecekan Asinkron**: Setiap kali aplikasi diluncurkan, ia akan membaca konfigurasi jarak jauh `update.json` di latar belakang secara asinkron.
* **Dialog Unduhan Kustom**: Jika tersedia versi terbaru, aplikasi memunculkan dialog pembaruan otomatis. Saat proses download berlangsung, aplikasi menampilkan progress bar horizontal dengan hitungan byte real-time (misal: `Mengunduh: 45% (12.40 MB / 27.50 MB)`).
* **Auto-Installer via FileProvider**: Setelah berkas APK selesai diunduh, aplikasi secara otomatis memicu Android Package Installer menggunakan `FileProvider` resmi bawaan aplikasi secara dinamis.
* **Build-Time Detection**: Deteksi pembaruan menggunakan penanda waktu (timestamp) milidetik yang di-inject otomatis saat proses kloning berjalan. Mencegah error loop update pada nomor versi yang sama.

### 3. 🎨 Kustomisasi Dinamis
* **Custom Extension Label**: Label ekstensi/plugin dapat disesuaikan untuk melokalisasi menu (misal: *"Ekstensi Saya"*, *"Daftar Provider"*, dll.).
* **QRIS Donation Integration**: Menampilkan dialog donasi QRIS kustom untuk mempermudah donatur melakukan scan kode pembayaran langsung dari dalam aplikasi.

---

## 📁 Struktur Metadata Pembaruan (`update.json`)

Berkas `update.json` di repositori ini berfungsi sebagai pusat kontrol pembaruan aplikasi klon. Format konfigurasinya adalah sebagai berikut:

```json
{
  "versionCode": 29718408,
  "versionName": "4.7.0-PRE",
  "apkUrl": "https://github.com/xr3ed/CloudStreamXR/releases/download/4.7.0-PRE/app-cloned.apk",
  "changelog": "Pembaruan rutin stabilitas aplikasi.",
  "forceUpdate": true,
  "buildTime": 17834523901
}
```

* **`versionCode`**: Kode versi asli APK pembantu.
* **`versionName`**: Label nama rilis yang akan ditampilkan di dialog pembaruan HP pengguna.
* **`apkUrl`**: Link tautan unduhan langsung berkas APK baru (diarahkan ke GitHub Releases).
* **`forceUpdate`**: Jika diset `true`, pengguna tidak bisa melewati dialog update dan tombol negatif akan berubah menjadi tombol keluar aplikasi paksa.
* **`buildTime`**: Penanda unik waktu pembuatan klon untuk mendeteksi update tumpang-tindih.

---

## 🛠️ Cara Merilis Update (DevOps Sekali Klik)

Pembaruan dapat dirilis langsung dari aplikasi **App Cloner** di HP Anda tanpa menyentuh terminal komputer:
1. Buat klon baru di menu **Clone**.
2. Masuk ke tab **History** di Cloner.
3. Klik tombol ikon **Awan (Cloud Upload)** di samping riwayat klon yang baru dibuat.
4. Masukkan nomor versi, tag rilis, dan changelog di dialog pop-up yang muncul.
5. Klik **Push Now**. Aplikasi Cloner akan otomatis membuat rilis baru di GitHub, mengunggah APK, dan memperbarui berkas `update.json` di repositori ini secara instan!

---
*Dikembangkan dengan ❤️ untuk CloudStreamXR Community.*