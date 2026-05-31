# Local Neural TTS -- Kokoro-82M Web App

A single-page web app that runs the **Kokoro-82M** neural text-to-speech
model entirely in your browser. No API keys, no cloud calls -- once the
model is cached, it works offline.

## How to use

1. Open `index.html` in a modern Chromium browser (Chrome 113+, Edge 113+).
   You can either double-click the file or, for best results, serve the
   folder over a local HTTP server (see below).
2. Click **Load model**. The first run downloads ~300 MB of model weights
   from the HuggingFace CDN; subsequent runs use the browser cache.
3. Type or paste text, pick a voice and speed, then click **Speak**.
4. Use **Save .wav** to export uncompressed audio, or **Save .mp3** to
   encode an MP3 (192 kbps stereo) locally in your browser using the
   bundled `lamejs.iife.js`. Both options run fully offline.

### Optional: serve over a local HTTP server

Some browsers handle ES module imports more reliably from `http://`
than from `file://`. From this folder:

```
python -m http.server 8000
```

then open <http://localhost:8000>.

## Requirements

- Chromium-based browser (Chrome, Edge, Brave, Opera, Arc).
- WebGPU recommended for speed (Chrome/Edge 113+). The app falls back
  to WebAssembly automatically if WebGPU is unavailable.
- ~300 MB of free disk/cache space for the model.
- Internet connection on first run only.

## What's in this folder

| File              | Purpose                                                       |
|-------------------|---------------------------------------------------------------|
| `index.html`      | The web app (HTML + CSS + JS).                                |
| `lamejs.iife.js`  | Bundled MP3 encoder (LGPL-3.0). Shipped unmodified.           |
| `INSTRUCTIONS.txt`| Plain-text quick start.                                       |
| `README.md`       | This file.                                                    |
| `LICENSE`         | Apache License, Version 2.0 -- full text.                     |
| `LICENSE.lamejs`  | LGPL-3.0 notice for the bundled `lamejs.iife.js`.             |
| `NOTICE`          | Required third-party attribution notices.                     |

## Privacy

All inference and MP3 encoding run locally in your browser. Your text and
the generated audio are never sent to any server. The only network
activity is the one-time model-weights download from the HuggingFace
public CDN.

## License

This web app (`index.html`, docs) is Copyright 2026 Omer Daniel <omer.daniel@solaredge.com> and is
licensed under the **Apache License, Version 2.0** -- see [`LICENSE`](LICENSE).
Required third-party attribution is in [`NOTICE`](NOTICE).

### Third-party components

- **Kokoro-82M** model weights -- Apache 2.0. Loaded at runtime from
  <https://huggingface.co/onnx-community/Kokoro-82M-v1.0-ONNX>.
- **kokoro-js** library -- Apache 2.0. Loaded at runtime from
  <https://cdn.jsdelivr.net/npm/kokoro-js@1.2.0>.
- **lamejs** (breezystack fork) -- **LGPL-3.0-or-later**. **Bundled**
  here as `lamejs.iife.js`, shipped unmodified from
  <https://www.npmjs.com/package/@breezystack/lamejs> v1.2.7.
  See [`LICENSE.lamejs`](LICENSE.lamejs). You may replace
  `lamejs.iife.js` with a different LGPL-compatible build.

### Modifications

`index.html` is an original work. It wraps `kokoro-js` and `lamejs` in a
UI but does not modify either, nor the Kokoro-82M model weights.

## Disclaimer

Distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF
ANY KIND, either express or implied. See the License for details.
