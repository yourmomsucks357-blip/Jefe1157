# JEFE — Local

JEFE configured to run against a **local model server on your own machine** (via llamafile). Self-contained `index.html`, no build step, talks to any OpenAI-compatible `/v1/chat/completions` endpoint. Preset to `http://127.0.0.1:8080`.

Best for privacy and zero cost. On older / low-power hardware (e.g. a 2013 Intel Mac on Big Sur), stick to a small model and expect a few tokens per second.

## Run the model (llamafile)

1. **Get the runtime** — download the file named `llamafile` from the [llamafile releases page](https://github.com/Mozilla-Ocho/llamafile/releases), then:
   ```bash
   chmod +x llamafile
   xattr -d com.apple.quarantine llamafile 2>/dev/null   # clears "unverified developer"
   ```
2. **Get a small model** (~2 GB):
   ```bash
   curl -L -o jefe-3b.gguf \
     "https://huggingface.co/bartowski/Dolphin3.0-Qwen2.5-3b-GGUF/resolve/main/Dolphin3.0-Qwen2.5-3b-Q4_K_M.gguf"
   ```
3. **Start it:**
   ```bash
   ./llamafile -m jefe-3b.gguf --host 127.0.0.1 --port 8080 --nobrowser
   ```
   (If a flag is rejected, `./llamafile -m jefe-3b.gguf` alone also serves on port 8080.)

## Use JEFE

- Open `index.html` (double-click is fine for local use — no hosting needed).
- The Server URL is already `http://127.0.0.1:8080`. Tap **Test connection**, pick the model, chat.

## Optional: host the page on GitHub Pages

Push `index.html` to a repo, then **Settings → Pages → Deploy from a branch → main → / (root)**. A Pages URL is HTTPS, and browsers allow it to reach `http://localhost`, so the local preset still works from the hosted page on the same machine.

## Notes

- RAM guide: 3B ≈ 4 GB free. With 16 GB you can try an 8B, just slower.
- The page only sends messages to the URL you set; settings stay in your browser.

MIT — see [LICENSE](LICENSE).
