# Rencana dan iterasi

[Beranda](00%20SAHAYA.md) · [Produk dan MVP](01%20Produk%20dan%20MVP.md) · [Desain UI](02%20Alur%20dan%20UX.md) · [Keperluan lomba](05%20Keperluan%20Lomba.md)

## Target 0.4.7

**0.4.7 Google: lulus pengujian emulator.** Varian publik mendukung kontribusi lokal; modul online dibangun terpisah dan belum diaktifkan pada varian publik.

1. **UI dan draf lokal (F03, F04, F06).** Kedua pintu masuk tambah tempat memakai satu form, satu model draf dan satu aturan snapshot. Tambah variasi notifikasi panas/hujan/rehat dan samakan latar header Kinerja dengan halaman. Uji sebelum menambah ketergantungan login.
2. **Pilot tertutup (F06, F08).** Verifikasi varian Google Auth, daftarkan akun pilot melalui admin, lalu uji akses privat dan transaksi publikasi dengan enam UID uji (satu pengusul, lima pengonfirmasi). Jangan aktifkan pengiriman ke komunitas sebelum aturan akses, idempotensi, dan data yang boleh tampil publik lulus uji.
3. **Cek regresi dan data nyata (F01–F08).** Uji build target di emulator dan satu perjalanan di HP fisik, termasuk background, catat/buka/hapus, pengingat, kategori/urutan Places dan detail nyata. Pulihkan prakiraan BMKG di aplikasi dan buktikan dua feed otomatis (berita dan BBM) secara terpisah. Fitur lokal tetap dapat dipakai tanpa akun atau saat layanan komunitas belum siap.

## Pemeriksaan F01–F08

| ID | Bukti yang perlu dikumpulkan |
|---|---|
| F01 | Selesaikan dan lewati onboarding. Tolak setiap izin secara terpisah, pulihkan lewat Pengaturan, lalu cek status saat kembali. Ubah jam/hari kerja dan pastikan preferensi baru dipakai. |
| F02 | Di HP: aktifkan pencatatan dengan persetujuan, mulai sesi di dalam jadwal dengan sinyal segar, dan uji jalur notifikasi bila mulai di latar dibatasi. Rekam satu perjalanan, buka lagi, hapus satu hari tanpa menghapus hari lain; cek pemisahan tengah malam WIB, retensi, dan jeda GPS tidak menambah jarak. Tanpa opt-in, tidak ada rute yang disimpan. |
| F03 | Tampilkan variasi panas, hujan, dan rehat dengan emoji dan ikon SAHAYA; satu pengingat per kejadian, tanpa klaim deteksi lelah. Prakiraan usang tidak memicu teks cuaca spesifik. Uji jadwal nyata, panel bawah dan notifikasi sistem pengingat durasi kerja; menutup panel tidak mencatat rehat. |
| F04 | Uji 4:59 dan 5:00 setelah perjalanan dengan fix layak. **Bukan** tidak menyimpan atau mengulangi ajakan di pemberhentian itu; **Tandai tempat** membuka form langsung. Gerak ulang dan jeda GPS membatalkan hitungan; ajakan tidak menggantikan pengingat 3 jam kerja tercatat. |
| F05 | APK target menampilkan jalan/landmark Google dan hasil Places nyata. Uji semua kategori, urutan harga/jarak, kamera otomatis, tarik-turun dan batas kuota. Buka detail satu tempat dengan foto, ulasan dan harga asli, serta satu listing yang datanya tidak lengkap. |
| F06 | Uji masuk dari Maps dan dari ajakan 5 menit. Keduanya menyimpan draf lokal dengan snapshot yang tidak bergeser saat GPS berubah; pin baru berlaku hanya setelah dipilih. Tanpa jaringan atau setelah login dibatalkan, draf/foto tetap ada. Jalankan matriks konfirmasi di runbook. |
| F07 | Prakiraan BMKG, PM2.5 dan ringkasan kerja tampil dengan sumber/area dan keadaan tanpa riwayat yang benar. Amati masing-masing feed berita dan BBM berubah tanpa tarik-turun; catat waktu terbit/berlaku, waktu ambil, dan hasil simulasi gagal dengan/tanpa data valid sebelumnya. |
| F08 | Cabut izin saat sesi aktif; status tidak boleh tampak normal. Uji gangguan jaringan, retry tanpa duplikat, data contoh, dan hapus riwayat. Cek lalu lintas atau log tersaring: tidak ada rute, foto draf, atau data identitas yang terkirim ke feed publik. |

## Runbook Firebase pilot

**Target:** `sahaya-pilot`, Firestore `(default)` dalam Production mode, Spark, terpisah dari proyek Maps berbilling. Konfigurasi APK pilot privat tersedia dan rules telah lulus di emulator. Akses admin Firebase Console belum tersedia dalam sesi ini; aturan cloud belum dipublikasikan atau dibaca balik.

1. **Periksa konfigurasi.** Operator mencocokkan ID proyek, lokasi database dan status Spark. Periksa provider Google aktif serta package/SHA-1 dari **APK yang akan diuji** (varian debug memakai `id.sahaya.app.test`). Konfigurasi Android yang sesuai tetap lokal dan tidak dicetak. Console siap tidak sama dengan login berhasil. Acuan: [Google Sign-In di Android](https://firebase.google.com/docs/auth/android/google-signin).
2. **Daftarkan peserta.** Setelah identitas peserta dicocokkan offline dan UID berasal dari login peserta yang benar, admin tepercaya membuat `pilotDrivers/{uid}` dengan `active: true`; gunakan `active: false` untuk mencabut akses pilot. Klien tidak dapat mengubah/mendaftar sendiri atau membaca roster pengguna lain. Jangan simpan dokumen identitas atau email pada roster yang dipakai aplikasi.
3. **Tutup akses secara default.** Rules menolak akses yang tidak diizinkan. `restProposals` bisa dibaca pengusul atau akun pilot aktif; tidak ada undangan per kandidat pada versi ini. Akun Google bisa membuat usulannya sendiri. Hanya akun pilot aktif dengan sesi Google yang bisa menambah konfirmasi miliknya, bukan atas nama orang lain atau untuk usulannya sendiri. Pada konfirmasi kelima, satu transaksi menulis `publicRestPlaces` yang hanya memuat data tempat, tanpa data akun/pemilih.
4. **Jalankan suite lokal.** `npm ci --prefix services/firestore`, lalu dengan emulator Firestore terpisah jalankan `FIRESTORE_EMULATOR_HOST=127.0.0.1:8080 npm test --prefix services/firestore`. Suite memakai proyek demo, bukan cloud asli. Emulator membuktikan usulan belum publik sebelum lima suara, suara duplikat ditolak, dan konfirmasi kelima harus memublikasikan data yang tepat dalam transaksi yang sama. Acuan: [Uji Rules dengan emulator](https://firebase.google.com/docs/firestore/security/test-rules-emulator) · [Transaksi Firestore](https://firebase.google.com/docs/firestore/manage-data/transactions).
5. **Validasi setelah izin terpisah.** Operator berwenang membandingkan aturan yang disetujui dengan Rules pada `sahaya-pilot`, baru menerapkannya jika disetujui. Baca kembali aturan yang aktif dan jalankan smoke test positif/negatif dengan data uji dan APK target. Catat versi aturan, jenis perangkat, hasil dan batas tes tanpa token, kredensial, UID peserta atau lokasi privat. Jika salah proyek, Rules berbeda, akses bocor, atau publikasi prematur, hentikan pengiriman/konfirmasi dan kembalikan ke akses tertutup yang sudah disetujui; pertahankan draf lokal. Emulator tidak membuktikan sign-in Google nyata, konfigurasi cloud atau kapasitas backend.

## Ukuran keberhasilan pilot

Gunakan catatan sesi uji tanpa histori lokasi atau identitas. Angka hasil belum diisi; pisahkan skenario yang lulus, gagal, dan belum diuji.

| Yang ingin diketahui | Cara mengukur / syarat lanjut |
|---|---|
| Persiapan shift dan rehat membantu tanpa mengganggu | Catat pengingat yang seharusnya dan benar-benar muncul, keterlambatan, duplikat dan pemicu keliru; tanyakan apakah pesan jelas. Lanjut jika kedua alur bekerja di HP dan tidak mengambil layar penuh saat berkendara. Ini bukan ukuran berkurangnya kelelahan. |
| Driver bisa mencatat kerja dan menemukan tempat | Catat keberhasilan dan waktu untuk membuka riwayat serta menemukan tempat menurut jarak/harga. Lanjut jika perjalanan fisik dapat dibuka dan dihapus kembali, dan detail Places nyata dapat dibuka di aplikasi. |
| Kondisi lokal bisa dipercaya | Catat waktu sumber dan waktu ambil untuk tiap feed, hasil pembaruan tanpa interaksi, serta tampilan saat gagal. Lanjut jika kedua feed otomatis dan data usang ditandai; catat BMKG secara terpisah sebagai cakupan cuaca. |
| Kontribusi berguna tanpa membuka data pribadi | Catat jumlah usaha yang sukses/gagal, suara sah per kandidat, waktu sampai publik, dan hasil uji akses. Tahan pilot komunitas jika peserta aktif kurang dari enam, kandidat terlihat sebelum lima suara berbeda, atau ada data privat yang bocor. |
| Biaya pilot terkendali | Catat jumlah upaya API, layanan yang digunakan dan penggunaan/biaya proyek yang bisa diperiksa. Jangan perluas pilot sebelum estimasi masuk Rp100.000/bulan dan setiap perubahan berbayar disetujui. |

## Log penting — 0.4.7 Google

- **Source:** `sahaya-android/main` (`a44627b`). Varian Google publik: `id.sahaya.app.test`, `versionCode=12`, Android 8.0+, Firebase pilot nonaktif. SHA-256 `c58099263f34a82bf656dee4c929fddd33d38e261052d936488bb7e983e01357`.
- **Bukti:** 65 tes unit, runner Android `OK (23 tests)` dengan satu tes khusus tanpa key dilewati, lint 0 error (54 warning di varian publik). Google Maps merender jalan pada pemilih pin; berhasil menyimpan draf tanpa izin GPS, harga atau login. Header Kinerja cocok dengan latar halaman. Tes notifikasi simulasi memeriksa aksi Bukan dan snapshot titik setelah bergerak.
- **Pilot:** 18 tes rules emulator lulus. Belum ada penerbitan aturan ke `sahaya-pilot`, login Google nyata, atau tes konfirmasi lintas HP. Foto dan histori tetap di HP.

## Log penting — 0.4.6 Google

- **Status:** build uji 0.4.6 tayang di Vercel. Unduhan tanpa login identik dengan APK QA; 0.4.5 masih tersedia di arsip. Source: `sahaya-android/main` (`fa3a15d`). Paket `id.sahaya.app.test`, `versionCode=11`. APK SHA-256 `52979bad70417247b4b0e55cbb496b0bf06a604226aa7e787b9b3f1020f4a9a5`.
- **Audit foto:** ketika visibilitas menjadi key efek, scroll dapat membatalkan permintaan yang telanjur ditandai sudah dicoba. Kini hanya mulai saat thumbnail terlihat; scroll biasa tidak membatalkan unduhan yang berjalan. Maksimal dua upaya per efek, tetap tunduk kuota. Foto asli dan kredit tampak di emulator; kartu tanpa foto tampil dengan ilustrasi generik.
- **Kondisi:** tidak mengulang jam/area pada kartu cuaca. Angka PM2.5 dibulatkan untuk tampilan; band dihitung dari nilai asli: ≤15,5 / >15,5–55,4 / >55,4 µg/m³. Ini band internal untuk estimasi per jam, bukan ISPU resmi. Panduan menjelaskan pengurangan paparan dan respirator yang pas; atribusi [Open-Meteo/CAMS](https://open-meteo.com/en/docs/air-quality-api) tetap ada di panduan.
- **Pengujian:** 62 tes unit, runner Google `OK (21 tests)` dengan satu kasus keyless dilewati, lint 0 error (47 warning). Emulator memverifikasi refresh Places setelah tarik-turun dan fix segar, serta tombol khusus BBM. PM2.5 dan harga tampil; prakiraan BMKG di app masih belum tersedia pada sesi ini, meski endpoint menjawab HTTP 200 dari host. Belum dites di HP fisik.

## Log penting — 0.4.5 Google

- **Status:** dibangun lokal dan diuji di emulator Google APIs Android 28. `versionCode=10`, `id.sahaya.app.test`, Android 8.0+, tanda tangan debug sama dengan APK sebelumnya. Diterbitkan di Vercel pada 23 November 2026. Unduhan tanpa login lolos verifikasi byte-for-byte; 0.4.4 Google masih tersedia di arsip. Source diverifikasi di `sahaya-android/main` (`4a7fd93`).
- **Hasil:** build debug dan release unsigned lulus; 60 tes unit, 0 lint error (47 warning). Runner Google melaporkan `OK (21 tests)` dengan satu tes khusus varian tanpa key dilewati. Foto asli Resto Raasaa dengan kredit terlihat di kartu. GPS emulator berpindah lebih dari 1 km, kamera dan daftar diperbarui; kuota jam berjalan diuji otomatis. Switch menghidupkan/mematikan foreground service. Tiga notifikasi Dev dan panel rehat dicoba di emulator; perjalanan dan alarm terjadwal belum diuji di HP fisik.
- **Artefak lokal:** `app/build/outputs/apk/debug/app-debug.apk`, SHA-256 `e07422414b9d45be66114edef5101b9fc0a86264d87c2daa4e7b2cdf0bcd3585`. Identik dengan APK 0.4.5 saat rilis, yang kini tersedia di arsip.
- **Mulai iterasi berikutnya:** baca catatan ini dahulu; checkout aktif `sahaya-google-migration`, langsung di `main`. `NearbyUiState`/`RollingProviderLimit` mengatur refresh & kuota, `HomePlaces`/`GoogleCardPhoto` untuk foto, `TrackingStarter`/`DriveTracking` untuk rute, `ScheduleReminder`/`ReminderEvents`/`RestSheet` untuk pengingat, `BogorConditions` untuk PM2.5, `DevSimulation` ada di source set debug/release. Build Google memakai `-PSAHAYA_USE_LOCAL_MAPS_KEY=true -PSAHAYA_PLACES_ENABLED=true`; key tidak pernah dicatat.
- **Batas yang perlu diingat:** 50 adalah batas upaya aplikasi per instalasi, bukan batas tagihan proyek. Jarak Places adalah garis lurus dari titik request terakhir, bukan jarak rute. Pengingat panas/hujan memakai BMKG dan jadwal aktif; Mode Dev menggunakan data sintetis. Vercel hanya untuk APK, bukan backend.

## Catatan versi sebelumnya

- **0.4.4 Google · 23 November 2026:** Maps dan Places berfungsi di emulator, cuaca BMKG. Source checkpoint `8f3da36` lulus build debug, lint, 57 tes unit Android dan 6 tes backend. Tidak identik dengan APK publik; perubahan UI dan penyegaran lokasi belum diuji menyeluruh di HP.
- **Versi sebelumnya:** arsip APK cukup di [halaman unduhan](https://sahaya-test-download.vercel.app/). Tidak perlu catatan atau folder desain per versi.

## Alur tiap iterasi

Perbarui catatan Obsidian yang sudah ada: apa yang berubah, bukti tes, apa yang belum, dan referensi build bila ada. Gunakan satu desain aktif; push source dan ekspor tersaring ke `main`, lalu distribusikan APK lulus uji di Vercel.

Untuk iterasi build yang memang diizinkan, pisahkan checkpoint source, salinan dokumentasi publik yang tersaring, dan APK uji. Catat SHA source, versi/varian dan SHA-256 artefak yang benar-benar diuji; bila distribusi termasuk lingkupnya, periksa unduhan tanpa login dan kecocokan file sebelum memperbarui status. Jangan ganti APK publik jika verifikasi atau persetujuan gagal. Key, konfigurasi privat, rute dan identitas tidak masuk salinan publik.
