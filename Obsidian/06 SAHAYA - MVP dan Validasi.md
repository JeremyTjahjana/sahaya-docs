# SAHAYA — MVP dan Validasi

[← Beranda](00%20Mulai%20di%20Sini.md) · [Brief tim](05%20SAHAYA%20-%20Brief%20Tim.md) · [Evaluasi](07%20SAHAYA%20-%20Evaluasi%20Ide.md) · [Mockup UI](Desain/01%20Desain%20UI.md)

> **Status: rancangan MVP rekomendasi, belum implementasi.** Dokumentasi/mockup diizinkan pengguna. APK, backend, pengujian perangkat, dan deployment belum dibuat atau diverifikasi. Tracker di bawah diperbarui manual.

## Tujuan MVP
Membuktikan satu alur: **siap bekerja → memantau sesi → mengevaluasi jeda → memilih tempat → mengonfirmasi jeda/berkontribusi.** Bukan membuktikan penurunan penyakit atau kecelakaan dalam demo singkat.

## Ruang lingkup dan penerimaan
| Prioritas | Fitur | Syarat penerimaan yang harus dibuktikan |
|---|---|---|
| P0 | Personalisasi | Hari, jam, area, dan pilihan pengingat tersimpan, dapat dilewati/diubah; perubahan jadwal hari ini mengalahkan jadwal rutin |
| P0 | Persetujuan dan izin | Tujuan pemantauan dijelaskan; penolakan izin tidak memunculkan klaim tracking aktif; pencarian area manual tetap tersedia |
| P0 | Mulai/selesai sesi | Ada indikator dan notifikasi pemantauan; selesai sesi menghentikan pekerjaan lokasi yang terkait sesi |
| P0 | Estimasi gerak/berhenti | Durasi sesi, bergerak, berhenti, dan jeda tidak tertukar; ada status tidak diketahui saat data tidak memadai |
| P0 | Jeda terkonfirmasi | Menunggu order tidak otomatis mereset waktu jeda; pengguna dapat mengonfirmasi/mengoreksi |
| P0 | Daftar/peta tempat rehat | Kandidat vs terkonfirmasi jelas; atribut tidak diketahui tidak diubah menjadi tersedia; bisa membuka navigasi eksternal |
| P0 | Kontribusi kandidat | Pilih/koreksi lokasi, kategori dan fasilitas, setujui pembagian tempat umum; laporan ulang tidak menambah konfirmasi independen |
| P0 | Persiapan cuaca | Area/waktu acuan, sumber dan waktu pembaruan terlihat; fallback jujur jika jaringan/API gagal |
| P1 | Pengingat berhenti lama | Ajakan kontribusi hanya pada kondisi yang layak, bisa dilewati, ada jeda notifikasi; durasi/radius belum final |
| P1 | Kurasi dan pelaporan perubahan | Tempat tutup/salah/privat bisa ditandai; konflik informasi tidak hilang diam-diam |
| Lanjutan | Polusi dan gangguan jalan | Masuk setelah sumber, cakupan, batas akses dan pembaruan dibuktikan; bukan syarat inti MVP |

P0 merupakan baseline asisten yang diajukan untuk diskusi. Jika waktu tidak cukup, pilih pengurangan ruang lingkup secara eksplisit; jangan menyebut fitur belum berjalan sebagai sudah selesai.

## Baseline teknis yang direkomendasikan
- Aplikasi Android, dimulai pengguna ketika layar aplikasi terlihat; foreground service lokasi dengan notifikasi sesuai izin dan versi Android. Jangan mengasumsikan bebas memulai dari background.[14]
- Activity Recognition dan lokasi adaptif sebagai kandidat pendekatan; uji deteksi saat naik motor, jangan menganggap label kendaraan sudah sama dengan sesi narik.[15][16]
- Untuk tempat belum dikenal, analisis periode berhenti dan minta konfirmasi titik. Geofence memantau area yang sudah ditentukan, bukan otomatis menemukan nama warung; event dapat terlambat.[13]
- Simpan sesi pribadi seminimal mungkin; database bersama hanya berisi kontribusi tempat yang disetujui dan bukti secukupnya. Retensi, akses dan penghapusan harus diputuskan sebelum pilot nyata.
- Data awal tempat dikurasi pada wilayah pilot. Nama/tempat contoh tidak boleh dipasarkan sebagai survei nyata.
- Backend, framework, autentikasi, provider peta, anggaran dan distribusi APK **belum dipilih**.

## Model status
**Sesi:** belum mulai → aktif → dugaan berhenti → menunggu/jeda terkonfirmasi → aktif → selesai. Kondisi izin/lokasi tidak memadai ditampilkan sebagai terhenti/tidak diketahui, bukan terus mengarang estimasi.

**Tempat:** kandidat → dikonfirmasi komunitas → perlu diperiksa ulang/diarsipkan bila relevan. Status tempat dan setiap fasilitas berbeda. Visibilitas kandidat sebelum ambang terpenuhi masih keputusan terbuka.

## Aturan keselamatan penggunaan
Interaksi detail dan kontribusi dilakukan setelah berhenti aman. Tidak ada tugas mengetik wajib saat berkendara. Lokasi pelanggan/rumah tidak otomatis dibagikan; komunitas tidak melihat posisi langsung driver. Izin ditolak dan notifikasi dimatikan ditangani tanpa menghukum pengguna. Pemantauan tidak diklaim tak bisa dihentikan sistem atau pengguna.

## Urutan pekerjaan usulan
1. Wawancara singkat dengan driver yang dapat diakses pengguna; periksa masalah jeda, aplikasi tambahan, dan kesediaan izin/baterai.
2. Spike Android di HP nyata: mulai sesi, layar mati, buka aplikasi lain, berhenti, lanjut dan selesai; catat yang benar-benar bekerja.
3. Pilih wilayah, kurasi fasilitas awal, dan tentukan proses koreksi tempat.
4. Bangun satu alur P0 dengan data nyata yang diizinkan; pisahkan mode contoh jika diperlukan.
5. Uji pemahaman dan tugas driver, baterai, izin/jaringan, serta kesalahan estimasi.
6. Perbaiki masalah material, kemas APK/demo, proposal dan video sesuai [03 Checklist Keperluan](03%20Checklist%20Keperluan.md).

Tanggal target internal: [04 Deadline](04%20Deadline.md). Jangan mengubah hasil spike menjadi klaim rilis sebelum tes penerimaan lolos.

## Rencana validasi
| Yang diuji | Metode | Bukti yang dicatat |
|---|---|---|
| Masalah relevan | Wawancara tentang kejadian nyata, bukan hanya “mau pakai?” | Catatan anonim, kutipan dengan izin, hambatan yang berulang |
| Tempat membantu | Tugas mencari tempat dengan fasilitas tertentu | Tugas berhasil/gagal, waktu aktual, informasi yang keliru |
| Pengingat diterima | Tinjau skenario sebelum kerja dan saat berhenti | Relevansi, gangguan, pilihan mematikan/mengubah |
| Deteksi cukup berguna | Bandingkan catatan observasi perjalanan aman dengan log aplikasi | Salah deteksi bergerak/berhenti, keterlambatan, periode tak diketahui |
| Baterai dan ketahanan | Perangkat/OS dan durasi tes dicatat; bandingkan kondisi setara | Konsumsi terukur, putusnya pemantauan, izin yang dibutuhkan |
| Kontribusi dipercaya | Duplikat, kunjungan berulang, akun berbeda dan konflik fasilitas | Hitungan independen, deduplikasi, audit koreksi |
| Privasi dipahami | Minta pengguna menjelaskan data yang dibagikan | Persetujuan yang dipahami, titik privat tidak dipublikasikan |

Jumlah peserta, ambang keberhasilan, dan batas baterai ditetapkan sebelum pilot setelah sumber daya tim jelas. Tidak ada hasil, persentase manfaat, atau batas medis yang sudah tersedia.

## Tracker manual
- [ ] Konfirmasi platform, wilayah dan anggota tim — bukti: keputusan tercatat.
- [ ] Wawancara driver — bukti: catatan anonim dan persetujuan relevan.
- [ ] Buktikan background tracking — bukti: perangkat/OS, rekaman/log dan batasnya.
- [ ] Tetapkan ambang jeda dan aturan kandidat — bukti: alasan dan kasus uji, bukan keputusan tersirat dari mockup.
- [ ] Kurasi tempat awal — bukti: asal data dan tanggal pemeriksaan fasilitas.
- [ ] Implementasikan dan uji alur P0 — bukti: build dan catatan tes penerimaan.
- [ ] Siapkan submission — bukti: checklist resmi dan status portal.

## Keputusan terbuka
| Keputusan | Status saat ini |
|---|---|
| Android/mobile dan framework | Rekomendasi teknis, belum keputusan final |
| Memulai otomatis atau tombol Mulai Kerja | Tombol manual baseline rekomendasi; belum diputuskan |
| Wilayah pilot | Belum dipilih; Bogor hanya ilustrasi mockup |
| Kandidat langsung terlihat atau tersembunyi | Belum diputuskan |
| Ambang laporan tempat | Usulan pengguna “lebih misal dari 5 kali/5 driver berbeda atau driver yang sudah mengisi 2 kali”; belum diformalkan |
| Durasi/radius berhenti dan pengingat jeda | Perlu pengujian; bukan batas diagnosis |
| Masa simpan dan penghapusan lokasi | Belum ditetapkan |
| Polusi/jalan dan anggaran layanan | Sumber operasional, cakupan, lisensi, biaya belum dibuktikan |

## Riwayat dan otorisasi
21 November 2026: pengguna mengizinkan pencatatan evaluasi/MVP, pengisian tab Google Docs yang diberikan, serta pembuatan gambar UI hijau terinspirasi referensi Gojek. Publikasi dokumentasi public di GitHub kemudian diizinkan pengguna. Ini tidak mencakup rilis aplikasi, pembelian API, akses data platform ojol, atau klaim telah menguji aplikasi.

## Hasil dokumentasi dan desain
Brief dan ringkasan Google Docs telah dibuat. Lima layar mockup (personalisasi, persiapan, sesi aktif, tempat rehat, kontribusi) tersedia bersama papan ringkasan. Sumber render dan laporan pemeriksaan tetap berada di workspace lokal. Pemeriksaan lokal memvalidasi PNG/SVG, hash aset, serta tautan dan embed Obsidian. Ini bukti penyelesaian artefak statis saja; checklist implementasi, tes perangkat dan validasi driver tetap belum dicentang.

## Sources

[13] https://developer.android.com/develop/sensors-and-location/location/geofencing
[14] https://developer.android.com/develop/background-work/services/fgs/restrictions-bg-start
[15] https://developer.android.com/develop/sensors-and-location/location/battery/scenarios
[16] https://developer.android.com/codelabs/activity-recognition-transition
