# Rencana dan iterasi

[Beranda](00%20SAHAYA.md) · [Desain UI](02%20Alur%20dan%20UX.md)

## Berikutnya

1. **Tuntaskan pengalaman otomatis:** satu switch pencatatan; peta mengikuti driver; foto asli tampil di kartu tempat; UI ringkas. Uji izin ditolak, foto kosong, dan berhenti merekam ketika switch dimatikan.
2. **Pembaruan berdasarkan perpindahan:** Places setelah lebih dari **1 km** dan Air Quality setelah lebih dari **5 km** dari titik permintaan terakhir. Maksimum **50 permintaan per API dalam jendela berjalan 60 menit**; hitung foto/detail dalam kuota Places. Ini target, bukan jaminan biaya. AQI adalah estimasi pada titik yang dibulatkan, bukan rata-rata radius 5 km. Uji hitungan dan akses backend privat dari HP.
3. **Uji pilot:** satu perjalanan penuh di HP, dua pengingat, semua kategori/urutan, serta pembaruan otomatis BBM dan berita dengan sumber dan status data lama. Setelah itu, validasi kontribusi komunitas dengan lima driver pilot terverifikasi.

## Catatan singkat

- **0.4.4 Google · 23 November 2026:** Maps dan Places berfungsi di emulator, cuaca BMKG. Source checkpoint `8f3da36` lulus build debug, lint, 57 tes unit Android dan 6 tes backend. Tidak identik dengan APK publik; perubahan UI dan penyegaran lokasi belum diuji menyeluruh di HP.
- **Versi sebelumnya:** arsip APK cukup di [halaman unduhan](https://sahaya-test-download.vercel.app/). Tidak perlu catatan atau folder desain per versi.

## Alur tiap iterasi

Perbarui catatan Obsidian yang sudah ada: apa yang berubah, bukti tes, apa yang belum, dan referensi build. Gunakan satu desain aktif; ganti acuan lama alih-alih menambah duplikat. Commit dan push ke **`main`** di GitHub; verifikasi SHA. Dokumentasi publik adalah salinan tersaring dari Obsidian, bukan sinkronisasi otomatis. Jangan publikasikan key, rute, konfigurasi privat, atau data pribadi. Publikasikan APK yang sudah diverifikasi hanya lewat halaman unduhan yang sama.
