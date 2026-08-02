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
- Beberapa mode pengisian lembar: Standar, Bulk (1 lembar = 1 file), Ukuran Beragam/Mixed Size (skyline packing), Campur Foto + Mixed Size, Custom Layout (isi foto manual), dan **Custom Layout (Mixed Size)** — kotak-kotak berbeda ukuran disusun manual dengan bantuan packing otomatis yang sama seperti mode Mixed Size.
- Edit layout manual: geser/putar kotak, atur zoom & posisi crop per foto.
- Panduan potong (guide), warna bingkai, preset Polaroid/Frame.
- Export ke **PDF**, **PNG/JPG per halaman** (atau **ZIP semua halaman**), dengan DPI & format pilihan sendiri. Bisa juga export **halaman tertentu atau rentang halaman** (mis. `1,3,5-7`) saja sebagai PDF, ZIP, atau file gambar terpisah. Tersedia juga **Export Foto per-Kotak** — unduh tiap foto individual sudah terpotong sesuai ukuran kotaknya (lihat section "Export Layout" di bawah).
- Undo/Redo (Ctrl+Z / Ctrl+Y), mode Terang/Gelap, Bahasa ID/EN.
- Export & Import pengaturan layout ke/dari file **JSON**.

## Toolbar Edit Kanvas

Bar toolbar di bawah header (bisa disembunyikan/ditampilkan lewat tombol **🧰** di header, statusnya tersimpan di `localStorage`) berisi semua kontrol untuk mengedit layout kotak foto secara manual:

- **Undo / Redo** — tombol ↩/↪, sama dengan Ctrl+Z / Ctrl+Y.
- **✏️ Edit Layout: ON/OFF** — toggle mode edit, dipasangkan dengan dropdown **cakupan** (`Halaman ini saja` / `Semua halaman`) yang menentukan apakah perubahan hanya berlaku di halaman aktif atau ke semua halaman sekaligus.
- **🔄 Rotate Kotak** — putar kotak (beserta isinya) 90° pada kotak terpilih.
- **🔄 Rotate Foto** — putar **hanya foto** 90° di dalam kotak (ukuran/orientasi kotak tidak berubah).
- **↔ Flip Foto H** / **↕ Flip Foto V** — cerminkan foto secara horizontal/vertikal di dalam kotak terpilih.
- **✥ Crop Drag** — mode klik & seret langsung di atas kotak untuk mengatur posisi crop foto. Saat mode ini aktif dan ada kotak terpilih, **tombol panah (arrow keys)** bisa dipakai untuk menggeser posisi crop sedikit demi sedikit (nudge).
- **🖐️ Hand Tool** — mode seret kanvas untuk menggeser tampilan (klik kanan+seret juga selalu bisa dipakai kapan saja, di mode manapun).
- **Zoom Tampilan Lembar** — tombol −/+ dan indikator **Fit ⇄ 100%** (klik untuk beralih); juga bisa pakai Ctrl+Scroll pada preview, atau Ctrl +/Ctrl −/Ctrl 0 dari keyboard.
- **➕ Foto + / ➖ Foto -** — perbesar/perkecil zoom foto pada kotak terpilih; **🎯 Reset Foto Pan** mengembalikan posisi geser (pan) ke tengah.
- **🤖 Auto Crop Terpilih** — Auto Face Crop (AI) khusus untuk kotak yang sedang diseleksi di halaman aktif (boleh multi-kotak, boleh campuran beberapa ukuran sekaligus). Tiap kotak dipas-kan otomatis memakai aspect rasio ukurannya **masing-masing** (termasuk kalau kotak diputar manual 90°/270°), jadi hasilnya tetap benar walau seleksinya campuran ukuran berbeda — cocok dipakai pada layout Mixed Size / Custom Layout (Mixed Size). Klik tombol untuk membuka panel slider **Kepala / Margin / Rambut**, lalu tekan **🤖 Jalankan**.
- **⚙ Adjust Terpilih** — panel slider **Zoom / Pan X / Pan Y / Rotate** untuk mengatur crop foto secara manual pada semua kotak yang sedang diseleksi sekaligus (tanpa perlu buka panel ⚙ satu-satu per foto); ada tombol **↺ Reset** untuk mengembalikan seleksi ke crop default.
- **Snap Kotak** — kotak otomatis "nempel" ke kotak lain saat digeser.
- **Snap Grid** — nempel ke grid dengan jarak (mm) yang bisa diatur di kolom angka di sebelahnya.
- **📐 Snap Cut-Guide** — snap khusus ke posisi garis potong tengah-jarak, cocok dipakai bersama Cut Guide Style "Garis di Tengah Jarak" / "Tanda Potong di Tengah Jarak" agar jarak antar kotak tetap presisi sama dengan Box Spacing.
- **↺ Reset Terpilih / Reset Halaman Ini / Reset Semua Halaman** — mengembalikan posisi & transformasi (rotasi/flip/pan) kotak: hanya yang terpilih, semua kotak di halaman aktif, atau semua kotak di semua halaman.
- **Ratakan** — perataan antar-kotak-terpilih: Kiri, Tengah H, Kanan, Atas, Tengah V, Bawah (butuh min. 2 kotak terpilih), plus **Sebar H / Sebar V** untuk menyebarkan jarak secara merata (butuh min. 3 kotak).
- **Ratakan ke Kertas** — meratakan kotak terpilih ke tepi/tengah area cetak kertas (Kiri/Tengah H/Kanan/Atas/Tengah V/Bawah Kertas, min. 1 kotak). Ada opsi centang **"Sebagai Grup"**: jika aktif, kotak-kotak terpilih diratakan bersama sebagai satu grup (posisi relatif antar kotak tetap terjaga); jika tidak, tiap kotak diratakan sendiri-sendiri.
- **Urutan (Z-order)** — Paling Depan / Maju 1 / Mundur 1 / Paling Belakang, untuk mengatur kotak mana yang tampil di atas saat saling tumpang tindih.
- **✕ Hapus Pilihan** — batalkan seleksi kotak yang sedang aktif.
- **☰ Select** — mode seleksi multi: klik kotak untuk menambah/mengurangi dari seleksi (perilakunya seperti menahan Shift terus-menerus), sementara drag area untuk seleksi tetap berfungsi seperti biasa.
- Indikator jumlah kotak terpilih ditampilkan di ujung kanan toolbar.

Di header juga terdapat navigasi halaman (**‹ Prev** / **Next ›** beserta indikator "Halaman X / Y"), tombol ganti bahasa (**ID/EN**), dan tombol ganti tema terang/gelap — semuanya independen dari toolbar edit di atas.

### Shortcut Keyboard

| Shortcut | Fungsi |
|---|---|
| `Ctrl/Cmd + Z` | Undo |
| `Ctrl/Cmd + Y` atau `Ctrl/Cmd + Shift + Z` | Redo |
| `Ctrl/Cmd + Scroll` pada preview | Zoom tampilan lembar |
| `Ctrl/Cmd + +` / `Ctrl/Cmd + -` | Zoom tampilan lembar in/out |
| `Ctrl/Cmd + 0` | Toggle Fit ⇄ 100% |
| Tombol panah (↑↓←→) | Nudge posisi crop foto sedikit demi sedikit — hanya aktif saat mode **Crop Drag** menyala dan ada kotak terpilih |

## Fitur Baru: Auto Crop Wajah (AI)

Terletak di kartu **"🤖 Auto Crop Wajah (AI)"**, tepat di bawah panel "Foto Sumber".

Cara kerja:
1. Mendeteksi titik wajah (mata, dahi, dagu) memakai model **MediaPipe Face Landmarker**.
2. Meluruskan kemiringan kepala (rotasi otomatis berdasarkan posisi mata).
3. Menghitung area crop otomatis berdasarkan:
   - **Tinggi Kepala thd Kotak** — proporsi tinggi kepala terhadap tinggi kotak foto.
   - **Margin Atas** — jarak dari ubun-ubun ke tepi atas kotak.
   - **Estimasi Rambut di Atas Dahi** — kompensasi karena titik landmark dahi bukan ubun-ubun asli (rambut tidak terdeteksi model).
4. Untuk layout dengan kotak **seragam** ukurannya, hasil crop otomatis mengikuti **ukuran Kotak Foto** yang sudah diatur di kartu "Ukuran Kotak Foto" — jadi tidak ada preset ukuran terpisah, semuanya konsisten dengan layout cetak yang sedang dibuat. Untuk layout dengan kotak **berbeda-beda ukuran** (Mixed Size / Custom Layout Mixed Size), lihat sub-bagian "Auto Crop untuk Kotak-Foto yang Berbeda Ukuran" di bawah.
5. Nilai zoom & posisi pan yang dihasilkan langsung dipakai oleh sistem crop bawaan app utama (bisa disesuaikan manual lagi lewat tombol ⚙ seperti biasa).

### Auto Crop untuk Kotak-Foto yang Berbeda Ukuran (Mixed Size)

Kalau layout memakai mode **Mixed Size**, **Campur Foto + Mixed Size**, atau **Custom Layout (Mixed Size)** — di mana kotak foto tidak seragam dan tiap kotak bisa punya ukuran/aspect rasio sendiri — Auto Crop Wajah tetap bisa dipakai dan tetap menghasilkan crop yang pas untuk **masing-masing** ukuran, lewat dua jalur:

1. **Per baris ukuran, dari kartu "Daftar Ukuran Kotak per Lembar"** — tiap baris ukuran (mis. 30×40mm) di panel Mode Pengisian Lembar punya tombol **🤖** sendiri. Klik untuk membuka panel slider Kepala/Margin/Rambut khusus baris itu (kalau tidak diisi, otomatis memakai nilai slider global di kartu Auto Crop), lalu tekan **"🤖 Auto Crop Ukuran W×H mm"**. Sistem mencari **semua kotak di semua halaman** yang ukuran on-page-nya cocok dengan baris ini (termasuk kalau posisinya diputar 90° oleh algoritma packing) dan meng-crop ulang foto di kotak-kotak tersebut sesuai aspect rasio baris itu — tanpa mengubah crop foto yang sama di kotak berukuran lain. Baris yang sama juga punya tombol **⚙** untuk mengatur Zoom/Pan/Rotate manual yang berlaku ke semua kotak berukuran itu sekaligus, plus tombol reset khusus baris tersebut.
2. **Per seleksi kotak, dari toolbar edit kanvas** — tombol **🤖 Auto Crop Terpilih** (lihat section "Toolbar Edit Kanvas") meng-crop hanya kotak yang sedang diseleksi di halaman aktif, masing-masing memakai aspect rasio ukurannya sendiri — cocok untuk seleksi campuran beberapa ukuran kotak sekaligus, atau untuk mengoreksi ulang sebagian kotak saja. Tombol **⚙ Adjust Terpilih** di sebelahnya untuk penyesuaian manual Zoom/Pan/Rotate ke seleksi yang sama.

Karena hasil crop untuk kedua jalur ini disimpan sebagai **override per-kotak** (bukan menimpa nilai zoom/pan global milik foto), satu foto yang sama bisa dipakai di beberapa kotak berbeda ukuran dalam layout yang sama — dan masing-masing kotak tetap terframe dengan benar sesuai ukurannya sendiri-sendiri, tidak saling menimpa.

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

## Export Layout (PDF / Gambar / Foto per-Kotak)

Kartu **"Export"** di panel kanan (di bawah Preview) berisi pengaturan resolusi & format, plus empat kelompok tombol unduh.

### Pengaturan Resolusi & Format

- **Resolusi (DPI)** — dropdown 72 (layar) / 150 (draft) / 300 (cetak standar, default) / 450 / 600 (cetak tinggi) / **Custom…** (nilai bebas 30–1200 dpi lewat kolom "DPI Custom" di sebelahnya). DPI ini berlaku untuk semua hasil unduhan (gambar halaman, PDF, dan export foto per-kotak) — preview di layar sendiri tetap dirender ringan di resolusi tetap (150dpi dasar × devicePixelRatio), tidak ikut berubah mengikuti DPI export yang dipilih.
- **Format Unduh Gambar** — PNG (lossless, mendukung transparansi) atau JPG. Memilih JPG memunculkan kolom **Kualitas JPG** (10–100, default 92).
- Kedua pengaturan ini ikut tersimpan/dimuat lewat "Export/Import Pengaturan" (JSON) — lihat bagian di bawah.

### 🔢 Export Halaman Tertentu / Rentang

Kolom input khusus untuk export hanya sebagian halaman saja, bukan seluruh layout — berguna untuk cetak ulang 1 halaman saja, atau export beberapa halaman saja dari layout multi-halaman yang besar.

- Kolom **Nomor Halaman** — ketik daftar nomor halaman dan/atau rentang, dipisah koma, mis. `1,3,5-7` (halaman 1, 3, 5, 6, 7). Spasi di sekitar koma/tanda hubung diabaikan, dan entri duplikat/tumpang tindih otomatis dihilangkan & diurutkan. Kosongkan kolom ini dan pakai tombol "Semua Halaman" di bawah kalau mau export semuanya.
- **⬇ PDF** — export hanya halaman yang diisi, digabung jadi satu file PDF (urut halaman menaik, terlepas dari urutan pengetikan).
- **⬇ ZIP** — export hanya halaman yang diisi sebagai gambar, dikemas jadi satu file ZIP.
- **⬇ Terpisah** — export hanya halaman yang diisi sebagai file gambar terpisah, satu unduhan per halaman (perilakunya sama seperti "⬇ Semua Halaman" tapi dibatasi ke halaman yang diisi saja).
- Kalau kolom kosong, ada bagian yang tidak dikenali formatnya, atau semua nomor halaman di luar jangkauan (misal lebih besar dari jumlah total halaman), muncul toast peringatan dan tidak ada yang diekspor.
- Nama file otomatis mendapat tag rentang halaman, mis. `pasfoto-halaman-1-3_5.pdf` / `...-1-3_5.zip`, dengan halaman berurutan digabung jadi rentang `awal-akhir` dan dipisah `_`.

### 📄 Export PDF

- **⬇ Halaman Ini** — export halaman aktif sebagai satu file PDF.
- **⬇ Semua Halaman** — export seluruh halaman jadi satu file PDF multi-halaman, tiap halaman mengikuti ukuran kertas yang dipilih.

### 🖼️ Export Gambar (PNG/JPG)

- **⬇ Halaman Ini** — unduh halaman aktif sebagai satu file gambar (PNG/JPG sesuai format terpilih).
- **⬇ Semua Halaman** — unduh tiap halaman sebagai file gambar terpisah, satu per satu.
- **⬇ Semua Halaman (ZIP)** — unduh semua halaman sekaligus, dikemas dalam satu file ZIP.
- Nama file gambar/PDF halaman mengikuti nama foto sumber untuk mode **Bulk** dan **Mixed Size** (karena tiap lembar = 1 foto), dengan suffix `-2`, `-3`, dst. kalau ada nama sama. Untuk mode lain (Standar, Custom Layout, dll. — di mana 1 lembar bisa berisi banyak foto berbeda) nama file jatuh ke default `pasfoto-halaman-N`.

### ✂️ Export Foto (Ukuran Crop/Kotak) — fitur baru

Kelompok export baru yang mengunduh **foto individual, bukan halaman komposit** — tiap foto diekspor sudah terpotong (crop) persis sesuai ukuran kotaknya masing-masing, termasuk kalau layout memakai kotak berbeda-beda ukuran (Mixed Size). Cocok untuk kebutuhan seperti mengirim file lepas per foto ke studio cetak lain, alih-alih lembar gabungan.

- **⬇ Halaman Ini** — export semua foto di halaman aktif.
- **⬇ Semua Halaman** — export semua foto dari semua halaman, satu per satu.
- **⬇ Semua Foto (ZIP)** — sama seperti di atas, tapi dikemas dalam satu file ZIP.
- **⬇ Kotak Terpilih** — hanya foto dari kotak yang sedang diseleksi di halaman aktif.

Detail penamaan & dedup:
- Pola nama file: `[hal0N_]NamaFoto[-2] - kotak_LxTmm` — prefiks `hal0N_` hanya muncul kalau cakupan export mencakup lebih dari 1 halaman (Semua Halaman / ZIP); tag ukuran (mis. `30x40mm`) selalu mengikuti ukuran kotak asli foto tsb.
- Kalau ada beberapa kotak yang **identik persis** (foto sumber sama, ukuran kotak sama, rotasi/flip sama, dan crop/zoom/pan/tilt sama) — misalnya hasil "isi penuh 1 halaman" bulk dengan 1 foto — hanya **1 file** yang diekspor untuk kombinasi itu, bukan diulang per kotak, supaya tidak menghasilkan banyak file duplikat identik. Kotak dengan ukuran atau crop yang berbeda tetap diekspor terpisah walau berasal dari foto sumber yang sama.

---

## Export & Import Pengaturan (JSON)

Tombol **"⬆ Export Pengaturan"** / **"⬇ Import Pengaturan"** menyimpan/memuat konfigurasi layout ke file `.json`, termasuk:

- Ukuran kertas, kotak, gap, margin, warna, mode isi, guide, dll (semua pengaturan bawaan app).
- 3 slider Auto Crop AI: `aiHeadRatio`, `aiTopMargin`, `aiHairExt`.
- Pengaturan Export: **DPI** (termasuk nilai Custom), **Format Unduh Gambar** (PNG/JPG), dan **Kualitas JPG**.

**Yang tidak ikut tersimpan:** daftar foto itu sendiri (file gambar) dan status AI per foto (`aiStatus` auto-crop maupun `bgStatus` hapus-background) — ini karena file gambar tidak bisa disematkan otomatis ke JSON pengaturan. Setelah reload halaman atau import settings, foto perlu di-upload ulang, lalu bisa dijalankan ulang "Auto Crop Semua Foto" / hapus background per foto bila perlu.

---

## Catatan Teknis (untuk pengembangan lebih lanjut)

- Model AI dimuat lewat `<script type="module">` terpisah, mengekspos `window.faceAI = { ready, model, detect() }` agar bisa dipakai dari script utama (non-module).
- Fungsi inti ada di bagian `AI AUTO CROP` pada script utama:
  - `aiRotateImageToCanvas()` — memutar gambar ke canvas baru agar mata sejajar.
  - `aiTransformPoint()` — mentransformasi koordinat landmark ke sistem koordinat canvas hasil rotasi.
  - `autoCropImage(im)` — pipeline lengkap: deteksi → rotasi → hitung rect crop → konversi ke `zoom/offX/offY` sesuai skema `drawCover()` app utama.
  - `autoCropAllImages()` — batch semua foto.
  - Untuk kotak berbeda ukuran (Mixed Size): `cellMatchesBoxSize()` mencocokkan ukuran on-page sebuah kotak (mendukung orientasi tertukar akibat rotasi packing, toleransi 0.05mm) dengan salah satu baris `state.mixedBoxes`; `findCellsForBoxSize()` mengumpulkan semua kotak di semua halaman yang cocok; `autoCropBoxSize()` menjalankan auto crop untuk kumpulan tersebut (dipanggil dari tombol 🤖 per baris ukuran); `autoCropSelectedCells()` melakukan hal serupa tapi untuk `state.selection` di halaman aktif (dipanggil dari tombol toolbar 🤖 Auto Crop Terpilih), dengan aspect rasio per kotak diambil dari `getCellEffectiveRect()` (memperhitungkan rotasi manual kotak). Hasilnya disimpan sebagai override di `state.cellCropOverrides['pageIdx:cellIdx']` — bukan menimpa `im.zoom/offX/offY` milik foto — supaya satu foto yang dipakai di kotak-kotak berbeda ukuran tetap ter-crop independen per kotak.
- Foto hasil auto-crop (sudah diputar) disimpan sebagai elemen `<img>` baru (dari `canvas.toDataURL()`), bukan menimpa foto asli. Foto asli tetap disimpan di `im.origImg` untuk keperluan tombol 🗘 dan deteksi ulang (deteksi selalu dijalankan dari foto asli, bukan hasil rotasi sebelumnya, supaya tidak terjadi akumulasi kesalahan rotasi).
- `aiImageCache` (Map `url → Image`) menyimpan semua elemen `<img>` yang pernah dibuat, karena sistem Undo/Redo bawaan app menyimpan snapshot sebagai **string JSON** — objek `<img>` tidak bisa diserialisasi langsung ke JSON, jadi snapshot hanya menyimpan `url` (data-URL) dan mengambil kembali elemen `<img>`-nya dari cache saat undo/redo dijalankan.
- Batas zoom UI bawaan app adalah `1×`–`3×` (tidak bisa "zoom out" di bawah crop cover default); jika area wajah yang dibutuhkan lebih lebar dari itu, nilai zoom otomatis dibatasi ke `1×` dan ditandai `🤖✓*`.
- Fitur Hapus Background dimuat lewat `<script type="module">` terpisah, mengekspos `window.bgRemovalAI = { ready, model, removeBackground(imgEl) }` — polanya sama dengan `window.faceAI`, tapi model yang dipakai adalah `ImageSegmenter` (bukan `FaceLandmarker`), dengan `outputConfidenceMasks: true`.
  - `removeBgImage(im)` — pipeline: tunggu model siap → `removeBackground()` → hasil data-URL PNG di-load jadi `<img>` baru → menimpa `im.img`/`im.url` (masuk ke `aiImageCache` yang sama seperti auto-crop) → update badge `bgStatus`.
  - `bgBadge(status)` — render badge status (`processing`/`ok`/`fail`) di baris foto, berdampingan dengan `aiBadge(status)` milik auto-crop.
  - Di dalam `removeBackground()`, mask hasil model (resolusi rendah) di-upscale **terpisah** dari foto asli (yang tetap digambar di resolusi penuh), lalu digabung sebagai alpha channel — supaya ketajaman foto tidak ikut turun mengikuti resolusi mask.
- `drawCoverRotated(ctx,img,dx,dy,dw,dh,zoom,offX,offY,rotDeg)` — fungsi gambar tunggal yang dipakai untuk slider **"Putar (Miring)"** (dipakai di render halaman, preview live, dan hasil export PDF/PNG, jadi semuanya konsisten). Foto digambar `cover`-fit lalu diputar `rotDeg` derajat di sekitar titik tengah kotak, dengan `clip()` ke area kotak (dw×dh) supaya kemiringan tidak bocor ke frame/kotak tetangga. Sebelum diputar, ukuran persegi tujuan (dw,dh) discale otomatis dengan faktor `s = |cos θ| + max(dw/dh, dh/dw) × |sin θ|` — rumus minimum supaya persegi yang sudah diputar itu tetap menutupi penuh kotak asli (dw×dh) di sudut berapa pun, mencegah sudut kotak yang tidak tertutup foto ("segitiga putih diagonal"). `zoom`/`offX`/`offY` (dari sistem crop bawaan) tetap dipakai apa adanya di atas rect yang sudah di-scale itu.
- Export: `getSelectedDPI()`/`canvasToDpiBlob()` menerapkan DPI & format (PNG/JPG+quality) terpilih ke sebuah canvas sebelum diunduh; `downloadCanvas()` membungkusnya jadi trigger `<a download>`. `buildPageFilenames()` menentukan nama file per halaman (ikut nama foto sumber utk mode Bulk/Mixed Size, fallback `pasfoto-halaman-N` utk mode lain). Untuk export foto per-kotak: `buildCropExportPlan(meta,scope)` mengumpulkan sel-sel bergambar sesuai cakupan (`page`/`all`/`selected`), melewati sel duplikat lewat `cellCropSignature()` (signature dari id foto + rotasi/flip kotak & foto + zoom/pan/tilt, dibulatkan 2 desimal) supaya kotak yang hasilnya identik byte-per-byte hanya diekspor sekali, lalu menyusun nama file lewat `sanitizeFilename()` + `formatBoxSizeTag()` (mis. `NamaFoto - kotak_30x40mm`, dengan prefiks `hal0N_` kalau cakupannya multi-halaman).
- Export rentang halaman: `parsePageRangeInput(str,maxPages)` mem-parse teks bergaya `1,3,5-7` menjadi array indeks halaman 0-based yang terurut & bebas duplikat, dibatasi ke `[1..maxPages]`, dan mengembalikan `null` untuk input kosong/tidak dikenali/seluruhnya di luar jangkauan (dipakai handler tombol untuk menampilkan toast validasi, bukan mengekspor apa-apa). `formatPageRangeTag(indices)` mengubah array itu kembali jadi tag nama file yang ringkas, menggabungkan halaman berurutan jadi rentang `awal-akhir` yang dipisah `_` (mis. `[0,1,2,4]` → `1-3_5`). Ketiga tombol rentang (`btnExportPdfRange`/`btnDlRangeZip`/`btnDlRange`) memakai ulang pipeline `renderPageCanvas()`/`canvasToDpiBlob()`/`downloadCanvas()` yang persis sama dengan tombol "Semua Halaman", hanya saja melakukan iterasi pada daftar indeks hasil parsing, bukan semua halaman.

---

## Pembaruan UI Lainnya

- **Panel kiri diperlebar** dari 400px → 460px, supaya label-label di kartu Auto Crop AI (mis. "Margin Atas (Ubun ke Tepi)") tidak terpotong/wrap ke 2 baris.
- **Preview canvas dirender lebih tajam**: resolusi raster preview dinaikkan dari 150dpi menjadi 300dpi dasar, dikalikan lagi dengan `devicePixelRatio` layar (maks 2×) — supaya tidak buram di layar retina/high-DPI atau saat di-zoom. Tidak memengaruhi resolusi hasil export PDF/PNG (itu memang sudah memakai DPI pilihan sendiri).
- **Perbaikan slider "Putar (Miring)" — segitiga putih/background di sudut sekarang hilang.** Slider ini (di panel ⚙ per-foto, juga berlaku pada hasil Auto Crop Wajah AI) memutar foto secara halus per-derajat di dalam kotak. Sebelumnya, memutar foto pada sudut berapa pun membuat sudut-sudut kotak tidak lagi tertutup foto, sehingga warna latar (`photoBgColor`) atau putih polos mengintip di sudut secara diagonal. Sekarang zoom foto dikompensasi otomatis mengikuti sudut kemiringan — makin miring, foto membesar secukupnya — supaya kotak selalu tertutup penuh di sudut berapa pun, mirip cara kerja alat "Straighten" di Lightroom/Photoshop.
- **Perbaikan fitur Hapus Background (✂️) yang selalu gagal.** Ada bug scoping variabel di dalam `window.bgRemovalAI.removeBackground()` yang membuat fungsi ini selalu melempar error di setiap pemanggilan (bahkan setelah proses segmentasinya sendiri berhasil sepenuhnya), sehingga tombol ✂️ selalu berakhir menampilkan badge/toast gagal `✂️⚠`. Canvas-canvas kerja sekarang dideklarasikan di scope fungsi, bukan di dalam blok `try{}`, supaya blok `finally{}`-nya bisa benar-benar mengaksesnya — fitur ini sekarang berjalan sampai selesai dan mengembalikan hasil background transparan seperti seharusnya.

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
