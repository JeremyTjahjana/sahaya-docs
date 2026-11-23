# Fitur dan API

[Beranda](00%20SAHAYA.md) · [Alur dan UX](02%20Alur%20dan%20UX.md) · [Rencana uji](04%20Rencana%20Kerja.md)

## Sasaran produk

Driver ojol sering perlu memilih kapan berhenti dan di mana bisa rehat tanpa membuang waktu mencari. SAHAYA memberi informasi praktis sebelum dan selama shift: kondisi sekitar, durasi kerja yang tercatat, serta jarak, harga dan fasilitas tempat rehat jika tersedia. Kontribusinya ke SDG 3 adalah membantu driver menyiapkan kerja dan mengambil keputusan rehat, bukan mendeteksi kelelahan, mengukur dampak kesehatan, atau menjanjikan kenaikan pendapatan.

Pilot pertama mencakup **Kota Bogor, WIB**. Cakupan, zona waktu dan penyedia data mengikuti konfigurasi wilayah; berita Kota Bogor tidak otomatis mencakup Kabupaten Bogor. Driver bisa memakai fitur dasar tanpa akun dan tanpa ikut komunitas.

## Cakupan MVP dan bukti yang tersedia

Kolom tengah merujuk pada bukti 0.4.6 yang sudah ada; kolom kanan adalah syarat produk, bukan daftar fitur yang dinyatakan selesai. Rincian pengujian ada di [rencana kerja](04%20Rencana%20Kerja.md#pemeriksaan-f01f08).

| ID / fitur | Tercatat pada 0.4.6 Google | Target dan yang masih perlu bukti |
|---|---|---|
| F01 Personalisasi | Pengaturan profil, jadwal dan pengingat; Mode Dev pada build debug. | Hari, jam, area biasa narik dan pengingat dapat diubah; onboarding bisa dilewati. Izin punya penjelasan dan aksi masing-masing, juga bisa diatur ulang dari Pengaturan. |
| F02 Sesi dan riwayat | Satu switch pencatatan; GPS, riwayat harian lokal, durasi dan rute. Switch dan simulasi pernah diuji di emulator. | Sesi otomatis dalam jadwal saat ada sinyal kendaraan yang segar dan izin tersedia; gunakan ketukan notifikasi jika Android membatasi mulai di latar. Buktikan perjalanan, buka ulang dan hapus data di HP. Jangan janjikan mulai tepat jam atau pulih setelah force-stop. |
| F03 Pengingat persiapan dan rehat | Mode Dev pernah memicu notifikasi panas, hujan dan panel rehat; ini bukan bukti alarm terjadwal atau perjalanan nyata. | Persiapan shift memakai jadwal dan prakiraan BMKG yang layak. Pengingat rehat didasarkan pada durasi kerja tercatat, bukan deteksi lelah; berhenti tidak otomatis dicatat sebagai rehat. Variasi teks dan emoji direncanakan untuk 0.4.7. |
| F04 Ajakan tambah tempat | Ada dasar kontribusi lokal dan panel rehat; ajakan 5 menit bukan bukti 0.4.6. | Setelah 5 menit berhenti yang memenuhi syarat, tawarkan **Tandai tempat** atau **Bukan**. Ajakan ini terpisah dari pengingat durasi kerja dan tidak menyatakan tempat belum ada di Google. |
| F05 Maps dan Places | Peta Google tertanam dan hasil Places nyata tampil di emulator; foto asli dan kredit pada kartu teramati, serta refresh setelah tarik-turun dengan GPS segar. Detail dan urutan pernah diuji pada checkpoint Google sebelumnya. | Buktikan pada APK target dan HP: peta nyata, kategori dan urutan, serta detail dengan foto, ulasan, dan harga asli dari Places. Tautan eksternal dan peta cadangan tidak memenuhi syarat ini. |
| F06 Kontribusi dan konfirmasi | Form menyimpan kontribusi dan foto lokal. Login Google dan Firestore belum dipakai APK 0.4.6. | 0.4.7 menyediakan draf lokal dari kedua jalur. Pengajuan dengan akun Google dan konfirmasi oleh driver pilot aktif disiapkan di varian privat; publikasi hanya setelah lima konfirmasi sah. |
| F07 Dashboard | PM2.5 regional dan harga BBM terlihat di emulator. Prakiraan BMKG belum tampil pada sesi 0.4.6, meski endpoint menjawab dari host. | Rata-rata durasi kerja, cuaca, kualitas udara, berita lokal dan harga BBM. **Berita dan BBM wajib diperbarui otomatis**; tombol muat ulang bukan pengganti. Buktikan sumber, cakupan, waktu terbit/berlaku dan waktu ambil, serta kondisi data lama. |
| F08 Kendali data dan pemulihan | Pencatatan bisa dimatikan, rute lokal bisa dihapus, dan pencarian Places meminta persetujuan tersendiri. | Uji penolakan/pencabutan izin, GPS belum siap, offline, penyedia gagal, data usang, serta kirim ulang yang tidak menggandakan data. Pisahkan data nyata dan Mode Dev. |

## Sumber data dan batas biaya

- **Google Maps SDK for Android** merender peta; **Places API (New) / Places UI Kit** menyediakan hasil dan detail. Pakai foto/ulasan/rating dari tempat yang tepat dan pertahankan atribusi. Jika tersedia, tampilkan rentang harga asli; jika hanya ada *price level*, tampilkan sebagai tingkat harga tanpa menebak rupiah. Untuk urutan termurah, pakai rentang nominal yang dapat dibandingkan; tempat tanpa harga tetap terlihat dan ditandai. Pisahkan informasi Google, draf lokal, dan kontribusi komunitas.
- **BMKG** untuk prakiraan dan persiapan shift (acuan pilot: Paledang, Bogor Tengah). Jika prakiraan tidak tersedia atau usang, jangan memberi notifikasi spesifik panas/hujan seolah data masih terbaru. **Open-Meteo/CAMS Global** untuk estimasi PM2.5 regional di titik tetap Bogor, tanpa GPS driver. Ini bukan sensor per jalan, AQI atau ISPU resmi. Google Weather dan Google Air Quality tidak dipakai di 0.4.6.
- **Berita dan BBM:** sumber otomatis, izin penggunaan, dan cakupannya harus dicek. Simpan hasil valid terakhir dengan label *data lama* ketika pembaruan gagal; jika belum pernah ada hasil valid, tampilkan *belum tersedia*. Jangan isi angka atau berita contoh dalam mode nyata. Usulan definisi rata-rata: total durasi kerja tercatat dibagi jumlah hari dengan catatan dalam rentang yang ditampilkan; jika belum ada hari tercatat, jangan tampilkan angka nol sebagai hasil pengukuran.
- **Batas pilot Rp100.000/bulan**, bukan persetujuan belanja. Catatan 0.4.6: Places otomatis mencari ulang setelah berpindah **lebih dari 1 km** garis lurus dari titik permintaan terakhir. Maksimal **50 upaya per 60 menit bergulir per instalasi**, termasuk detail/foto; ini bukan batas tagihan proyek. Pisahkan proyek Firebase pilot dari proyek Maps berbilling; perubahan billing, layanan berbayar atau perluasan pilot memerlukan pengecekan dan persetujuan tersendiri.

## Privasi dan komunitas

**Akun opsional (0.4.8).** Firebase Authentication menangani login Google atau email, pendaftaran dan reset sandi. Auth terpisah dari pencatatan, draf dan verifikasi tempat. Keluar tidak menghapus data lokal, dan masuk tidak menyinkronkannya. Login bukan status driver pilot.

Kotlin/Compose dengan Room untuk riwayat di HP. Izin GPS bukan persetujuan menyimpan rute. Penyimpanan rute bersifat opsional dan tidak mengunggah titik rute; persetujuan Places hanya membolehkan pengiriman titik pencarian yang dibulatkan. Persetujuan mengajukan pin tempat umum tidak mencakup riwayat kunjungan, alamat pelanggan, atau lokasi pribadi. Mode Dev tidak menulis rute nyata dan tidak menggunakan kuota Places.

**Kontrak komunitas (varian pilot privat):** sesi Google diperlukan untuk **Ajukan tempat** atau **Konfirmasi**. Tim mencocokkan akun dengan peserta secara offline tanpa unggahan identitas sensitif; admin tepercaya menetapkan `pilotDrivers/{uid}` dengan `active: true`. Akun Google sendiri bukan bukti status driver. Draf dan fotonya tetap di HP. Pengiriman eksplisit hanya membawa data tempat umum yang ditinjau driver (nama, pin, kategori, fasilitas, harga dan catatan opsional); jangan unggah foto, rute, atau identitas ke data publik.

Kandidat **Menunggu konfirmasi** hanya terlihat oleh pengusul dan driver pilot aktif lewat menu Verifikasi. Undangan per kandidat dan pembatasan kedekatan belum diterapkan; jangan pakai riwayat rute untuk menilai kedekatan. **Lima driver pilot aktif yang berbeda selain pengusul** harus mengonfirmasi. Satu UID hanya dihitung sekali, jadi perlu minimal **enam peserta aktif** untuk satu usulan jika pengusul juga driver pilot. Setelah konfirmasi kelima sah, backend menerbitkan data tempat melalui satu transaksi; sebelum itu tempat tidak masuk hasil publik. Publik melihat tempatnya, bukan UID, nama akun, email, atau daftar pemilih. Status tempat publik tidak berarti semua fasilitasnya terverifikasi; tampilkan status fasilitas yang memang punya bukti dan biarkan sisanya belum diketahui.
