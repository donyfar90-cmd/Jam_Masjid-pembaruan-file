# Panduan Update Smart Masjid (WAJIB dibaca manusia dan AI)

## Instruksi untuk asisten AI
Baca seluruh file ini sebelum mengubah proyek. Tujuan utama: update tidak boleh mengharuskan
aplikasi dihapus. Jika sebuah permintaan melanggar aturan tetap, jelaskan risikonya dan jangan lanjutkan
sebelum pemilik memahami dan menyetujuinya. Jangan meminta pemilik menempelkan isi kunci atau password ke chat.

## Kondisi
- Aplikasi LAMA: "Jam Masjid Digital V2", ID `id.jammasjid.digital`, port 8080.
  Kuncinya tidak tersimpan di GitHub Secrets.
- Aplikasi BARU: "Smart Masjid", ID `id.jammasjid.smartmasjid`, port 8081.
- Solusi sementara: keduanya terpasang berdampingan. Smart Masjid BUKAN update dari aplikasi lama.
  Pengaturan dan foto tidak pindah otomatis.
- Jika kunci asli aplikasi lama ditemukan (misalnya `.android/debug.keystore` di komputer pembuat APK),
  update langsung mungkin bisa dilakukan. Periksa sidik jarinya dulu; jangan hapus apa pun.

## Aturan tetap
1. Jangan ubah `applicationId` (`id.jammasjid.smartmasjid`).
2. Jangan ganti atau membuat ulang kunci. Alias: `smartmasjid`.
   SHA-256 sertifikat: `98:3C:94:83:B7:E0:4D:1E:6B:F5:F6:75:03:64:5A:82:05:BD:C3:D2:38:5D:47:C6:E8:E5:F9:9F:89:30:D3:5D`
3. Jangan simpan file kunci, base64, atau password di repo.
4. `versionCode` harus selalu naik. Saat ini 100 + nomor run GitHub Actions. Jika file workflow diganti
   namanya, repo dipindah, atau cara build diubah (nomor run bisa mulai dari awal), naikkan angka dasarnya
   di atas versionCode terakhir yang terpasang.
5. Jangan ubah port 8081, alamat `http://127.0.0.1:8081/`, kunci localStorage
   `jammasjid.digital.v2.settings`, atau database `JamMasjidMediaV2`. Jika diubah, pengaturan atau foto
   bisa tidak terbaca walaupun aplikasi berhasil diupdate. Perubahan format data wajib memakai migrasi.
6. Jangan hapus pemeriksaan kunci di `.github/workflows/build.yml`.

## Pemasangan pertama
1. Simpan cadangan kunci di dua tempat pribadi.
2. GitHub: Settings > Secrets and variables > Actions. Isi `KEYSTORE_BASE64` dan `KEYSTORE_PASSWORD`.
3. Unggah file proyek terbaru, lalu jalankan workflow "Build Android APK".
   Pakai hanya APK dari build yang berisi semua perubahan.
4. Pasang APK. JANGAN hapus aplikasi lama. Hasilnya harus ada dua aplikasi.
5. Isi ulang pengaturan dan pilih ulang foto di Smart Masjid.
6. Agar aplikasi lama tidak ikut terbuka: Pengaturan Android > Aplikasi > Jam Masjid Digital V2 >
   Paksa berhenti. Jangan buka lagi kecuali diperlukan. Uji dengan menyalakan ulang perangkat;
   perilaku buka otomatis bisa berbeda tiap perangkat.

## Setiap update
1. Ubah kode, commit ke `main`, tunggu build bercentang hijau.
2. Unduh artifact `JamMasjidDigital-debug-apk`.
3. Pasang di atas Smart Masjid. Android harus menawarkan UPDATE.
4. Pastikan pengaturan dan foto masih ada.

## Uji wajib sebelum dipakai di masjid
Setelah pemasangan pertama, jalankan "Run workflow" sekali lagi (run baru, bukan "Re-run"),
lalu pasang hasilnya tanpa menghapus aplikasi. Lakukan sebaiknya di perangkat cadangan atau di luar jam salat.

## Jika muncul "Aplikasi tidak terinstal"
JANGAN langsung hapus aplikasi (data akan hilang). Catat pesan errornya, lalu periksa: kunci sama
(`apksigner verify --print-certs app-debug.apk`), `applicationId` sama, `versionCode` lebih tinggi,
ruang penyimpanan cukup.
