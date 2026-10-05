# UKHUWAH MART POS

Aplikasi kasir minimarket satu halaman. Produk, transaksi, inventori, akun, dan laporan disimpan di IndexedDB browser pada perangkat yang menjalankan aplikasi; tidak ada sinkronisasi antarperangkat.

## Menjalankan aplikasi

Jalankan server web lokal dari folder repository:

```sh
python3 -m http.server 8000
```

Buka `http://localhost:8000`, lalu buat akun Admin pertama. Akun karyawan dapat ditambahkan oleh Admin melalui menu Karyawan.

Database IndexedDB dan pustaka spreadsheet, scanner, serta cetak struk tersedia lokal di repo. Service worker menyimpan halaman dan aset aplikasi agar dapat dimuat kembali tanpa internet.

Untuk mengaktifkan mode offline, jalankan aplikasi melalui `localhost` atau HTTPS (bukan dengan membuka file HTML langsung), buka sekali saat online, lalu muat ulang setelah service worker aktif. Setelah itu halaman dan library yang sudah di-cache dapat digunakan tanpa internet. Browser harus tetap memiliki izin kamera; akses kamera memerlukan secure context seperti `localhost` atau HTTPS.

Library vendor di folder `vendor/`:

- SheetJS XLSX 0.18.5 — Apache-2.0
- html5-qrcode 2.3.8 — Apache-2.0
- PrintJS 1.6.0 — MIT

Setiap lisensi disertakan di folder yang sama dengan library.

## Catatan data

- Data hanya ada di browser/perangkat ini. Menghapus data situs atau berpindah browser/perangkat dapat menghilangkannya.
- Saat pertama dibuka setelah pembaruan, data lama dari `localStorage` otomatis dipindahkan ke IndexedDB dan kunci lama dihapus setelah migrasi berhasil.
- Service worker menyimpan aset aplikasi, bukan database; transaksi dan data tetap menggunakan IndexedDB browser.
- Ekspor produk, laporan, dan riwayat inventori secara berkala sebagai cadangan.
- Login dan peran hanya untuk alur kerja lokal; ini bukan sistem keamanan untuk data sensitif atau penggunaan multi-perangkat.
