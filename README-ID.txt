KENDEVSEC — ULTIMATE ADMIN DASHBOARD (EXPANDED)
================================================

FITUR WEBSITE PUBLIK
- Beranda premium, responsive/mobile-first, navigasi mobile.
- Daftar layanan dari Firestore dan tombol pesan.
- Form permintaan layanan tersimpan ke Firestore.
- Setelah pengiriman order, WhatsApp dibuka dengan detail permintaan.
- Kode promo (validasi dasar: kode aktif dan diskon).
- Artikel/jurnal, FAQ, testimoni, announcement bar, bagian halaman dinamis.
- Kontak WhatsApp, email, Instagram.
- Maintenance mode dan SEO title/description.

FITUR ADMIN
- Login email/password melalui Firebase Authentication.
- Pemeriksaan UID admin melalui dokumen admins/{UID}.
- Dashboard ringkasan data.
- CRUD layanan dan kategori.
- CRUD artikel, FAQ, testimoni, kode promo, bagian halaman (page builder berbasis blok).
- Upload gambar langsung ke Firebase Storage untuk layanan, artikel, testimoni, dan blok halaman (JPG/PNG/WEBP/GIF, maks. 5 MB).
- Daftar pesanan dan perubahan status: new / processing / done / cancelled.
- Pengaturan brand, teks hero, tentang, kontak, SEO, announcement, maintenance.
- Log aktivitas admin.
- Layout responsive untuk perangkat mobile.

PERSIAPAN FIREBASE
1. Buat proyek Firebase baru.
2. Authentication > Get started > Sign-in method > aktifkan Email/Password.
3. Authentication > Users > Add user untuk membuat akun admin.
4. Salin UID user tersebut.
5. Firestore Database > Create database.
6. Firestore > Rules: tempel isi firestore.rules lalu Publish.
7. Firebase Console > Storage > Get started > pilih lokasi bucket. Buka tab Rules, tempel isi storage.rules lalu Publish.
8. Buat collection admins. Document ID harus sama persis dengan UID admin.
   Tambahkan field active (boolean) = true dan role (string) = owner.
9. Project settings > General > Your apps > Add app > Web app.
10. Salin firebaseConfig ke assets/firebase-config.js. Ganti seluruh placeholder.
11. Authentication > Settings > Authorized domains: tambahkan domain GitHub Pages.
12. Upload isi folder ini ke repository GitHub. Settings > Pages > Deploy from a branch > main > /(root).
13. Buka /admin.html untuk login.

CATATAN KEAMANAN DAN PRODUKSI
- Jangan membagikan password admin atau service-account private key.
- API key Firebase web bukan rahasia admin; Firestore Security Rules dan Auth yang
  mengontrol akses data.
- Rules memberi baca publik untuk konten katalog, FAQ, testimoni, kategori, dan
  pengaturan publik. Jangan menyimpan data rahasia di koleksi yang dibaca publik.
- Kode promo dibaca publik pada implementasi starter ini. Jangan gunakan kode promo
  sebagai mekanisme diskon bernilai tinggi tanpa validasi server-side.
- Untuk produksi, validasi harga, diskon, status order, rate limiting, dan notifikasi
  sebaiknya dipindah ke Cloud Functions / backend tepercaya.
- Order publik membatasi field dan tipe dasar; aktifkan App Check dan pantau abuse.
- Upload gambar memakai Firebase Storage; bucket harus diaktifkan dan storage.rules harus dipasang. File publik dapat dilihat melalui URL download; hanya admin aktif yang boleh mengunggah.
- "Bagian halaman" tersimpan dan dapat dikelola, namun belum menjadi visual drag-drop
  page builder; konten halaman publik utama masih menggunakan template tetap.
- Role admin tunggal owner; manajemen role multi-user belum dibuat.
- Email otomatis, invoice PDF, payment gateway, live chat, dan analytics eksternal
  belum terhubung.
- Pastikan menguji rules, order, promo, dan login di proyek Firebase milik sendiri.

TROUBLESHOOTING
- auth/unauthorized-domain: tambah domain GitHub Pages di Authorized domains.
- Login ditolak: cek UID dokumen admins/{UID} dan active boolean true.
- Data kosong: periksa firebaseConfig, Rules, koneksi internet, dan nama koleksi.

FITUR MEDIA / PAGE BUILDER
- Pada menu Layanan, Artikel, Testimoni, dan Bagian halaman tersedia upload gambar langsung.
- Bagian halaman dapat diurutkan dengan angka sort dan ditampilkan/disembunyikan lewat checkbox aktif.
- Ini page builder berbasis blok konten, bukan editor drag-and-drop bebas.
