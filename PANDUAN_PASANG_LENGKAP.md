# Panduan Lengkap Memasang My Money di iPhone (Safari)

Panduan ini menjelaskan cara menerbitkan My Money menjadi website HTTPS, lalu memasangnya pada Home Screen iPhone seperti aplikasi. Ikuti urutan dari Bagian A sampai D.

> **Penting:** ZIP ini berisi source code website. ZIP tidak dapat langsung dipasang sebagai aplikasi di iPhone. Website harus diterbitkan ke internet terlebih dahulu. Sesudah URL website aktif, barulah URL itu ditambahkan ke Home Screen melalui Safari.

## Ringkasan alur

1. Unduh dan ekstrak `MyMoney_Safari_PWA.zip`.
2. Masukkan file proyek ke repository GitHub.
3. Biarkan GitHub Actions menjalankan workflow publikasi.
4. Buka URL website yang berhasil diterbitkan.
5. Di Safari iPhone, pilih **Bagikan → Tambahkan ke Layar Utama**.
6. Buka My Money dari ikon barunya.

## Bagian A — Siapkan file ZIP

1. Unduh file `MyMoney_Safari_PWA.zip` dari percakapan ini.
2. Di komputer Windows: klik kanan ZIP → **Extract All / Ekstrak Semua**. Di Mac: klik dua kali ZIP. Di iPhone: buka aplikasi **Files / File**, cari ZIP di Downloads, lalu ketuk ZIP untuk mengekstraknya.
3. Setelah diekstrak, buka folder `MyMoney_Safari_PWA`.
4. Pastikan file dan folder ini ada:

   ```text
   index.html
   app.js
   styles.css
   manifest.webmanifest
   sw.js
   assets/
     icon.svg
     icon-192.png
     icon-512.png
   .github/
     workflows/
       deploy-pages.yml
   README.md
   PANDUAN_PASANG_LENGKAP.md
   ```

5. **Jangan unggah file ZIP sebagai satu file saja.** Yang perlu dimasukkan ke repository adalah isi folder hasil ekstrak.
6. Untuk mempermudah, lakukan langkah unggah dan pengaturan pertama kali memakai komputer/laptop dengan browser. Setelah website live, pemakaian sehari-hari cukup lewat iPhone.

## Bagian B — Buat repository GitHub

1. Buka [https://github.com](https://github.com) dan masuk ke akun GitHub. Jika belum punya akun, pilih **Sign up** dan selesaikan pendaftarannya.
2. Buka [https://github.com/new](https://github.com/new).
3. Isi **Repository name** dengan `my-money-safari` (boleh nama lain, tetapi catat nama yang dipakai).
4. Pilih **Public** sebagai pilihan paling sederhana untuk GitHub Free. Ingat: website yang diterbitkan lewat GitHub Pages akan dapat diakses publik. Jangan masukkan transaksi pribadi, password, kunci API, atau file rahasia ke dalam repository.
5. Untuk membuat repository kosong, jangan centang opsi untuk menambahkan README, `.gitignore`, atau license. Klik **Create repository**.
6. Biarkan halaman repository baru terbuka.

## Bagian C — Unggah file proyek dengan struktur yang benar

### Metode yang disarankan: unggah dari komputer

1. Di halaman repository, pilih **Add file → Upload files**.
2. Dari folder hasil ekstrak, pilih atau seret **isi folder proyek**, bukan folder terluarnya dan bukan ZIP. Pastikan struktur folder dipertahankan, terutama `assets/` dan `.github/workflows/`.
3. Jika browser tidak mempertahankan folder saat memilih banyak file, gunakan folder/unggahan yang mempertahankan struktur, atau buat file workflow secara manual menggunakan petunjuk di bagian “Jika folder .github tidak ikut terunggah”.
4. Sebelum menyimpan, cek bahwa `index.html`, `app.js`, `styles.css`, `manifest.webmanifest`, dan `sw.js` muncul langsung pada tingkat paling atas repository. Folder `assets` juga harus berada pada tingkat yang sama.
5. Scroll ke bagian bawah halaman.
6. Pada kotak **Commit changes**, isi pesan misalnya `Add My Money web app`.
7. Klik **Commit changes**. Tunggu sampai GitHub selesai menyimpan file.

### Jika folder `.github/workflows` tidak ikut terunggah

Folder yang namanya diawali titik kadang tersembunyi atau tidak ikut saat mengunggah. Workflow diperlukan untuk cara publikasi otomatis dalam paket ini.

1. Di halaman utama repository, pilih **Add file → Create new file**.
2. Pada kolom nama file, masukkan path lengkap berikut: `.github/workflows/deploy-pages.yml`. GitHub akan membuat struktur folder berdasarkan path tersebut.
3. Buka file `deploy-pages.yml` di hasil ekstrak ZIP dengan editor teks, salin seluruh isinya, lalu tempel ke editor GitHub.
4. Klik **Commit changes**.
5. Pastikan file tersebut benar-benar terlihat pada path `.github/workflows/deploy-pages.yml` di repository.

### Contoh struktur repository yang benar

```text
my-money-safari/           ← root repository
├── index.html
├── styles.css
├── app.js
├── manifest.webmanifest
├── sw.js
├── assets/
│   ├── icon.svg
│   ├── icon-192.png
│   └── icon-512.png
└── .github/
    └── workflows/
        └── deploy-pages.yml
```

**Jangan** menaruh semuanya di dalam satu folder tambahan seperti `MyMoney_Safari_PWA/index.html`. Jika `index.html` berada satu tingkat terlalu dalam, proses publikasi dapat gagal atau website menampilkan 404.

## Bagian D — Aktifkan GitHub Pages dan jalankan workflow

1. Di repository, klik tab **Settings**. Pada layar sempit, Settings mungkin berada di menu tab tambahan.
2. Di sisi kiri, buka **Pages**. Jika perlu, cari bagian **Code and automation → Pages**.
3. Pada bagian **Build and deployment**, cari **Source** lalu pilih **GitHub Actions**.
4. Kembali ke tab **Actions** di repository.
5. Cari workflow bernama **Deploy My Money to GitHub Pages**. Jika workflow tidak muncul, periksa apakah file `.github/workflows/deploy-pages.yml` sudah berada di lokasi yang benar dan sudah di-commit ke branch `main`.
6. Setelah commit pertama, workflow biasanya berjalan otomatis. Buka workflow itu, lalu buka run terbaru untuk melihat status.
7. Tunggu sampai job selesai dengan tanda centang hijau. Jika masih berjalan, tunggu hingga selesai; jika merah, buka job dan baca pesan error.
8. Jika tidak berjalan otomatis, buka workflow tersebut dan pilih **Run workflow** jika tombol tersedia, kemudian jalankan pada branch `main`.
9. Kembali ke **Settings → Pages** atau buka detail deployment yang berhasil. Cari tautan situs yang berakhiran `github.io`.
10. URL biasanya berbentuk `https://NAMA-AKUN.github.io/NAMA-REPOSITORY/`. Ganti `NAMA-AKUN` dan `NAMA-REPOSITORY` dengan akun serta nama repository milikmu. **Jangan menebak URL** jika tautan sebenarnya sudah ditampilkan di GitHub.
11. Buka URL itu dan pastikan dashboard My Money terlihat. Bila baru saja dipublikasikan, tunggu beberapa saat lalu muat ulang halaman.

## Bagian E — Pasang My Money pada iPhone

Lakukan bagian ini setelah website berhasil terbuka melalui alamat HTTPS `github.io`.

1. Di iPhone, buka aplikasi **Safari**. Jangan memulai dari browser mini di dalam aplikasi chat atau media sosial.
2. Ketik atau tempel URL website GitHub Pages yang benar ke bilah alamat Safari.
3. Tunggu My Money selesai dimuat. Pastikan halaman dashboard muncul dan navigasi dapat digunakan.
4. Ketuk tombol **Bagikan / Share**. Ikonnya biasanya berbentuk kotak dengan panah ke atas. Letaknya dapat berbeda tergantung tata letak Safari.
5. Gulir menu berbagi ke bawah dan pilih **Tambahkan ke Layar Utama / Add to Home Screen**.
6. Jika pilihan tersebut tidak muncul, gulir ke bagian bawah menu, pilih **Edit Actions / Edit Tindakan**, lalu tambahkan tindakan **Add to Home Screen** jika tersedia.
7. Periksa nama ikon. Gunakan `My Money` atau nama pilihanmu.
8. Jika tersedia, aktifkan **Open as Web App / Buka sebagai App Web** agar dibuka dengan pengalaman seperti aplikasi.
9. Ketuk **Tambah / Add**.
10. Kembali ke Home Screen. Ikon **My Money** seharusnya sudah muncul.
11. Ketuk ikon tersebut untuk membuka aplikasi. Uji navigasi, tambah satu transaksi percobaan, lalu pastikan saldo berubah sesuai catatan.
12. Setelah uji coba, hapus transaksi percobaan atau pulihkan backup yang sesuai sebelum memasukkan data sebenarnya.

## Bagian F — Pengaturan awal dan penggunaan

1. Buka tab **Akun**.
2. Isi nama panggilan.
3. Masukkan **saldo awal** sesuai uang yang ingin dijadikan titik awal pencatatan. Jika ingin mulai dari nol, gunakan `0`.
4. Isi target tabungan jika diperlukan.
5. Tekan **Simpan pengaturan**.
6. Buka **Transaksi** atau tombol `+` untuk mencatat pemasukan/pengeluaran.
7. Pilih jenis transaksi, nama/keterangan, nominal, kategori, dan tanggal. Periksa tanda desimal/nominal sebelum menyimpan.
8. Buka **Laporan** untuk melihat ringkasan dan grafik.
9. Buka **Akun → Backup** secara berkala. Simpan file JSON ke Files/iCloud Drive atau tempat aman lain.
10. Untuk membuka data di spreadsheet, pilih **Ekspor CSV**. Pada iPhone, file mungkin terbuka sebagai pratinjau; gunakan tombol Share lalu **Save to Files / Simpan ke File**.

## Bagian G — Membuat pembaruan otomatis

Setelah pemasangan pertama, setiap perubahan file yang di-commit ke branch `main` akan memicu workflow publikasi secara otomatis.

1. Buka repository GitHub.
2. Edit atau unggah file yang ingin diperbarui.
3. Simpan perubahan dengan **Commit changes** ke branch `main`.
4. Buka **Actions → Deploy My Money to GitHub Pages** dan pastikan run terbaru hijau.
5. Buka ulang website di iPhone.
6. Jika yang terlihat masih versi lama, tutup aplikasi My Money sepenuhnya, buka kembali, lalu reload Safari. Service worker dapat membuat versi cache terlihat sementara.

## Troubleshooting — masalah yang sering terjadi

### Website menampilkan 404 / tidak ditemukan

- Pastikan `index.html` berada langsung di root repository, bukan di folder tambahan.
- Pastikan nama repository dan URL yang dibuka benar.
- Pastikan GitHub Pages sudah disetel ke **GitHub Actions**.
- Buka **Actions** dan cek apakah workflow terakhir hijau.
- Jika workflow merah, buka run tersebut untuk membaca langkah mana yang gagal.

### Workflow tidak muncul di tab Actions

- Pastikan `.github/workflows/deploy-pages.yml` berada persis di lokasi tersebut.
- Pastikan file sudah di-commit ke branch default `main`.
- Pastikan bukan hanya ZIP yang diunggah ke repository.

### Workflow merah / gagal menerbitkan

- Pastikan `index.html`, `app.js`, `styles.css`, `manifest.webmanifest`, `sw.js`, `assets/icon-192.png`, dan `assets/icon-512.png` ada.
- Periksa apakah nama file dan huruf besar-kecilnya sama persis.
- Buka log job untuk mengetahui pesan error spesifik; jangan hanya menjalankan ulang tanpa memperbaiki penyebabnya.

### Ikon tidak muncul atau Add to Home Screen tidak tersedia

- Buka URL HTTPS di Safari, bukan browser dalam aplikasi lain.
- Gunakan menu **Share → Add to Home Screen**.
- Pastikan website sudah terbit dan dapat dibuka normal terlebih dahulu.

### Data hilang atau tidak sama pada dua perangkat

- Catatan disimpan secara lokal pada browser/perangkat. Data tidak otomatis sinkron antar-iPhone, iPad, atau komputer.
- Jangan hapus data website Safari sebelum backup.
- Untuk pindah perangkat, gunakan **Backup JSON** di perangkat lama, lalu **Pulihkan** di perangkat baru.
- Jangan gunakan Private Browsing untuk penyimpanan utama.

### Hasil scan struk atau input suara keliru

- OCR hanya perkiraan; pastikan nominal dan tanggal benar sebelum menyimpan.
- Scan struk membutuhkan internet saat mesin OCR dimuat.
- Dikte suara bergantung pada dukungan Safari/iOS, izin mikrofon, dan bahasa. Jika tidak berjalan, gunakan keyboard/dikte iPhone atau masukkan secara manual.

### Data tidak otomatis dicadangkan ke iCloud

- Penyimpanan aplikasi tidak sama dengan sinkronisasi iCloud. Simpan file Backup JSON ke Files/iCloud Drive secara manual.

## Keamanan dan privasi

- GitHub Pages adalah website publik. Source code yang diunggah tidak boleh berisi transaksi pribadi, PIN, kata sandi, OTP, atau kredensial bank.
- Data keuangan yang kamu masukkan ke My Money tersimpan pada browser/perangkat, bukan di database online milik aplikasi ini.
- Jika browser atau data website dibersihkan, catatan lokal dapat hilang. Backup rutin sangat dianjurkan.
- Jangan pernah menempelkan kata sandi, OTP, PIN, atau kredensial perbankan ke kolom teks mutasi.
- Fitur ini untuk pencatatan manual, bukan koneksi langsung ke rekening bank.

## Sumber resmi

- GitHub Pages dengan GitHub Actions: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
- Apple — menambahkan situs menjadi aplikasi web di iPhone: https://support.apple.com/guide/iphone/open-as-web-app-iphea86e5236/27/ios/27

---

**Jika selesai:** simpan URL `github.io` milikmu di tempat aman. Untuk penggunaan harian, kamu tidak perlu membuka GitHub lagi—cukup ketuk ikon My Money di Home Screen iPhone.
