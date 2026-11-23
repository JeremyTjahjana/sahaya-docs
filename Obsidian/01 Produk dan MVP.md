# Fitur dan API

[Beranda](00%20SAHAYA.md) · [Rencana](04%20Rencana%20Kerja.md)

| Fitur | Sumber | Status APK 0.4.4 Google |
|---|---|---|
| Peta dalam aplikasi | Google Maps SDK for Android | Tampil di emulator. |
| Tempat rehat | Places API (New), Places UI Kit | Hasil nyata, rating, foto dan ulasan pada detail, jika tersedia. Urutan harga/jarak diuji di emulator; belum semua filter kategori diuji langsung. |
| Cuaca | BMKG | Prakiraan Paledang, Bogor Tengah. Google Weather tidak digunakan. |
| Kualitas udara | Google Air Quality | Belum aktif di APK. Google sudah merespons dari Linux; akses backend dan pembaruan berdasarkan lokasi belum diverifikasi di HP. |
| Kinerja dan pengingat | Penyimpanan lokal Android; GPS | Riwayat harian, pengingat rehat dan persiapan shift. APK publik masih memakai **Atur GPS**. Satu perjalanan penuh di HP belum terverifikasi. |
| Harga BBM dan berita | Feed terpisah | Kelengkapan pembaruan otomatis, sumber, dan penanda data lama belum terverifikasi. |

**Teknis:** Kotlin/Compose dan Room. Rute hanya disimpan di HP setelah persetujuan. Izin GPS tidak otomatis berarti persetujuan menyimpan rute atau berbagi lokasi dengan penyedia data. Untuk Air Quality, kirim hanya titik yang sudah dibulatkan setelah pengguna setuju; key ada di server, bukan APK. Firebase login belum dipakai di APK.
