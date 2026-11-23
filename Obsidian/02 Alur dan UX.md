# Desain UI

[Beranda](00%20SAHAYA.md) · [Produk dan MVP](01%20Produk%20dan%20MVP.md) · [Rencana uji](04%20Rencana%20Kerja.md)

**Acuan aktif:** komposisi tata letak 0.4.3 yang dipertahankan pada 0.4.4 Google. Pertahankan ikon helm–spark, Plus Jakarta Sans, hijau `#2EC466`, mint `#8CE9AD`, aksen oranye `#F78E26`, latar `#F4F7F4` dan teks `#1A2E22`. Pakai teks gelap di atas warna terang; gunakan teks dan ikon, bukan warna saja, untuk membedakan status. Perubahan bertanda 0.4.7 di bawah ini adalah target desain, bukan bukti APK.

## Masuk dan lima tab

Splash dilanjutkan personalisasi satu pertanyaan per layar: profil, hari/jam kerja, area, dan pilihan pengingat. Langkah terakhir memisahkan izin lokasi, notifikasi, dan aktivitas fisik; tiap izin punya alasan singkat dan aksi untuk membuka prompt Android. Driver bisa melewati langkah itu dan mengulangnya dari **Pengaturan → Izin & Privasi**. Minta lokasi saat aplikasi dipakai lebih dulu; akses latar hanya ditawarkan terpisah untuk mulai otomatis. Perbarui status saat kembali dari Pengaturan. Jangan gabungkan izin dengan persetujuan simpan rute atau pencarian Places.

| Tab | Susunan dan perilaku |
|---|---|
| Beranda | Ringkasan durasi kerja dan kondisi, peta tinggi, lalu kartu tempat terdekat dengan foto asli. Jika belum ada foto, gunakan ilustrasi generik berlabel; ganti setelah foto asli termuat dan tampilkan kredit. Strip berita lokal beraksen oranye selebar layar di atas navigasi bawah hanya ketika relevan. |
| Kondisi | Judul area dan waktu sekali saja, misalnya `Paledang, Bogor Tengah · 16:29` (contoh format). Kartu cuaca tidak mengulang keduanya. Angka PM2.5 bulat, satuan tetap terbaca, kategori internal dan penjelasan/atribusi di panduan. Ikon di bawah tabel hanya menyegarkan harga BBM. |
| Kinerja | **0.4.7:** latar judul **Kinerja** sama dengan latar halaman, tanpa blok putih. Pertahankan peta lebar, tanggal dan **Riwayat** di atas peta; kartu bawah memuat status GPS, durasi kerja harian, jarak rute yang benar-benar tercatat, dan satu switch **Pencatatan**. Data dan aksi hapus mengikuti tanggal yang dipilih. |
| Maps | Fokus otomatis ke posisi driver saat GPS tersedia, tanpa tombol **Lokasi saya** dan **Kota Bogor**. Hanya tampilkan posisi driver sendiri. Filter kategori dan urutan memperbarui daftar; ketuk marker atau kartu untuk membuka detail ringkas dengan foto, harga, dan ulasan yang tersedia. **0.4.7:** sediakan aksi **Tambah tempat** yang dapat ditemukan dari Maps. |
| Pengaturan | Profil, jadwal, pengingat, izin dan privasi. Varian debug menambahkan satu switch **Mode Dev**; kontrol simulasi tidak tampil pada penggunaan biasa. |

Tarik turun dari posisi teratas Beranda, Kondisi, atau daftar tempat di Maps untuk menyegarkan data. Places tetap memerlukan persetujuan, posisi segar dan sisa kuota; BMKG mengikuti jeda permintaannya. Hilangkan teks akurasi GPS, cooldown/kuota dan instruksi berulang dari layar utama, tetapi jangan sembunyikan atribusi atau keadaan seperti **Data lama**, **Lokasi belum tersedia**, atau **Belum ada riwayat**. Data contoh harus bertanda `Contoh`, termasuk nama, titik dan angka.

## Tawaran kontribusi dan pengingat rehat

- **5 menit berhenti yang memenuhi syarat (0.4.7):** sesudah bergerak dengan posisi yang layak, berhenti terus-menerus dapat memunculkan ajakan singkat **Sudah berhenti 5 menit** di aplikasi. **Tandai tempat** langsung membuka form yang sama dengan aksi manual di Maps, tanpa layar perantara. **Bukan** tidak membuat draf, tidak mengirim apa pun, dan tidak mengulang ajakan pada pemberhentian yang sama. Gerak lagi atau kehilangan fix yang layak membatalkan hitungan; GPS yang buruk atau simulasi tidak memicu kontribusi nyata.
- **Durasi kerja:** pengingat terpisah mengajak rehat setelah 3 jam kerja tercatat, tanpa mengambil alih layar. Di aplikasi gunakan panel bawah berilustrasi, durasi jam:menit:detik, dan beberapa saran tempat jika tersedia. Di luar aplikasi gunakan notifikasi Android yang membuka panel saat diketuk, bukan layar penuh. Driver boleh tutup, memilih rehat, atau lanjut; diam atau menutup panel bukan konfirmasi istirahat. Tutup ajakan tambah tempat tanpa mematikan pengingat rehat yang diaktifkan driver.

## Form tambah tempat dan status

**Maps → Tambah tempat** dan **ajakan 5 menit → Tandai tempat** memakai form dan format draf lokal yang sama. Form membuka satu snapshot titik awal yang valid (manual: titik yang dipilih driver atau saran dari lokasi segar; ajakan: titik berhenti yang ditawarkan). Kamera/GPS yang bergerak tidak mengganti snapshot diam-diam. **Pilih pin** memungkinkan driver menempatkan atau mengoreksi titik secara sengaja lalu menyetujuinya; tanpa titik valid, minta pilih pin sebelum simpan atau ajukan. Tanyakan nama, kategori dan fasilitas; harga dan foto opsional. Nama wajib untuk pengajuan online. Tandai rumah dan alamat pelanggan sebagai lokasi yang tidak boleh diajukan.

**Simpan draf** tidak meminta login atau jaringan. **Ajukan tempat** (varian pilot privat) menampilkan pratinjau data yang akan dikirim, lalu menawarkan login Google jika diperlukan. Draf dan foto tetap di HP; membatalkan login, kehilangan jaringan atau ditolak tidak menghapus draf. Tampilkan **Draf lokal**, **Belum terkirim** atau **Menunggu konfirmasi** sesuai hasil nyata. Driver pilot aktif membuka daftar usulan privat melalui Maps → Verifikasi; hasil publik tidak menampilkan identitas pengusul atau pemilih. Rincian akses di [kontrak pilot](01%20Produk%20dan%20MVP.md#privasi-dan-komunitas).

## Notifikasi dan variasi teks

Gunakan ikon kecil SAHAYA pada notifikasi sistem, serta satu emoji yang relevan pada judul (target 0.4.7). Teks tetap jelas tanpa emoji. Pilih satu variasi per kejadian; jangan mengirim semua variasi sekaligus. Untuk panas/hujan, gunakan prakiraan yang sesuai jadwal. Untuk rehat, gunakan bahasa bersyarat: aplikasi tidak tahu apakah driver lelah. Berikut contoh teks untuk QA, bukan klaim semua salinan sudah masuk APK.

| Pemicu | Variasi A | Variasi B |
|---|---|---|
| Prakiraan panas | **☀️ Ingat minum** · Diprakirakan panas saat shift. Siapkan air minum sebelum berangkat. | **💧 Isi botol dulu** · Cuaca diprakirakan panas. Bawa air supaya mudah minum saat berhenti. |
| Prakiraan hujan | **🌧️ Bawa jas hujan** · Ada prakiraan hujan saat shift. Cek jas hujan sebelum berangkat. | **☔ Siapkan perlengkapan hujan** · Hujan mungkin turun saat kamu narik. Taruh jas hujan di tempat yang mudah dijangkau saat berhenti. |
| Ajakan rehat / rasa lelah | **😴 Mau rehat sebentar?** · Kalau mulai lelah, ambil jeda saat sudah berhenti di tempat aman. | **🛑 Cek tempat rehat** · Kalau butuh jeda, lihat pilihan tempat rehat terdekat saat aman membuka aplikasi. |

**QA debug:** **Pengaturan → Mode Dev → Kinerja** untuk joystick dan **Tes notifikasi**: **Ingat minum**, **Bawa jas hujan**, atau **Istirahat**. Uji notifikasi sistem dan panel bawah secara terpisah. Matikan Mode Dev untuk pengujian GPS, jadwal, cuaca, dan Places nyata; simulasi tidak menyimpan rute asli atau memakai kuota Places.

Aset acuan UI disimpan di vault lokal dan tidak didistribusikan di GitHub.

Acuan komposisi dari pengguna. Nama, angka, ilustrasi, dan sumber pada gambar adalah contoh, bukan bukti data live.
