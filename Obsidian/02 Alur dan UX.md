# Desain UI

[Beranda](00%20SAHAYA.md) · [Rencana](04%20Rencana%20Kerja.md)

**Acuan aktif:** tata letak 0.4.3 yang dipertahankan di 0.4.4 Google. Pertahankan ikon helm–spark, Plus Jakarta Sans, hijau `#2EC466`, mint `#8CE9AD`, aksen oranye `#F78E26`, latar `#F4F7F4` dan teks `#1A2E22`. Perubahan di bawah ini adalah arah iterasi, bukan klaim APK publik sudah berubah.

| Tab | Arah UI |
|---|---|
| Beranda | Ringkasan kondisi, peta lebih tinggi, dan kartu tempat dengan foto asli. Tampilkan ilustrasi berlabel saat foto belum tersedia; ganti saat foto asli berhasil dimuat. Rating/harga hanya jika ada datanya. |
| Kondisi | Tampilkan `Paledang, Bogor Tengah · 16:29` sebagai contoh format, bukan jam tetap. Kartu cuaca tanpa waktu/lokasi berulang. PM2.5 berupa bilangan bulat, satuan kecil, dan tiga kategori aplikasi; panduan hijau memuat penjelasan serta atribusi. Ikon di bawah tabel hanya memuat ulang harga BBM. |
| Kinerja | Satu switch pencatatan. Setelah pengguna setuju dan izin tersedia, mulai otomatis sesuai batas Android; tetap sediakan tanggal, riwayat, dan hapus rute. |
| Maps | Fokus dan zoom otomatis ke posisi driver saat GPS tersedia. Hapus tombol “Lokasi saya” dan “Kota Bogor”; minta izin hanya jika diperlukan. |
| Pengaturan | Profil, jadwal, pengingat, izin dan privasi; build debug menambah satu switch Mode Dev. |

**Tes di HP:** aktifkan **Pengaturan → Mode Dev**, lalu buka **Kinerja**. Gunakan joystick dan **Tes notifikasi** → **Ingat minum**, **Bawa jas hujan**, atau **Istirahat**. Yang terakhir membuka panel bawah berisi contoh tempat rehat. Matikan Mode Dev untuk tes GPS, Maps, dan Places nyata. Dev tidak menyimpan rute asli atau memakai kuota Places.

Tarik turun dari posisi teratas Beranda, Kondisi, atau daftar tempat di Maps untuk menyegarkan data. Places tetap membutuhkan izin, GPS yang segar, dan kuota; BMKG tetap mengikuti jeda permintaan.

Hilangkan teks akurasi GPS, cooldown/kuota dan instruksi berulang dari layar utama. Pertahankan persetujuan yang diperlukan, status singkat saat gagal, dan atribusi wajib peta/foto/data.
