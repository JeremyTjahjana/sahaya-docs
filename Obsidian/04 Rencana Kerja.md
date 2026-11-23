# Rencana dan iterasi

[Beranda](00%20SAHAYA.md) · [Desain UI](02%20Alur%20dan%20UX.md)

## Berikutnya

1. **0.4.5 — fokus peta:** switch pencatatan tunggal, foto asli pada kartu, peta otomatis mengikuti driver, UI ringkas. Places mencari ulang setelah >1 km dari titik permintaan sebelumnya, 50 permintaan per 60 menit berjalan per instalasi termasuk detail/foto.
2. **Polusi dan tes:** gunakan PM2.5 Open-Meteo/CAMS regional untuk uji nonkomersial, bukan Google Air Quality atau estimasi per jalan. Cuaca tetap BMKG; Mode Dev menampilkan joystick di Kinerja dan tiga tombol tes: minum, jas hujan, dan rehat dengan saran tempat.
3. **Uji pilot:** satu perjalanan penuh di HP, dua pengingat, semua kategori/urutan, serta pembaruan otomatis BBM dan berita dengan sumber dan status data lama. Setelah itu, validasi kontribusi komunitas dengan lima driver pilot terverifikasi.

## Log penting — 0.4.5 Google

- **Status:** dibangun lokal dan diuji di emulator Google APIs Android 28. `versionCode=10`, `id.sahaya.app.test`, Android 8.0+, tanda tangan debug sama dengan APK sebelumnya. Diterbitkan di Vercel pada 23 November 2026. Unduhan tanpa login lolos verifikasi byte-for-byte; 0.4.4 Google masih tersedia di arsip. Source diverifikasi di `sahaya-android/main` (`4a7fd93`).
- **Hasil:** build debug dan release unsigned lulus; 60 tes unit, 0 lint error (47 warning). Runner Google melaporkan `OK (21 tests)` dengan satu tes khusus varian tanpa key dilewati. Foto asli Resto Raasaa dengan kredit terlihat di kartu. GPS emulator berpindah lebih dari 1 km, kamera dan daftar diperbarui; kuota jam berjalan diuji otomatis. Switch menghidupkan/mematikan foreground service. Tiga notifikasi Dev dan panel rehat dicoba di emulator; perjalanan dan alarm terjadwal belum diuji di HP fisik.
- **Artefak lokal:** `app/build/outputs/apk/debug/app-debug.apk`, SHA-256 `e07422414b9d45be66114edef5101b9fc0a86264d87c2daa4e7b2cdf0bcd3585`. Identik dengan `sahaya-0.4.5-google-test.apk` pada halaman unduhan publik.
- **Mulai iterasi berikutnya:** baca catatan ini dahulu; checkout aktif `sahaya-google-migration`, langsung di `main`. `NearbyUiState`/`RollingProviderLimit` mengatur refresh & kuota, `HomePlaces`/`GoogleCardPhoto` untuk foto, `TrackingStarter`/`DriveTracking` untuk rute, `ScheduleReminder`/`ReminderEvents`/`RestSheet` untuk pengingat, `BogorConditions` untuk PM2.5, `DevSimulation` ada di source set debug/release. Build Google memakai `-PSAHAYA_USE_LOCAL_MAPS_KEY=true -PSAHAYA_PLACES_ENABLED=true`; key tidak pernah dicatat.
- **Batas yang perlu diingat:** 50 adalah batas upaya aplikasi per instalasi, bukan batas tagihan proyek. Jarak Places adalah garis lurus dari titik request terakhir, bukan jarak rute. Pengingat panas/hujan memakai BMKG dan jadwal aktif; Mode Dev menggunakan data sintetis. Vercel hanya untuk APK, bukan backend.

## Catatan versi sebelumnya

- **0.4.4 Google · 23 November 2026:** Maps dan Places berfungsi di emulator, cuaca BMKG. Source checkpoint `8f3da36` lulus build debug, lint, 57 tes unit Android dan 6 tes backend. Tidak identik dengan APK publik; perubahan UI dan penyegaran lokasi belum diuji menyeluruh di HP.
- **Versi sebelumnya:** arsip APK cukup di [halaman unduhan](https://sahaya-test-download.vercel.app/). Tidak perlu catatan atau folder desain per versi.

## Alur tiap iterasi

Perbarui catatan Obsidian yang sudah ada: apa yang berubah, bukti tes, apa yang belum, dan referensi build. Gunakan satu desain aktif; ganti acuan lama alih-alih menambah duplikat. Commit dan push ke **`main`** di GitHub; verifikasi SHA. Dokumentasi publik adalah salinan tersaring dari Obsidian, bukan sinkronisasi otomatis. Jangan publikasikan key, rute, konfigurasi privat, atau data pribadi. Publikasikan APK yang sudah diverifikasi hanya lewat halaman unduhan yang sama.
