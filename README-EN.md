# AutoPasFoto

PasFoto Layout + Auto Crop AI (Combined)

A passport-photo print-layout app (`autopasfoto.html`) — a merge of:

- **PasFoto Layout** — the main app for arranging multiple photos onto printable sheets (custom paper size, custom box size, sheet-filling modes, PDF/PNG/ZIP export, etc.).
- **Pas Foto Auto Crop & Align** — an automatic face-detection (AI) feature, integrated as a new card **"🤖 Auto Crop Wajah (AI)"** (Auto Crop Face (AI)) in the main app's left panel.
- **Background Removal (AI)** — a new feature, a ✂️ button on every photo row that automatically removes the photo's background (making it transparent) using an AI model that runs 100% in the browser.

Single HTML file, no installation required — just open it in a modern browser (latest Chrome/Edge/Firefox).

---

## Core Features (from the original app, unchanged)

- Upload multiple photos at once (individual files or a whole folder).
- Configure paper size, photo box size, spacing between boxes, inner/outer margins.
- Several sheet-filling modes: Standard, Bulk (1 sheet = 1 file), Mixed Size (skyline packing).
- Manual layout editing: drag/rotate boxes, adjust zoom & crop position per photo.
- Cut guides, frame color, Polaroid/Frame presets.
- Export to **PDF** and **PNG per page**, or **ZIP of all pages**.
- Undo/Redo (Ctrl+Z / Ctrl+Y), Light/Dark mode, ID/EN language switch.
- Export & Import layout settings to/from a **JSON** file.

## Canvas Edit Toolbar

The toolbar bar under the header (can be hidden/shown with the **🧰** button in the header; its state persists in `localStorage`) holds all the controls for manually editing the photo-box layout:

- **Undo / Redo** — ↩/↪ buttons, same as Ctrl+Z / Ctrl+Y.
- **✏️ Edit Layout: ON/OFF** — toggles edit mode, paired with a **scope** dropdown (`Halaman ini saja` "This page only" / `Semua halaman` "All pages") that decides whether changes apply only to the current page or to every page at once.
- **🔄 Rotate Kotak** (Rotate Box) — rotates the box (and its contents) 90° for the selected box(es).
- **🔄 Rotate Foto** (Rotate Photo) — rotates **only the photo** 90° inside the box (the box's own size/orientation stays the same).
- **↔ Flip Foto H** / **↕ Flip Foto V** — mirrors the photo horizontally/vertically inside the selected box(es).
- **✥ Crop Drag** — click-and-drag mode directly on a box to adjust the photo's crop position. While this mode is active and a box is selected, the **arrow keys** can be used to nudge the crop position in small steps.
- **🖐️ Hand Tool** — drag-to-pan mode for the canvas view (right-click+drag also always works, in any mode).
- **Sheet zoom controls** — −/+ buttons plus a **Fit ⇄ 100%** indicator (click to toggle); Ctrl+Scroll on the preview also zooms, as do Ctrl +/Ctrl −/Ctrl 0 on the keyboard.
- **➕ Foto + / ➖ Foto -** — zoom the photo in/out within the selected box; **🎯 Reset Foto Pan** resets the pan position back to center.
- **Snap Kotak** (Snap Boxes) — boxes automatically snap to other boxes while dragging.
- **Snap Grid** — snaps to a grid whose spacing (mm) is set in the number field next to it.
- **📐 Snap Cut-Guide** — snaps specifically to mid-gap cut-guide positions, meant to be used together with the Cut Guide Style "Garis di Tengah Jarak" / "Tanda Potong di Tengah Jarak" (mid-gap line/cut-mark) so spacing between boxes stays exactly matched to Box Spacing.
- **↺ Reset Terpilih / Reset Halaman Ini / Reset Semua Halaman** — resets box position & transforms (rotation/flip/pan): only the selected boxes, all boxes on the current page, or all boxes on every page.
- **Align (Ratakan)** — aligns the selected boxes to each other: Left, Center H, Right, Top, Center V, Bottom (needs at least 2 selected boxes), plus **Distribute H / Distribute V** to space them evenly (needs at least 3 boxes).
- **Align to Paper (Ratakan ke Kertas)** — aligns the selected box(es) to the edges/center of the paper's print area (Left/Center H/Right/Top/Center V/Bottom, needs at least 1 box). A **"Sebagai Grup"** (As a Group) checkbox controls whether selected boxes are aligned together as one group (keeping their relative positions) or each individually.
- **Arrange (Urutan / z-order)** — Bring to Front / Forward One / Backward One / Send to Back, controlling which box appears on top when boxes overlap.
- **✕ Hapus Pilihan** (Clear Selection) — clears the current box selection.
- **☰ Select** — multi-select mode: clicking a box adds/removes it from the selection (behaves like holding Shift continuously), while drag-to-select still works as usual.
- A selection-count indicator is shown at the far right of the toolbar.

The header also includes page navigation (**‹ Prev** / **Next ›** with a "Page X / Y" indicator), the language toggle (**ID/EN**), and the light/dark theme toggle — all independent of the edit toolbar above.

### Keyboard Shortcuts

| Shortcut | Function |
|---|---|
| `Ctrl/Cmd + Z` | Undo |
| `Ctrl/Cmd + Y` or `Ctrl/Cmd + Shift + Z` | Redo |
| `Ctrl/Cmd + Scroll` on the preview | Zoom the sheet view |
| `Ctrl/Cmd + +` / `Ctrl/Cmd + -` | Zoom the sheet view in/out |
| `Ctrl/Cmd + 0` | Toggle Fit ⇄ 100% |
| Arrow keys (↑↓←→) | Nudge the photo crop position in small steps — only active while **Crop Drag** mode is on and a box is selected |

## New Feature: Auto Crop Face (AI)

Located in the **"🤖 Auto Crop Wajah (AI)"** card, right below the "Foto Sumber" (Source Photos) panel.

How it works:
1. Detects facial landmarks (eyes, forehead, chin) using the **MediaPipe Face Landmarker** model.
2. Levels head tilt (automatic rotation based on eye position).
3. Computes the crop area automatically based on:
   - **Head Height vs. Box** — the proportion of head height relative to the photo box height.
   - **Top Margin** — the distance from the crown of the head to the box's top edge.
   - **Estimated Hair Above Forehead** — compensation since the forehead landmark point isn't the true crown of the head (hair isn't detected by the model).
4. The auto-crop result follows whatever **Photo Box Size** is currently set in the "Ukuran Kotak Foto" (Photo Box Size) card — so there's no separate size preset; everything stays consistent with the print layout you're building.
5. The resulting zoom and pan values are fed directly into the main app's built-in crop system (still fully adjustable manually via the usual ⚙ button).

Per-photo controls:
| Button | Function |
|---|---|
| 🤖 | Auto-crop this photo only |
| ✂️ | Remove this photo's background (see the "Background Removal (AI)" section below) |
| 🗘 | Restore the original photo (undo the auto-crop **and/or** background-removal result) — only appears once a photo has been processed by AI |
| ⚙ | Manual zoom/pan adjustment (built-in to the app) |
| 🗎 | Fill a target number of sheets (built-in to the app) |
| ✕ | Remove photo |

The **"⚙️ Auto Crop Semua Foto"** (Auto Crop All Photos) button processes the entire photo list sequentially.

Status badges shown on each photo row:
- `🤖…` — detecting
- `🤖✓` — success
- `🤖✓*` — success, but zoom was clamped (the required face area needs a wider crop than the current box aspect ratio can show)
- `🤖⚠` — no face detected (the photo can still be adjusted manually as usual)

---

## New Feature: Background Removal (AI)

The **✂️** button on every photo row (next to the 🤖 button) automatically removes the photo's background, producing a photo with a **transparent** background (alpha-channel PNG).

How it works:
1. Uses the **MediaPipe Image Segmenter (selfie segmenter)** model to distinguish the person from the background on a per-pixel basis (a 0–1 confidence mask).
2. The photo itself is always drawn at **full/original resolution** — only the mask/alpha (which the model outputs at a lower resolution) is upscaled, so photo sharpness never degrades.
3. Since the app already has a **Photo Background Color** setting (`photoBgColor`), the transparency produced by background removal is automatically "filled in" with whatever background color you've chosen (e.g. red/blue for official passport photos) when rendered into the layout/PDF/PNG — no extra step needed.
4. The **🗘 (restore original photo)** button undoes both the background-removal result and any auto-crop result, since both overwrite `im.img`/`im.url` and are tracked the same way as auto-crop (the original photo stays safe in `im.origImg`).

Status badges shown on each photo row:
- `✂️…` — processing
- `✂️✓` — background successfully removed
- `✂️⚠` — failed to remove background (check your internet connection / model status)

Quality notes:
- Best results come from photos with a background that contrasts reasonably well against the person/clothing. Backgrounds close in color to skin/clothing may sometimes need manual correction (e.g. retaking the photo against a plain background).
- Cut edges (especially hair) will look slightly soft — this is normal for any AI-based background-removal tool, not a sign of a blurry photo; the photo's own resolution stays fully intact (see point 2 above).

---

## Internet Connection Requirement

The AI model is **not bundled in the file** — it's loaded from a CDN when the page opens:

- `https://cdn.jsdelivr.net/npm/@mediapipe/tasks-vision@0.10.14/...` (library + WASM runtime, shared by both the Auto Crop Face and Background Removal features)
- `https://storage.googleapis.com/mediapipe-models/face_landmarker/...` (the face-detection model file, for Auto Crop)
- `https://storage.googleapis.com/mediapipe-models/image_segmenter/selfie_segmenter/...` (the person/background segmentation model file, for the ✂️ Background Removal feature)

If this fails, the AI card will show **"❌ Gagal memuat model..."** ("Failed to load model..."), and you'll typically see a `Failed to fetch` error in the console. All other layout/print features keep working normally without this connection.

> **Note:** the status for the Auto Crop Face model and the Background Removal model are both shown in the same status line (`aiEngineStatus`) in the UI. Since both are loaded through separate modules in parallel, whichever one finishes loading **last** is the message you'll see — it doesn't mean the other one failed. Check the Console (F12) if you need each status separately.

Common causes of failure:
1. No internet connection when the page loads.
2. The file is opened directly as `file://...` — some browsers restrict fetches from local files. Fix: serve it through a local server, e.g. `python3 -m http.server`, then open `http://localhost:8000/autopasfoto.html`.
3. An ad-blocker / privacy extension / corporate firewall blocking `cdn.jsdelivr.net` or `storage.googleapis.com`.

---

## Export & Import Settings (JSON)

The **"⬆ Export Pengaturan"** / **"⬇ Import Pengaturan"** (Export/Import Settings) buttons save/load the layout configuration to/from a `.json` file, including:

- Paper size, box size, gap, margins, colors, fill mode, guides, etc. (all of the app's built-in settings).
- The 3 Auto Crop AI sliders: `aiHeadRatio`, `aiTopMargin`, `aiHairExt`.

**Not included in the save:** the photo list itself (the image files) and each photo's AI status (`aiStatus` for auto-crop, `bgStatus` for background removal) — this is because image files can't be automatically embedded into the settings JSON. After reloading the page or importing settings, photos need to be re-uploaded, after which "Auto Crop Semua Foto" / per-photo background removal can be re-run if needed.

---

## Technical Notes (for further development)

- The AI model is loaded through a separate `<script type="module">`, exposing `window.faceAI = { ready, model, detect() }` so it can be used from the main (non-module) script.
- The core logic lives in the `AI AUTO CROP` section of the main script:
  - `aiRotateImageToCanvas()` — rotates the image onto a new canvas so the eyes are level.
  - `aiTransformPoint()` — transforms landmark coordinates into the rotated canvas's coordinate system.
  - `autoCropImage(im)` — the full pipeline: detect → rotate → compute crop rect → convert to `zoom/offX/offY` matching the main app's `drawCover()` scheme.
  - `autoCropAllImages()` — batches the process across all photos.
- The auto-cropped (already rotated) photo is stored as a new `<img>` element (built from `canvas.toDataURL()`), rather than overwriting the original. The original photo is kept in `im.origImg` for the 🗘 button and re-detection (detection always runs from the original photo, not a previous rotation result, to avoid compounding rotation error).
- `aiImageCache` (a `Map` of `url → Image`) keeps every `<img>` element ever created, because the app's built-in Undo/Redo system stores snapshots as a **JSON string** — an `<img>` object can't be serialized directly to JSON, so the snapshot only stores the `url` (data URL) and looks the actual `<img>` element back up from the cache when undo/redo runs.
- The app's built-in zoom UI range is `1×`–`3×` (you can't "zoom out" below the default cover crop); if the required face area is wider than that, the zoom value is automatically clamped to `1×` and flagged with `🤖✓*`.
- The Background Removal feature is loaded through a separate `<script type="module">`, exposing `window.bgRemovalAI = { ready, model, removeBackground(imgEl) }` — the same pattern as `window.faceAI`, but using an `ImageSegmenter` model (instead of `FaceLandmarker`), with `outputConfidenceMasks: true`.
  - `removeBgImage(im)` — the pipeline: wait for the model to be ready → `removeBackground()` → the resulting PNG data URL is loaded into a new `<img>` → overwrites `im.img`/`im.url` (added to the same `aiImageCache` as auto-crop) → updates the `bgStatus` badge.
  - `bgBadge(status)` — renders the status badge (`processing`/`ok`/`fail`) on the photo row, alongside auto-crop's `aiBadge(status)`.
  - Inside `removeBackground()`, the model's output mask (low resolution) is upscaled **separately** from the original photo (which is always drawn at full resolution), then combined as the alpha channel — so photo sharpness doesn't degrade to match the mask's resolution.
- `drawCoverRotated(ctx,img,dx,dy,dw,dh,zoom,offX,offY,rotDeg)` — the single drawing function used for the **"Rotate (Tilt)"** slider (used for page rendering, the live preview, and PDF/PNG export alike, so all three stay consistent). The photo is drawn `cover`-fit and then rotated by `rotDeg` degrees around the box's center, `clip()`-ed to the box area (dw×dh) so the tilt never bleeds onto the frame or neighboring boxes. Before rotating, the destination rect (dw,dh) is auto-scaled by a factor `s = |cos θ| + max(dw/dh, dh/dw) × |sin θ|` — the minimum scale needed for the rotated rect to still fully cover the original (dw×dh) box at any angle, preventing uncovered box corners (the "diagonal white triangle" bug). The existing `zoom`/`offX`/`offY` crop values are then applied as-is on top of that already-scaled rect.

---

## Other UI Improvements

- **Left panel widened** from 400px → 460px, so labels in the Auto Crop AI card (e.g. "Margin Atas (Ubun ke Tepi)") no longer get clipped/wrapped onto 2 lines.
- **Sharper preview canvas rendering**: preview raster resolution raised from a base of 150dpi to 300dpi, multiplied further by the screen's `devicePixelRatio` (capped at 2×) — so it no longer looks blurry on retina/high-DPI screens or when zoomed in. This does not affect PDF/PNG export resolution (those already use whatever DPI you select separately).
- **Fixed the "Rotate (Tilt)" slider — the diagonal white/background triangles at the corners are now gone.** This slider (in the per-photo ⚙ panel, including on top of an Auto Crop Face AI result) smoothly tilts the photo by degree inside its box. Previously, tilting the photo at any angle left the box's own corners no longer covered by the photo, so the background color (`photoBgColor`) or plain white showed through diagonally at the corners. The photo's zoom is now auto-compensated based on the tilt angle — the more it's tilted, the more it's scaled up just enough — so the box stays fully covered at any angle, the same way the Straighten tool works in Lightroom/Photoshop.

---

## Running 100% Offline (`autopasfoto-offline.html`)

Alongside `autopasfoto.html` (which loads every library from a CDN), there's also an **`autopasfoto-offline.html`** version that points to local files in a `libs/` folder, so it can be used with no internet connection at all.

### Folder structure you need to set up

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
            └── (the entire contents of the CDN's wasm folder, as-is)
```

### How to populate the `libs/` folder

1. **jspdf.umd.min.js**
   Download from `https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js` → save as `libs/jspdf.umd.min.js`.

2. **jszip.min.js**
   Download from `https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js` → save as `libs/jszip.min.js`.

3. **MediaPipe (Auto Crop AI feature)** — easiest via npm on a machine that's online:
   ```bash
   npm install @mediapipe/tasks-vision@0.10.14
   ```
   Then copy:
   - `node_modules/@mediapipe/tasks-vision/vision_bundle.mjs` → `libs/mediapipe/vision_bundle.mjs`
   - the entire contents of `node_modules/@mediapipe/tasks-vision/wasm/` → `libs/mediapipe/wasm/` (this folder contains several `.wasm`/`.js` files — copy **all of them**, not just one)
   - manually download the face-detection model from `https://storage.googleapis.com/mediapipe-models/face_landmarker/face_landmarker/float16/1/face_landmarker.task` → save as `libs/mediapipe/face_landmarker.task` (this file is not included in the npm package and must be fetched separately).
   - manually download the background-removal model (for the ✂️ feature) from `https://storage.googleapis.com/mediapipe-models/image_segmenter/selfie_segmenter/float16/latest/selfie_segmenter.tflite` → save as `libs/mediapipe/selfie_segmenter.tflite` (also not included in the npm package, same as the face-detection model).

4. **Google Fonts (optional)** — removed in the offline version. Without it, the layout still looks normal; the browser automatically falls back to a system font in place of `DM Mono`/`Syne`. If you want an identical look, download the `.woff2` font files and add a manual `@font-face` block in the `<style>` section.

### ⚠️ Must be opened through a local server, not by double-clicking the file

Because this app uses `<script type="module">` and `fetch()` (MediaPipe fetches the wasm files and model via fetch), browsers will **block those requests** if the file is opened directly as `file://...` (blocked by the browser's CORS policy). Run a simple static server in the project folder first, for example:

```bash
cd project-folder
python3 -m http.server 8000
```

Then open `http://localhost:8000/autopasfoto-offline.html` in your browser. Once all the `libs/` files above are correctly in place, every feature — including Auto Crop Face AI — will work with no internet connection at all.

### How to verify the installation is correct

- Open DevTools (F12) → the **Console** and **Network** tabs while the page loads.
- There should be no requests going out to external domains (`cdn.jsdelivr.net`, `storage.googleapis.com`, etc.) — everything should point to local `libs/...` paths.
- The **"🤖 Auto Crop Wajah (AI)"** card will show **"✅ Model hapus background siap"** ("Background-removal model ready") or **"✅ Model AI siap digunakan"** ("AI model ready") — whichever finishes loading last, see the note in the "Internet Connection Requirement" section — once `libs/mediapipe/` is complete and correct, including `selfie_segmenter.tflite` for the ✂️ feature.

---

## Known Limitations

- Face detection only supports **1 face per photo** (`numFaces: 1`); if a photo contains more than one face, the result may not be what you expect.
- The "crown of the head" estimate (`hairExt`) is a geometric approximation, not actual hair detection — it's worth double-checking manually for official print output (passports, legal documents, etc.).
- Background Removal (✂️) uses a general-purpose segmentation model (not one specialized for fine hair/portrait detail); soft hair edges or a background color close to skin/clothing tone can produce a less precise cutout that's worth checking manually.
- The Auto Crop Face and Background Removal model-status messages share a single status line in the UI (`aiEngineStatus`) — only the message from whichever model finished loading last is shown on screen, even though both load/run independently.
- Requires an active internet connection every time the page loads (the model isn't permanently cached in every browser) — **except** when using the `autopasfoto-offline.html` version with a fully populated `libs/` folder (see "Running 100% Offline" above).
- Undo/Redo doesn't track photos being added/removed — it only stores qty/zoom/pan/AI status for photos already present in that session (matching the original app's behavior).
