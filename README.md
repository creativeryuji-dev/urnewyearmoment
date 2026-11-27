# Soora New Year Photobox

Web statis (tanpa build). Customer pilih strip photobooth, tambah foto, isi nama + wish, lalu download PNG 1200x1800 (4x6 inci).
Foto TIDAK diunggah; hanya nama + wish (opsional, dengan centang persetujuan) disimpan ke Firestore.

## Ganti desain
- `logos/soora-cream.png`: logo (versi krem untuk latar gelap).
- `assets/overlay.png` (opsional): PNG transparan 1200x1800 (4x6 inci) yang digambar di atas semuanya (twibbon/frame dari tim desain). Jika file ada, otomatis dipakai.
- Warna/teks ada di bagian atas `index.html` (`O`, `C`, teks "HAPPY NEW YEAR 2027").

## Setup
1. Firebase: buat project baru (mis. `soora-newyear`), aktifkan Firestore saja (tanpa Auth/Storage). Isi `firebase-config.js`.
2. Rules: `firebase deploy --only firestore:rules` atau tempel isi `firestore.rules` di tab Rules.
3. GitHub: push semua file. Netlify: import repo, build command kosong, publish directory `.`
4. Firebase Console > Authentication > Settings > Authorized domains tidak perlu (tanpa Auth).
