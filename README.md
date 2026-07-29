# AutoPasFoto

PasFoto Layout + Auto Crop AI (Combined)

Aplikasi tata letak cetak pas foto (`autopasfoto.html`) — gabungan dari:

- **PasFoto Layout** — app utama untuk menyusun beberapa foto ke dalam lembar cetak (ukuran kertas custom, ukuran kotak custom, mode isi lembar, export PDF/PNG/ZIP, dll).
- **Pas Foto Auto Crop & Align** — fitur deteksi wajah otomatis (AI) yang diintegrasikan sebagai kartu baru **"🤖 Auto Crop Wajah (AI)"** di panel kiri app utama.
- **Hapus Background (AI)** — fitur baru, tombol ✂️ di tiap baris foto untuk menghapus background foto secara otomatis (jadi transparan) memakai model AI yang jalan 100% di browser.

Satu file HTML, tidak perlu instalasi apa pun — cukup dibuka di browser modern (Chrome/Edge/Firefox terbaru).

---

## Fitur Utama (dari app aslinya, tidak berubah)

- Upload banyak foto sekaligus (file atau folder).
- Atur ukuran kertas, ukuran kotak foto, jarak antar kotak, margin dalam/luar.
- Beberapa mode pengisian lembar: Standar, Bulk (1 lembar = 1 file), Mixed Size (skyline packing).
- Edit layout manual: geser/putar kotak, atur zoom & posisi crop per foto.
- Panduan potong (guide), warna bingkai, preset Polaroid/Frame.
- Export ke **PDF** dan **PNG per halaman**, atau **ZIP semua halaman**.
- Undo/Redo (Ctrl+Z / Ctrl+Y), mode Terang/Gelap, Bahasa ID/EN.
- Export & Import pengaturan layout ke/dari file **JSON**.

## Fitur Baru: Auto Crop Wajah (AI)

Terletak di kartu **"🤖 Auto Crop Wajah (AI)"**, tepat di bawah panel "Foto Sumber".

Cara kerja:
1. Mendeteksi titik wajah (mata, dahi, dagu) memakai model **MediaPipe Face Landmarker**.
2. Meluruskan kemiringan kepala (rotasi otomatis berdasarkan posisi mata).
3. Menghitung area crop otomatis berdasarkan:
   - **Tinggi Kepala thd Kotak** — proporsi tinggi kepala terhadap tinggi kotak foto.
   - **Margin Atas** — jarak dari ubun-ubun ke tepi atas kotak.
   - **Estimasi Rambut di Atas Dahi** — kompensasi karena titik landmark dahi bukan ubun-ubun asli (rambut tidak terdeteksi model).
4. Hasil crop otomatis mengikuti **ukuran Kotak Foto** yang sudah diatur di kartu "Ukuran Kotak Foto" — jadi tidak ada preset ukuran terpisah, semuanya konsisten dengan layout cetak yang sedang dibuat.
5. Nilai zoom & posisi pan yang dihasilkan langsung dipakai oleh sistem crop bawaan app utama (bisa disesuaikan manual lagi lewat tombol ⚙ seperti biasa).

Kontrol per foto:
| Tombol | Fungsi |
|---|---|
| 🤖 | Auto crop foto ini saja |
| ✂️ | Hapus background foto ini (lihat section "Hapus Background (AI)" di bawah) |
| 🗘 | Kembalikan ke foto asli (batalkan hasil auto-crop **dan/atau** hapus-background) — hanya muncul jika foto sudah pernah diproses AI |
| ⚙ | Atur zoom/pan manual (bawaan app) |
| 🗎 | Isi penuh sejumlah lembar (bawaan app) |
| ✕ | Hapus foto |

Tombol **"⚙️ Auto Crop Semua Foto"** memproses seluruh daftar foto secara berurutan.

Badge status di tiap baris foto:
- `🤖…` — sedang mendeteksi
- `🤖✓` — berhasil
- `🤖✓*` — berhasil, tapi zoom dibatasi (area wajah minta crop lebih lebar dari yang bisa ditampilkan pada rasio kotak saat ini)
- `🤖⚠` — wajah tidak terdeteksi (foto tetap bisa diatur manual seperti biasa)

---

## Fitur Baru: Hapus Background (AI)

Tombol **✂️** di tiap baris foto (sebelah tombol 🤖) menghapus background foto secara otomatis, menghasilkan foto dengan background **transparan** (PNG alpha channel).

Cara kerja:
1. Memakai model segmentasi **MediaPipe Image Segmenter (selfie segmenter)** untuk membedakan area orang vs. background per piksel (confidence mask 0–1).
2. Foto tetap digambar di **resolusi penuh/asli** — hanya mask/alpha-nya saja yang di-upscale dari resolusi rendah keluaran model, supaya ketajaman foto tidak ikut turun.
3. Karena app ini sudah punya pengaturan **Warna Background Foto** (`photoBgColor`), transparansi hasil hapus-background otomatis "diisi" warna latar yang kamu pilih (mis. merah/biru untuk pas foto resmi) saat dirender ke layout/PDF/PNG — jadi tidak perlu proses tambahan.
4. Tombol **🗘 (kembalikan foto asli)** akan membatalkan hasil hapus-background sekaligus hasil auto-crop, karena keduanya sama-sama menimpa `im.img`/`im.url` dan disimpan lewat mekanisme yang sama seperti auto-crop (foto asli tetap aman di `im.origImg`).

Badge status di tiap baris foto:
- `✂️…` — sedang memproses
- `✂️✓` — background berhasil dihapus
- `✂️⚠` — gagal menghapus background (cek koneksi internet / status model)

Catatan kualitas:
- Hasil terbaik untuk foto dengan latar cukup kontras terhadap orang/baju. Latar yang mirip warna kulit/baju kadang perlu koreksi manual (mis. foto ulang dengan latar polos).
- Tepi potongan (terutama rambut) akan sedikit lembut/halus — ini normal untuk semua tool background-removal berbasis AI, bukan indikasi foto yang blur; resolusi foto itu sendiri tetap terjaga penuh (lihat poin 2 di atas).

---

## Kebutuhan Koneksi Internet

Model AI **tidak disertakan dalam file** — dimuat dari CDN saat halaman dibuka:

- `https://cdn.jsdelivr.net/npm/@mediapipe/tasks-vision@0.10.14/...` (library + runtime WASM, dipakai bersama oleh fitur Auto Crop Wajah dan Hapus Background)
- `https://storage.googleapis.com/mediapipe-models/face_landmarker/...` (file model deteksi wajah, untuk Auto Crop)
- `https://storage.googleapis.com/mediapipe-models/image_segmenter/selfie_segmenter/...` (file model segmentasi orang/background, untuk fitur Hapus Background ✂️)

Selama proses ini gagal, kartu AI akan menampilkan status **"❌ Gagal memuat model..."**, dan biasanya muncul error semacam `Failed to fetch` di console. Fitur layout/cetak lain di app tetap berfungsi normal tanpa koneksi ini.

> **Catatan:** status model Auto Crop Wajah dan status model Hapus Background sama-sama ditampilkan di baris status yang sama (`aiEngineStatus`) di UI. Karena keduanya dimuat lewat modul terpisah secara paralel, pesan yang tampil di layar adalah pesan dari model yang **terakhir selesai dimuat** — bukan berarti model yang satunya gagal. Cek Console (F12) kalau butuh detail kedua status ini secara terpisah.

Penyebab umum bila gagal:
1. Tidak ada koneksi internet saat halaman dimuat.
2. File dibuka langsung sebagai `file://...` — sebagian browser membatasi fetch dari file lokal. Solusi: jalankan lewat server lokal, mis. `python3 -m http.server` lalu buka `http://localhost:8000/autopasfoto.html`.
3. Ad-blocker / ekstensi privasi / firewall kantor memblokir `cdn.jsdelivr.net` atau `storage.googleapis.com`.

---

## Export & Import Pengaturan (JSON)

Tombol **"⬆ Export Pengaturan"** / **"⬇ Import Pengaturan"** menyimpan/memuat konfigurasi layout ke file `.json`, termasuk:

- Ukuran kertas, kotak, gap, margin, warna, mode isi, guide, dll (semua pengaturan bawaan app).
- 3 slider Auto Crop AI: `aiHeadRatio`, `aiTopMargin`, `aiHairExt`.

**Yang tidak ikut tersimpan:** daftar foto itu sendiri (file gambar) dan status AI per foto (`aiStatus` auto-crop maupun `bgStatus` hapus-background) — ini karena file gambar tidak bisa disematkan otomatis ke JSON pengaturan. Setelah reload halaman atau import settings, foto perlu di-upload ulang, lalu bisa dijalankan ulang "Auto Crop Semua Foto" / hapus background per foto bila perlu.

---

## Catatan Teknis (untuk pengembangan lebih lanjut)

- Model AI dimuat lewat `<script type="module">` terpisah, mengekspos `window.faceAI = { ready, model, detect() }` agar bisa dipakai dari script utama (non-module).
- Fungsi inti ada di bagian `AI AUTO CROP` pada script utama:
  - `aiRotateImageToCanvas()` — memutar gambar ke canvas baru agar mata sejajar.
  - `aiTransformPoint()` — mentransformasi koordinat landmark ke sistem koordinat canvas hasil rotasi.
  - `autoCropImage(im)` — pipeline lengkap: deteksi → rotasi → hitung rect crop → konversi ke `zoom/offX/offY` sesuai skema `drawCover()` app utama.
  - `autoCropAllImages()` — batch semua foto.
- Foto hasil auto-crop (sudah diputar) disimpan sebagai elemen `<img>` baru (dari `canvas.toDataURL()`), bukan menimpa foto asli. Foto asli tetap disimpan di `im.origImg` untuk keperluan tombol 🗘 dan deteksi ulang (deteksi selalu dijalankan dari foto asli, bukan hasil rotasi sebelumnya, supaya tidak terjadi akumulasi kesalahan rotasi).
- `aiImageCache` (Map `url → Image`) menyimpan semua elemen `<img>` yang pernah dibuat, karena sistem Undo/Redo bawaan app menyimpan snapshot sebagai **string JSON** — objek `<img>` tidak bisa diserialisasi langsung ke JSON, jadi snapshot hanya menyimpan `url` (data-URL) dan mengambil kembali elemen `<img>`-nya dari cache saat undo/redo dijalankan.
- Batas zoom UI bawaan app adalah `1×`–`3×` (tidak bisa "zoom out" di bawah crop cover default); jika area wajah yang dibutuhkan lebih lebar dari itu, nilai zoom otomatis dibatasi ke `1×` dan ditandai `🤖✓*`.
- Fitur Hapus Background dimuat lewat `<script type="module">` terpisah, mengekspos `window.bgRemovalAI = { ready, model, removeBackground(imgEl) }` — polanya sama dengan `window.faceAI`, tapi model yang dipakai adalah `ImageSegmenter` (bukan `FaceLandmarker`), dengan `outputConfidenceMasks: true`.
  - `removeBgImage(im)` — pipeline: tunggu model siap → `removeBackground()` → hasil data-URL PNG di-load jadi `<img>` baru → menimpa `im.img`/`im.url` (masuk ke `aiImageCache` yang sama seperti auto-crop) → update badge `bgStatus`.
  - `bgBadge(status)` — render badge status (`processing`/`ok`/`fail`) di baris foto, berdampingan dengan `aiBadge(status)` milik auto-crop.
  - Di dalam `removeBackground()`, mask hasil model (resolusi rendah) di-upscale **terpisah** dari foto asli (yang tetap digambar di resolusi penuh), lalu digabung sebagai alpha channel — supaya ketajaman foto tidak ikut turun mengikuti resolusi mask.

---

## Pembaruan UI Lainnya

- **Panel kiri diperlebar** dari 400px → 460px, supaya label-label di kartu Auto Crop AI (mis. "Margin Atas (Ubun ke Tepi)") tidak terpotong/wrap ke 2 baris.
- **Preview canvas dirender lebih tajam**: resolusi raster preview dinaikkan dari 150dpi menjadi 300dpi dasar, dikalikan lagi dengan `devicePixelRatio` layar (maks 2×) — supaya tidak buram di layar retina/high-DPI atau saat di-zoom. Tidak memengaruhi resolusi hasil export PDF/PNG (itu memang sudah memakai DPI pilihan sendiri).

---

---

## Menjalankan 100% Offline (`autopasfoto-offline.html`)

Selain `autopasfoto.html` (yang memuat semua library dari CDN), tersedia juga versi **`autopasfoto-offline.html`** yang mengarah ke file lokal di folder `libs/`, jadi bisa dipakai tanpa koneksi internet sama sekali.

### Struktur folder yang harus disiapkan

```
project-folder/
├── autopasfoto-offline.html
└── libs/
    ├── jspdf.umd.min.js
    ├── jszip.min.js
    └── mediapipe/
        ├── vision_bundle.mjs
        ├── face_landmarker.task
        ├── selfie_segmenter.tflite
        └── wasm/
            └── (semua isi folder wasm dari CDN, apa adanya)
```

### Cara mengisi folder `libs/`

1. **jspdf.umd.min.js**
   Unduh dari `https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js` → simpan ke `libs/jspdf.umd.min.js`.

2. **jszip.min.js**
   Unduh dari `https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js` → simpan ke `libs/jszip.min.js`.

3. **MediaPipe (fitur Auto Crop AI)** — paling gampang lewat npm di komputer yang online:
   ```bash
   npm install @mediapipe/tasks-vision@0.10.14
   ```
   Lalu salin:
   - `node_modules/@mediapipe/tasks-vision/vision_bundle.mjs` → `libs/mediapipe/vision_bundle.mjs`
   - seluruh isi `node_modules/@mediapipe/tasks-vision/wasm/` → `libs/mediapipe/wasm/` (folder ini berisi beberapa file `.wasm`/`.js`, salin **semuanya**, bukan cuma satu file)
   - unduh manual model deteksi wajahnya dari `https://storage.googleapis.com/mediapipe-models/face_landmarker/face_landmarker/float16/1/face_landmarker.task` → simpan ke `libs/mediapipe/face_landmarker.task` (file ini tidak ikut ter-download lewat `npm install`, harus diambil terpisah).
   - unduh manual model hapus-background (untuk fitur ✂️) dari `https://storage.googleapis.com/mediapipe-models/image_segmenter/selfie_segmenter/float16/latest/selfie_segmenter.tflite` → simpan ke `libs/mediapipe/selfie_segmenter.tflite` (file ini juga tidak ikut ter-download lewat `npm install`, harus diambil terpisah, sama seperti model deteksi wajah).

4. **Font Google (opsional)** — dihapus dari versi offline. Tanpa ini, tampilan tetap normal, browser otomatis pakai font sistem sebagai pengganti `DM Mono`/`Syne`. Kalau mau font identik, unduh file `.woff2`-nya dan tambahkan `@font-face` manual di bagian `<style>`.

### ⚠️ Wajib dibuka lewat server lokal, bukan double-click file

Karena app ini pakai `<script type="module">` dan `fetch()` (MediaPipe mengambil file wasm & model lewat fetch), browser akan **memblokir permintaan tersebut** kalau file dibuka langsung sebagai `file://...` (kena kebijakan CORS browser). Jalankan server statis sederhana dulu di folder project, misalnya:

```bash
cd project-folder
python3 -m http.server 8000
```

Lalu buka `http://localhost:8000/autopasfoto-offline.html` di browser. Setelah semua file `libs/` di atas terpasang lengkap, seluruh fitur — termasuk Auto Crop Wajah AI — akan berjalan tanpa koneksi internet sama sekali.

### Cara cek instalasi sudah benar

- Buka DevTools (F12) → tab **Console** dan **Network** saat memuat halaman.
- Tidak boleh ada request yang mengarah ke domain luar (`cdn.jsdelivr.net`, `storage.googleapis.com`, dst) — semua harus mengarah ke `libs/...` lokal.
- Kartu **"🤖 Auto Crop Wajah (AI)"** akan menampilkan **"✅ Model hapus background siap"** atau **"✅ Model AI siap digunakan"** (bergantian, lihat catatan di section "Kebutuhan Koneksi Internet") jika `libs/mediapipe/` sudah lengkap dan benar — termasuk `selfie_segmenter.tflite` untuk fitur ✂️.

---

## Keterbatasan yang Diketahui


- Deteksi wajah hanya mendukung **1 wajah per foto** (`numFaces: 1`); jika foto berisi lebih dari satu wajah, hasil bisa tidak sesuai harapan.
- Estimasi "ubun-ubun" (`hairExt`) bersifat perkiraan geometris, bukan deteksi rambut sesungguhnya — sebaiknya dicek ulang manual untuk hasil cetak resmi (paspor, dokumen legal, dll).
- Hapus Background (✂️) memakai model segmentasi umum (bukan khusus rambut/potret detail); tepi rambut halus atau warna latar yang mirip warna kulit/baju bisa menghasilkan potongan yang kurang presisi dan perlu dicek manual.
- Status model Auto Crop Wajah dan Hapus Background berbagi satu baris status di UI (`aiEngineStatus`) — hanya pesan dari model yang terakhir selesai dimuat yang tampil di layar, meski keduanya dimuat/berjalan secara independen.
- Butuh koneksi internet aktif setiap kali halaman dibuka (model tidak di-cache secara permanen di semua browser) — **kecuali** memakai versi `autopasfoto-offline.html` dengan folder `libs/` terisi lengkap (lihat bagian "Menjalankan 100% Offline" di atas).
- Undo/Redo tidak menyimpan daftar foto yang ditambah/dihapus, hanya menyimpan qty/zoom/pan/status AI dari foto yang sudah ada dalam sesi tersebut (mengikuti perilaku app aslinya).
