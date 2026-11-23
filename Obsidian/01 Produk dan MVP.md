# Fitur dan API

[Beranda](00%20SAHAYA.md) · [Rencana](04%20Rencana%20Kerja.md)

| Fitur | Sumber | Status APK 0.4.4 Google |
|---|---|---|
| Peta dalam aplikasi | Google Maps SDK for Android | Tampil di emulator. |
| Tempat rehat | Places API (New), Places UI Kit | Hasil nyata, rating, foto dan ulasan pada detail, jika tersedia. Urutan harga/jarak diuji di emulator; belum semua filter kategori diuji langsung. |
| Cuaca | BMKG | Prakiraan Paledang, Bogor Tengah. Google Weather tidak digunakan. |
| Kualitas udara | Tidak aktif di 0.4.4 | Build lokal 0.4.5 memakai **Open-Meteo/CAMS Global** untuk PM2.5 regional di titik tetap Bogor, tanpa mengirim GPS driver. Bukan sensor per jalan atau AQI. [Dokumentasi](https://open-meteo.com/en/docs/air-quality-api) · [Syarat API nonkomersial](https://open-meteo.com/en/terms). |
| Kinerja dan pengingat | Penyimpanan lokal Android; GPS | Riwayat harian, pengingat rehat dan persiapan shift. APK publik masih memakai **Atur GPS**. Satu perjalanan penuh di HP belum terverifikasi. |
| Harga BBM dan berita | Feed terpisah | Kelengkapan pembaruan otomatis, sumber, dan penanda data lama belum terverifikasi. |

**Teknis:** Kotlin/Compose dan Room. Rute hanya disimpan di HP setelah persetujuan. Izin GPS tidak otomatis berarti persetujuan menyimpan rute atau berbagi lokasi dengan penyedia data. Di 0.4.5, hanya titik Places yang dibulatkan dan dikirim setelah persetujuan. Key Google Air Quality yang tersimpan lokal tidak dipakai oleh build ini. Firebase login belum dipakai di APK.
