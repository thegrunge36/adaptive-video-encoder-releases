# 🎬 Adaptive Video Encoder

> **The H.265 encoder that doesn't break your Dolby Vision.**

[![Discord](https://img.shields.io/badge/Discord-Join-5865F2?logo=discord&logoColor=white)](https://discord.gg/UHrEn2H6jD) [![Buy me a coffee](https://img.shields.io/badge/Buy%20me%20a%20coffee-PayPal-00457C?logo=paypal&logoColor=white)](https://paypal.me/thegrunge45)

---

## Re-encode your video library without quality compromise

You have a video library full of 1080p Blu-rays, 4K Dolby Vision rips, HDR10 or HLG sources. You want to re-encode to H.265 to reclaim terabytes — without destroying the metadata that makes your movies display correctly on your OLED.

**The problem:** Most H.265 tools strip out Dolby Vision Profile 7 metadata or smooth grain by default. Manual ffmpeg requires hours of testing to find the right parameters — and those parameters change for every video (grain, noise, motion, complexity).

**The solution:** Adaptive Video Encoder analyzes each video frame by frame *before* encoding, automatically picks the best x265 parameters, and fully preserves your Dolby Vision (Profile 5, 7, 8.x), HDR10 and HLG metadata.

> 💡 **Philosophy:** Adaptive Video Encoder prioritizes **maximum preservation of detail, grain, and HDR metadata** over aggressive compression. The goal is near-remux quality, not the absolute best size/quality ratio.

---

## 🎯 Built for you if...

**1080p Blu-ray libraries:**
- You archive 1080p Blu-ray remuxes and want to preserve film grain (horror movies, classics, 35mm auteur films)
- You have HDR10 1080p sources that generic encoders handle poorly
- You want to preserve every fine detail of complex scenes (action, fantasy, sci-fi)

**4K UHD libraries:**
- You archive UHD Blu-rays with Dolby Vision and want maximum quality
- You handle HDR10 or HLG without manually calibrating each film

**All formats:**
- You value image quality over disk space savings
- You're comfortable with the command line
- You're tired of tweaking x265 parameters and comparing 12 versions of the same film

## ⚠️ Not for you if...

- You're looking for maximum compression to save disk space
- You mostly encode simple SDR content without grain (recent indoor comedies, smooth animation, talking heads) — for those cases, simpler tools often give better compression ratios
- You want a GUI
- You need fast encoding (the tool prioritizes quality, not speed)

---

## ⚡ Why a dedicated adaptive encoder?

| | Generic encoders | Manual ffmpeg | **Adaptive Video Encoder** |
|---|---|---|---|
| Dolby Vision Profile 7 | ❌ Broken | ⚠️ Possible with `dovi_tool` + scripting | ✅ Automatic |
| Grain preservation | ❌ Smoothed by default | ⚠️ If you know what to flag | ✅ Preserved automatically |
| Settings adapted *per video* | ❌ Fixed presets | ⚠️ If you test yourself | ✅ Frame-by-frame analysis |
| HDR10 / HLG preserved | ⚠️ Sometimes | ⚠️ If you know what to flag | ✅ Always |
| Black bar detection | ✅ | ⚠️ Manual | ✅ Automatic |
| Setup time | 5 min | 1-3 h per film | **0 min** |

---

## 🎞️ Particularly excellent on 1080p Blu-rays

Many users mistakenly think this tool is only for 4K. **It's not.** Adaptive Video Encoder shines particularly well on 1080p Blu-ray remuxes for 3 reasons:

**1. Film grain preservation.** Classic films, horror movies, recent 35mm auteur films have grain that's part of their visual identity. Most encoders smooth it by default. Adaptive Encoder detects and preserves it.

**2. Adaptive complex scene detection.** On a 1080p action film, fight scenes have radically different complexity than dialogue. Frame-by-frame analysis adjusts x265 parameters accordingly, where generic encoders use the same settings start to finish.

**3. 1080p HDR10 metadata preservation.** Some recent Blu-rays have HDR10 in 1080p. Adaptive Encoder preserves everything: master display, MaxCLL/MaxFALL, color primaries.

**Less relevant for:** recently-shot digital content with clean image (romantic comedies, sitcoms, indoor documentaries). Those sources have neither grain nor complex detail to preserve.

---

## 🧠 Why CPU encoding instead of GPU?

Short answer: **NVENC, QuickSync and AMF are designed for speed, not quality.**

| | GPU (NVENC / QSV / AMF) | **CPU (x265)** |
|---|---|---|
| Encoding speed | ⚡⚡⚡ Fast | 🐢 Slow |
| Quality per bit | ⚠️ Decent | ✅ Excellent |
| Final file size | ⚠️ Larger | ✅ Smaller |
| Ideal use case | Live streaming, real-time capture | **Archival, video library** |

**For archiving a library, speed doesn't matter — you encode once, watch 100 times.**

---

## ✨ What it does

- 🔍 **Adaptive analysis** — detects noise, grain, complexity, edge density to tune x265
- 📺 **Dolby Vision Profile 5, 7, 8.x** — metadata extracted, preserved, reinjected
- 🎨 **HDR10 and HLG** — color primaries, transfers, master display, MaxCLL/MaxFALL preserved
- 🎞️ **Grain preservation** — 35mm film, horror movies, grainy sources handled automatically
- ✂️ **Smart crop** — detects black bars without accidentally cutting content
- 🔊 **All audio and subtitle tracks** copied by default, zero loss
- 🎞️ **Supported formats** — MKV, MP4, MOV, AVI, MXF, WebM, M4V, TS
- 📐 **Resolutions** — 480p to 8K (excellent for 1080p AND 4K)
- 📦 **Single binary** — ffmpeg and ffprobe bundled. No dependencies to install.

---

## 💻 Platform support

| Platform | Status | Notes |
|---|---|---|
| 🐧 Linux (x64) | ✅ Supported | Ubuntu 22.04+, Debian 12+, Fedora 40+ |
| 🪟 Windows 10/11 (x64) | ✅ Supported | PowerShell or CMD |
| 🍎 macOS (Apple Silicon) | ✅ Supported | M1, M2, M3 — native arm64 binary |

---

## ☕ This tool is free — buy me a coffee if it helped!

Adaptive Video Encoder is completely free to use. If it saved you time or improved your library, a small coffee is always appreciated — but never required.

👉 **[Buy me a coffee](https://paypal.me/thegrunge45)** — totally optional, always appreciated ☕

💬 **Questions or feedback? Join the [Discord](https://discord.gg/UHrEn2H6jD)** — happy to help.

---

## ⚙️ Installation & requirements

ffmpeg and ffprobe are bundled — no need to install them separately. However, **two tools must be installed** before using the encoder:

### 1. mkvmerge — required for MKV output

| Platform | Install |
|---|---|
| 🐧 Linux | `sudo apt-get install mkvtoolnix` |
| 🍎 macOS | `brew install mkvtoolnix` |
| 🪟 Windows | Download [MKVToolNix](https://mkvtoolnix.download/downloads.html), install it, then copy `mkvmerge.exe` from `C:\Program Files\MKVToolNix\` into the **same folder** as `adaptive-encoder.exe` |

### 2. dovi_tool — required for Dolby Vision

| Platform | Install |
|---|---|
| 🐧 Linux | `wget https://github.com/quietvoid/dovi_tool/releases/download/2.3.1/dovi_tool-2.3.1-x86_64-unknown-linux-musl.tar.gz && tar -xzf dovi_tool-*.tar.gz && chmod +x dovi_tool && sudo mv dovi_tool /usr/local/bin/` |
| 🍎 macOS | Download from [github.com/quietvoid/dovi_tool/releases](https://github.com/quietvoid/dovi_tool/releases), then `chmod +x dovi_tool && sudo mv dovi_tool /usr/local/bin/` |
| 🪟 Windows | Download `dovi_tool-x86_64-pc-windows-msvc.zip` from [github.com/quietvoid/dovi_tool/releases](https://github.com/quietvoid/dovi_tool/releases), extract and place `dovi_tool.exe` in the **same folder** as `adaptive-encoder.exe` |

Without `dovi_tool`, the encoder falls back to HDR10 only.

### 3. First launch — macOS only

macOS blocks unsigned binaries. Run this **once** after downloading:

```bash
xattr -d com.apple.quarantine ./adaptive-encoder
chmod +x ./adaptive-encoder
```

After that, macOS will never warn about this file again.

---

## 🚀 Quick start

```bash
# 🐧 Linux / 🍎 macOS
./adaptive-encoder "my_movie.mkv"

# 🪟 Windows (PowerShell or CMD)
.\adaptive-encoder.exe "my_movie.mkv"
```

> 💡 **Windows tip:** Shift + right-click in the folder → "Open PowerShell window here"

**Test mode — analyze without encoding:**
```bash
./adaptive-encoder "my_movie.mkv" --dry-run
```

---

## 🗂️ Batch encode an entire library

```bash
# 🐧 Linux / 🍎 macOS
for file in *.mkv; do
    ./adaptive-encoder "$file"
done
```

```powershell
# 🪟 Windows
Get-ChildItem *.mkv | ForEach-Object {
    .\adaptive-encoder.exe $_.FullName
}
```

> 💡 **Tip:** run with `--dry-run` on a single file first to verify Dolby Vision and HDR are correctly detected.

---

## 📖 All options

```
-h, --help                            Display this help message and exit
-o, --output OUTPUT                   Output video file (default: <input>_adaptive.mkv)
--max-samples MAX_SAMPLES             Max number of frames to sample for analysis
--target-hours TARGET_HOURS           Fallback duration (h) if ffprobe cannot determine it
--max-bitrate MAX_BITRATE             Force VBV max bitrate (kbps)
--vbv-bufsize VBV_BUFSIZE             Optional VBV buffer size (kbits)
--no-vbv                              Disable automatic VBV bitrate capping
--no-veryslow                         Limit presets to 'slower' instead of 'veryslow'
--no-audio                            Remove audio tracks (copied by default)
--no-subs                             Remove subtitle tracks (copied by default)
--no-crop-detect                      Disable automatic black bar detection
--no-dolby-vision                     Ignore Dolby Vision metadata, encode as HDR10 only
--preserve-dv-profile                 Skip Dolby Vision if the source profile cannot be
                                      reproduced by x265 (e.g. profile 7.x), instead of
                                      silently downgrading to 8.1. Outputs HDR10 in that case
--force-tune {grain,animation}        Force x265 tune preset. 'grain' preserves film grain
                                      structure (higher psy-rd). 'animation' optimizes for
                                      flat areas and sharp edges. Default: auto-adaptive
--crop-samples CROP_SAMPLES           Number of time points for crop detection
--no-denoise                          Disable adaptive noise reduction (auto-enabled for noisy sources)
--denoise-strength DENOISE_STRENGTH   Override denoise strength (0.0=off, 1.0=max). Default: auto
--denoise-preserve-grain              Gentler denoise that preserves some film grain texture
--denoise-engine {nlmeans,bm3d,hybrid}
                                      Force a specific denoise engine instead of automatic
                                      selection. bm3d for maximum quality (3-5x slower),
                                      nlmeans for speed, hybrid for film grain
--verbose                             Display technical details of adaptive analysis
--dry-run                             Display analysis and command without encoding
```

---

## ❓ FAQ

**What platforms are supported?**
Windows 10/11 (x64), Linux (x64), and macOS Apple Silicon (M1/M2/M3). ffmpeg and ffprobe are bundled — only mkvmerge and dovi_tool need to be installed separately.

**Is this only for 4K?**
No, the tool is excellent for 1080p too. Particularly on Blu-ray remuxes with film grain (classics, horror, 35mm auteur films) or complex scenes (action, sci-fi).

**Do I need to install ffmpeg separately?**
No. ffmpeg and ffprobe are bundled inside the binary. Download, run, done.

**Dolby Vision doesn't work — why?**
`dovi_tool` must be installed separately (see Installation above). Without it, the encoder falls back to HDR10 only.

**Does Profile 7 → 8.1 conversion work?**
Yes, it's the default. Profile 7 (FEL/MEL) is extracted and reinjected as 8.1, compatible with most modern Dolby Vision players.

**Why are my files larger than with other encoders?**
Intentional design choice — maximum detail and HDR metadata preservation. To cap file size, use `--max-bitrate`.

**Encoding speed?**
The tool uses x265 `slower` or `veryslow` presets — not a fast encoder, a *good* one. For faster encoding use `--no-veryslow`.

**What if it doesn't work for my files?**
Open an issue on GitHub or ask on Discord — happy to help.

---

## 📧 Support

- 💬 **Discord** (fast replies): [https://discord.gg/UHrEn2H6jD](https://discord.gg/UHrEn2H6jD)
- 📧 **Email**: [osx300@gmail.com](mailto:osx300@gmail.com)
- ☕ **Buy me a coffee** (optional): [paypal.me/thegrunge45](https://paypal.me/thegrunge45)

