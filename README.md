# NADIA

A local AI roleplay companion for Windows with **voice**, **image generation**, and a
**phone (AFK) mode** — the chat brain, image engine, and voice all run on your own PC.
Cloud is used only for optional speech‑to‑text, image understanding, and web search
(your own free API keys).

> The app window and launcher are branded **Jarvia** (the executable is `Jarvia.exe`).
> "NADIA" is the project / one of the built‑in characters.

---

## Download & install (first‑time users)

1. **Download all parts.** Because the build is larger than GitHub's 2 GB‑per‑file
   limit, the download is split. From the [Releases](../../releases) page grab **all
   four** parts plus the rejoin helper, into one folder:
   `NADIA-Release.zip.001`, `.002`, `.003`, `.004`, and `Rejoin.bat`.

2. **Rejoin & extract.** Double‑click **`Rejoin.bat`** — it rebuilds
   `NADIA-Release.zip`. Right‑click that → **Extract All** to a normal folder
   (e.g. `Desktop\Jarvia`; avoid `Program Files`). See `SPLIT-README.txt` for details
   and an optional checksum.

3. **Double‑click `First-Run.bat`.**
   Windows will ask for **Administrator** permission — click **Yes**.
   This unblocks the files from the zip (mark‑of‑the‑web), sets a safe PowerShell
   policy, fixes folder permissions, and checks the bundled ComfyUI + Qwen3‑TTS engines.
   *(`First-Run-Setup.bat` is the same step under an older name.)*

4. **Double‑click `Jarvia.exe`** to start chatting.

If setup fails, right‑click **`First-Run.bat` → Run as administrator** and approve the prompt.

## First‑run downloads (one time, needs internet)

The release zip ships the **app + engines**, not the multi‑GB model weights — those
download themselves the first time you use each feature, so the download stays small:

| Feature | When it downloads | Size |
|---|---|---|
| Chat (language model) | First launch | ~8 GB |
| Image generation | First time you ask for a picture | ~6.5 GB |
| Voice (spoken replies) | First time you turn voice on | ~4.5 GB |

Chat works while these download. Image and voice need an **NVIDIA GPU** (12 GB card is the
realistic minimum, since they run alongside the chat brain).

## Optional free API keys

Two **free** keys (no credit card) unlock the cloud‑assisted features. See
`docs\SETUP-KEYS.txt` inside the install folder for step‑by‑step instructions.

| Key | Powers | Get it |
|---|---|---|
| `GROQ_API_KEY` (`gsk_…`) | speech‑to‑text + image understanding | https://console.groq.com/keys |
| `TAVILY_API_KEY` (`tvly-…`) | web search | https://app.tavily.com |

Set them once as Windows environment variables, then restart the app:

```powershell
setx GROQ_API_KEY "paste-your-gsk-key-here"
setx TAVILY_API_KEY "paste-your-tvly-key-here"
```

Typing always works without any keys.

## Features

- **Local chat** with persistent memory + a relationship that survives "New conversation".
- **Image generation** — ask "show me your outfit" and the character draws herself
  (local ComfyUI / SDXL). Starts itself the first time you ask.
- **Voice** — optional spoken replies (local Qwen3‑TTS), **muted by default**, with a
  graceful fallback to text if the voice server is busy or still warming up.
- **Phone / AFK mode** — chat from your phone over a private [Tailscale](https://tailscale.com)
  network (no password, never exposed to the open internet).
- **Web search** (Tavily) and **"turn me up"** music launch.

### Control panel (icon buttons under the portrait)

A **3×3 grid** of round buttons sits under the character portrait. Hover any of them for a
tooltip. A bright/filled icon means *on*; a dim/outline icon means *off*.

| | Left | Middle | Right |
|---|---|---|---|
| **Top** | **Voice** — turn spoken replies on/off (first unmute downloads the voice model) | **Narration** — plain dialogue vs. added *stage directions / narration* | **Template** — switch the image style template (Default vs. Alt) |
| **Middle** | **Go AFK** — start/stop the phone web server (shows the address to open) | **Image gallery** — grid of pictures she's generated, with save/copy | **Console** — hide/show the background command‑prompt window (eye icon) |
| **Bottom** | **New conversation** — fresh chat but **keeps** memory + relationship | **Quick reference** — in‑app help/cheatsheet | **ComfyUI** — start/stop the local image engine |

Below the grid is a small **status list** (ComfyUI, voice/TTS, Tavily) showing what's live.

## Requirements

- Windows 10/11, 64‑bit
- NVIDIA GPU recommended (required for voice and image generation; ~12 GB VRAM)
- Internet connection for the first‑run model downloads

## Troubleshooting

- *"not digitally signed"* → you skipped first‑run setup; run **`First-Run.bat`** once.
- Image generation OOM on a 12 GB card → open `comfyui\run_comfyui.ps1` next to
  `Jarvia.exe` and add `--lowvram` to the `$comfyArgs` line (commented right there).
- Voice stays silent → it's still downloading/warming, or the GPU is busy; replies fall
  back to text and nothing crashes.
