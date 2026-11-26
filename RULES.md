# RULES.md — Standar Kode, Desain & Workflow Alkuttab (الكُتَّاب)

## 1. Tech Stack & Prinsip Biaya Nol (Free Tier)
- Gunakan **Next.js (App Router) + TypeScript + Tailwind CSS** (siap deploy gratis di Vercel).
- Database *realtime* menggunakan **Firebase Realtime Database** (hanya diintegrasikan mulai Tahap 5).
- DILARANG menginstal Remotion di dalam repositori ini. Video panduan cukup berupa file `.mp4` statis di `/public/videos/`.

## 2. Aturan Audio & Aset (Kode Wajib Bersih)
- DILARANG memakai Web Speech API (`speechSynthesis`) atau live TTS API di dalam kode web.
- Semua audio dikte & mufrodat wajib memutar file `.mp3` statis dari `/public/audio/` yang dipetakan di file data bab.
- Untuk membuat file MP3 awal, jalankan skrip Python sementara (`edge-tts`, suara `ar-SA-ZariyahNeural`, teks Arab berharakat lengkap) di luar folder `src/` atau `app/`, lalu HAPUS skrip sementara tersebut setelah file `.mp3` berhasil tersimpan.

## 3. Design System "Modern Oasis" (Anti-AI Slop & Mobile-First)
- DILARANG membuat tampilan dark-mode neon/ungu generik.
- **Mobile-First:** Di layar HP wajib gunakan Bottom Navigation Bar dan area sentuh minimal `44x44px`. Sidebar kiri hanya tampil di layar desktop (tampilan Host/Proyektor).
- **Palet Warna:**
  - Background utama: `#FAF6F0` (Krem Perkamen Hangat)
  - Kartu / Surface: `#FFFFFF` dengan border `#E8E2D5`, sudut lembut (`rounded-2xl` / `rounded-3xl`), bayangan halus.
  - Primary (Hero Banner & Aksi Utama): `#159A8C` dan `#0F5C52` (Hijau Toska/Zamrud Oasis)
  - Accent 1 (Energi / Highlight): `#FBBF24` (Kuning Hangat)
  - Accent 2 (Duel / Aksen Ceria): `#F46A5B` (Koral Hangat)
  - Teks Utama: `#1F2937`
- **Tipografi Arab (WAJIB):**
  - Load Google Fonts `Noto Naskh Arabic` (untuk teks belajar/soal) dan `Plus Jakarta Sans` (untuk teks UI Indonesia).
  - Logo utama bertuliskan **الكُتَّاب** (dengan harakat jelas agar tidak terbaca *Al-Kitab*) disertai label `Alkuttab`.
  - Setiap elemen teks Arab wajib memiliki `dir="rtl"`, `lang="ar"`, ukuran minimal `text-2xl`, dan `leading-loose` agar harakat tidak bertabrakan.

## 4. Aturan Khusus Whiteboard (Anti-Bug Sentuhan HP)
- Wajib menggunakan HTML5 `<canvas>` dengan **Pointer Events** (`onPointerDown`, `onPointerMove`, `onPointerUp`).
- Wajib memasang CSS `touch-action: none` pada kanvas agar layar HP tidak ikut ter-scroll saat menulis.
- Wajib menyinkronkan resolusi internal kanvas dengan `window.devicePixelRatio` dan menghitung koordinat presisi memakai `canvas.getBoundingClientRect()`.

## 5. Aturan Eksekusi & Git Safety
- Bekerjalah bertahap satu per satu sesuai instruksi user. JANGAN membangun seluruh fitur dalam satu kali respons.
- JANGAN pernah melakukan *hardcode* isi bab di komponen halaman—selalu baca dari `/data/chapters/`.
- Di setiap akhir tahap, berikan langkah singkat cara mengetes di browser/HP dan tunggu konfirmasi "OKE LANJUT" sebelum membuat *commit* Git dan pindah ke tahap berikutnya.