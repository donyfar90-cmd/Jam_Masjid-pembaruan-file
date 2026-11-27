# Smart Masjid

**Sebelum mengubah atau mengupdate aplikasi, baca [PANDUAN-UPDATE.md](PANDUAN-UPDATE.md).**

Display landscape seperti digital signage masjid dengan jam, countdown salat berikutnya, jadwal salat editable, background/slideshow foto, pengumuman, laporan/info, running text, serta embed YouTube.

## Build APK via GitHub Actions
Upload/replace semua file proyek ke repository, kemudian buka Actions dan jalankan workflow Build Android APK. Artifact bernama `JamMasjidDigital-debug-apk`.

## Panel admin lokal
Saat APK berjalan, panel setting tersedia pada `http://IP-ANDROID:8081/admin` dari perangkat lain di jaringan Wi-Fi yang sama. Upload foto background melalui panel; slideshow dan setting disimpan lokal pada perangkat Android.

YouTube embed memerlukan internet. Autoplay dibatasi oleh Android/WebView/YouTube, jadi video mungkin perlu ditekan Play.

**Catatan:** Jadwal waktu salat dalam versi ini masih manual/editable. Verifikasi dan isi jadwal resmi masjid sebelum dipakai.


**Catatan build:** workflow saat ini membuat APK debug yang otomatis ditandatangani dengan debug key Android. Tidak perlu mengisi GitHub Secrets. APK dapat diunduh dari Artifact `JamMasjid-V2-apk` pada halaman Actions.
