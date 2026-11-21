# SAHAYA — Brief Tim

[← Beranda](00%20Mulai%20di%20Sini.md) · [MVP dan validasi](06%20SAHAYA%20-%20MVP%20dan%20Validasi.md) · [Evaluasi](07%20SAHAYA%20-%20Evaluasi%20Ide.md) · [Mockup UI](Desain/01%20Desain%20UI.md)

> **Status: konsep untuk didiskusikan bersama tim.** Pengguna meminta pendokumentasian dan mockup; belum ada implementasi aplikasi atau hasil uji driver. Fitur usulan dibedakan dari keputusan yang sudah dinyatakan.

## Penjelasan singkat untuk teman
SAHAYA adalah pendamping kesehatan kerja untuk driver ojek online. Aplikasi dirancang membantu driver mempersiapkan perlengkapan berdasarkan jadwal dan area kerja, memperkirakan pola bergerak/berhenti selama sesi, lalu menawarkan tempat rehat yang fasilitasnya relevan. Driver juga dapat membantu menemukan dan mengonfirmasi warung, kedai, toilet, atau tempat singgah yang belum terdaftar di SAHAYA. Fokusnya menghubungkan pengingat dengan tindakan yang bisa dilakukan, bukan hanya menambah notifikasi.

**Kalimat presentasi:** “SAHAYA membantu driver mempersiapkan kerja dan mengambil jeda, dengan memahami pola aktivitas serta menemukan tempat rehat yang dibangun bersama komunitas.”

## Tema dan sasaran
- **Lomba:** SEVENT X — Software Development.
- **Tema cabang:** Developing Sustainable Tech Solutions for Society.
- **Subtema utama:** SDG 3 — Good Health and Well-Being.
- **Sasaran utama:** driver ojol; kebutuhan yang dibahas paling dekat dengan pengendara motor. Solusi lintas platform merupakan arah usulan, tanpa menganggap ada kerja sama dengan Gojek/Grab.
- **Pengguna tambahan usulan:** pengelola/kurator tempat. Bukan syarat adanya dashboard bisnis di MVP.
- **Wilayah pilot:** belum diputuskan. Bogor pada mockup hanya contoh visual.

Kaitannya dengan SDG 3: dukungan jeda dan persiapan perjalanan berkaitan secara konseptual dengan keselamatan lalu lintas (3.6); informasi kualitas udara dengan paparan lingkungan (3.9). Target 3.4 juga membahas kesejahteraan, tetapi SAHAYA saat ini tidak memiliki intervensi kesehatan mental khusus. Keterkaitan ini bukan bukti bahwa aplikasi menurunkan kecelakaan atau penyakit.[11]

## Masalah yang ingin diuji
Hipotesis awal: driver dapat terus bekerja karena tekanan penghasilan, tidak menemukan tempat rehat yang sesuai, atau menganggap pengingat umum kurang membantu. Informasi penting bisa tersebar antara aplikasi cuaca, peta, dan pengetahuan sesama driver. Ini belum merupakan hasil wawancara; pengguna sudah mengonfirmasi memiliki akses ke driver untuk validasi.

Pertanyaan inti: **apakah pendamping yang minim input dan memberi pilihan tempat konkret membuat jeda lebih mudah dilakukan?**

## Cara kerja dari sudut pandang driver
1. **Personalisasi singkat:** hari biasa narik, rentang jam, area, dan jenis pengingat. Bisa dilewati dan diubah.
2. **Sebelum berangkat:** ringkasan persiapan dan checklist, misalnya jas hujan dan botol minum. Prakiraan untuk area/jam kerja menjadi konteks, bukan kepastian cuaca di setiap titik.[8]
3. **Mulai sesi:** tombol Mulai Kerja adalah baseline yang direkomendasikan, bukan keputusan final pengguna. Aplikasi menjelaskan izin dan pemantauan yang aktif.
4. **Selama sesi:** estimasi bergerak/berhenti dan durasi sesi; notifikasi latar belakang tetap transparan. Android direkomendasikan untuk jalur ini; mekanisme dan baterainya belum diuji di perangkat.[14][15][16]
5. **Evaluasi jeda:** pengingat mengajak driver mengecek kebutuhan istirahat. Diam tidak otomatis dianggap beristirahat; menunggu order dan lampu merah harus dibedakan melalui konfirmasi/koreksi.
6. **Cari tempat:** tampilkan tempat dengan fasilitas seperti toilet, tempat duduk, teduh, dan parkir. Status setiap atribut yang belum diketahui tetap terlihat.
7. **Kontribusi:** ketika sudah berhenti aman, driver boleh melaporkan tempat atau mengonfirmasi kandidat yang dekat. Pengguna mengoreksi titik dan memilih apakah lokasi layak dibagikan.
8. **Jeda dan selesai:** pengguna mengonfirmasi mulai/selesai jeda, kemudian mengakhiri sesi kerja dan pemantauan.

## Penemuan tempat oleh komunitas
- Lokasi berhenti merupakan petunjuk untuk bertanya, bukan bukti adanya warung.
- Laporan awal disimpan sebagai **kandidat**; masuk database berbeda dari direkomendasikan sebagai tempat terkonfirmasi.
- Gunakan status Kandidat, Dikonfirmasi Komunitas, dan Perlu Diperiksa Ulang.
- Laporan dari orang yang sama dan konfirmasi independen tidak disetarakan; akun berbeda juga belum membuktikan orang berbeda.
- Keberadaan tempat, toilet, biaya, jam buka, dan izin beristirahat dikonfirmasi secara terpisah.
- Cek kandidat sekitar dan minta pengguna memilih tempat yang sama sebelum membuat entri baru. Jangan menggabungkan warung bersebelahan hanya karena GPS berdekatan.
- Tempat privat, rumah, dan lokasi pelanggan tidak otomatis dipublikasikan. Tidak ada peta lokasi langsung driver yang terbuka ke komunitas.

**Ambang belum final:** pengguna mengusulkan “lebih misal dari 5 kali/5 driver berbeda atau driver yang sudah mengisi 2 kali”. Ini disimpan sebagai alternatif yang perlu diperjelas, bukan formula verifikasi yang sudah disetujui. Dua kunjungan pengguna sama bisa memperkaya kandidat, tetapi baseline usulan tidak menyebutnya konfirmasi independen.

## Mengapa bukan sekadar peta atau pengingat?
Pembeda yang ingin diuji adalah rangkaian **konteks kerja → ajakan jeda → tempat rehat yang sesuai → pengetahuan komunitas**. Pengingat dan fasilitas istirahat sendiri bukan hal baru: Grab telah mendokumentasikan lounge untuk driver.[12] Belum ada riset kompetitor menyeluruh yang membuktikan kombinasi SAHAYA unik.

## Prioritas produk
**MVP rekomendasi:** personalisasi ringan, sesi dengan pemantauan gerak/berhenti, persiapan cuaca, tempat rehat terkurasi, dan kontribusi kandidat. Batas teknis serta penerimaan ada di [06 SAHAYA - MVP dan Validasi](06%20SAHAYA%20-%20MVP%20dan%20Validasi.md).

**Visi lanjutan pengguna:** kualitas udara dan berita/gangguan jalan terkini. Data, cakupan, lisensi, biaya, dan pembaruannya belum dikunci; jangan ditampilkan sebagai integrasi live yang sudah ada.

**Ditunda:** prediksi pendapatan, diagnosis kelelahan, chatbot terapi, navigasi turn-by-turn sendiri, integrasi order/pendapatan platform, serta pelacakan otomatis sepanjang hari. Tekanan ekonomi tetap konteks masalah, bukan mesin optimasi penghasilan di MVP.

## Batas klaim dan status
- Pola gerak bukan pengukuran kelelahan, kesehatan mental, atau status pekerjaan yang pasti.
- Tidak menjanjikan pendapatan, keselamatan mutlak, fasilitas gratis, atau hasil kesehatan.
- Tidak perlu AI generatif untuk membuat alur inti berguna. AI bukan pembeda wajib.
- Izin ditolak, GPS tidak akurat, jaringan terputus, dan pemantauan dihentikan harus punya penanganan yang jujur.
- Mockup memakai peta, tempat, cuaca, dan angka ilustratif; bukan hasil API, lokasi, atau penggunaan nyata.

## Keputusan dan pertanyaan tim
**Dinyatakan pengguna:** ide untuk driver; background movement/stationary monitoring; rekomendasi fasilitas; kontribusi tempat; personalisasi hari/jam/area; pengingat perlengkapan/cuaca/polusi/jalan; brand hijau; gambar Gojek terlampir sebagai inspirasi visual. Akses ke driver tersedia, tetapi jadwal dan peserta belum tercatat.

**Rekomendasi asisten, belum keputusan final:** Android; mulai/selesai sesi manual; pilot satu wilayah; lokasi pribadi tetap lokal bila memungkinkan; konfirmasi komunitas independen; urutan MVP dan mockup.

**Masih terbuka:** wilayah, platform/stack final, anggota dan pembagian tugas, anggaran layanan, ambang jeda/konfirmasi, visibilitas kandidat, autentikasi, masa simpan data, serta ketersediaan sumber polusi/jalan.

## Dokumen kolaboratif

Tautan dokumen kerja tim tidak disertakan dalam salinan publik. Aturan lomba diringkas di catatan Guidebook; sumber asli tetap menjadi acuan.

## Sources

[8] https://data.bmkg.go.id/prakiraan-cuaca
[11] http://sdgs.un.org/goals/goal3
[12] https://www.grab.com/id/en/press/consumers-drivers/grab-resmikan-grabbike-lounge-pertamanya-di-jakarta-sebagai-bagian-dari-inisiatif-grabsejahtera-untuk-meningkatkan-kesejahteraan-para-mitra-pengemudi-grabbike
[14] https://developer.android.com/develop/background-work/services/fgs/restrictions-bg-start
[15] https://developer.android.com/develop/sensors-and-location/location/battery/scenarios
[16] https://developer.android.com/codelabs/activity-recognition-transition
