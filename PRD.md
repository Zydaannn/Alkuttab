# PRD — Alkuttab (الكُتَّاب): Media Pembelajaran Maharah Kitabah Berbasis Game

## 1. Ringkasan Produk
- **Nama Aplikasi:** Alkuttab (الكُتَّاب)
- **Target Pengguna:** Siswa Kelas 8 (uji coba 35–40 siswa serentak melalui HP masing-masing).
- **Target Tanggal Uji Coba:** Kamis, 3 Desember 2026.
- **Materi Prototipe:** Bab 1 — Al-Hiwayah (الهواية / Hobi).
- **Tujuan:** Menggabungkan modul pembelajaran *Maharah Kitabah* terstruktur, latihan tulis interaktif, kuis pemahaman penghasil energi, dan game kompetitif tim secara *real-time* dalam satu Web App.

## 2. Arsitektur Multi-Bab (Anti-Rusak Saat Tambah Materi)
- Semua data pembelajaran dipisahkan sepenuhnya dari komponen UI dan disimpan di `/data/chapters/`.
- Halaman utama menampilkan **Bab 1: Al-Hiwayah (Aktif)** beserta **2 kartu Bab tambahan (status "Segera Hadir" / terkunci)** untuk memastikan *layout* tetap rapi saat materi bertambah di masa depan.

## 3. Alur Pengguna (Gamification Loop)
1. **Masuk Tanpa Login Rumit:** Siswa cukup mengisi **Nama Panggilan** (tanpa email/password).
2. **Panduan Pertama Kali (Slot Video Remotion):**
   - Saat pertama kali membuka aplikasi atau masuk ke fitur Kuis/Game, muncul *modal* panduan singkat.
   - Menggunakan `localStorage` agar hanya muncul otomatis 1 kali per perangkat, lalu tersedia sebagai tombol ikon `?` (Panduan) di pojok layar.
   - **Sistem Fallback:** Sebelum file video `.mp4` pendek (dari Claude + Remotion) dimasukkan ke `/public/videos/`, modal menampilkan panduan cepat 3 langkah bergambar. Jika file `.mp4` sudah tersedia, otomatis memutar video dengan tombol "Lewati".
3. **Modul Materi (Al-Hiwayah):**
   - Kartu *Mufrodat* (huruf Arab berharakat, arti, ilustrasi ringan, dan tombol putar audio `.mp3` lokal).
   - Penjelasan singkat pola kalimat sederhana (*Jumlah Ismiyah* / *Fi'liyah* terkait hobi) dan contoh teks pendek.
4. **Whiteboard Latihan Tulis (Papan Khat):**
   - Mode *tracing* (menebalkan *watermark* tipis huruf/kata Arab) + tombol "Tampilkan Contoh" untuk evaluasi mandiri dan tombol Hapus/Ganti Warna Tinta.
   - Tidak menggunakan penilaian otomatis tulisan tangan (OCR).
5. **Kuis Pemahaman & Panen Energi (5 Indikator Kitabah):**
   - Indikator 1: Menyusun huruf-huruf menjadi kata yang benar (*tap/drag-and-drop*).
   - Indikator 2: Menyusun kata acak menjadi kalimat sempurna (*tap/drag-and-drop*).
   - Indikator 3: Dikte audio (memutar `.mp3` lokal + mengetik jawaban memakai *Virtual Keyboard* Arab di layar).
   - Indikator 4: Menyalin/menulis kosakata atau kalimat sesuai contoh (*Virtual Keyboard* Arab).
   - Indikator 5: Mengidentifikasi bentuk kata tertentu atau pola kalimat dalam teks.
   - Setiap jawaban benar memberi **Energi** (koin virtual) untuk modal bermain game.
6. **Game Kompetitif Realtime: "Jisr Al-Kalam" (Duel Jembatan Kata):**
   - **Mode Kelas (40 HP):** Guru/Host membuat 1 Kode Room. Siswa masuk dengan Kode Room dan terbagi otomatis ke dalam **4 Tim** (Hijau, Biru, Kuning, Merah).
   - **Peta Grid 2D:** 4 Tim membangun jembatan dari sudut masing-masing menuju Oasis di tengah arena.
   - **Mekanik Energi:** Memasang petak jembatan mengurangi Energi. Jika Energi habis di tengah permainan, siswa klik **"Isi Energi"** dan menjawab soal kilat *Kitabah* untuk melanjutkan.
   - **Mekanik Duel:** Jika ujung jembatan dua tim bersentuhan, muncul *pop-up* **Duel Cepat 15 Detik** di layar anggota kedua tim—tim dengan akumulasi jawaban benar terbanyak merebut petak tersebut hingga *timer* permainan habis.