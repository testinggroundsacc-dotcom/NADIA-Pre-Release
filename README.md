<div align="center">

# N.A.D.I.A

### Networked Assistant for Dialogue, Intimacy and Affection

*A local-first AI companion for the desktop — voiced, embodied, and persistent.*

`v0.1.0 · alpha` — dev build

<img src="docs/images/cover.png" width="360" alt="NADIA portrait">



</div>

---

## What is NADIA?

NADIA is a self-hosted AI companion application that runs on your own machine. She is not a wrapper around a cloud chatbot — the language model, the voice, and the image generation all run locally, on your own hardware.

She is built around three ideas:

- **She talks like a person, not a tool.** A carefully authored persona gives her a consistent voice — warm, unhurried, with her own judgement. She is dialogue-first; she is not a chirpy assistant reading search results back at you.
- **She is embodied.** NADIA has a fixed visual identity — an original character design — and can generate images of herself on request, so she has a face, not just a text box.
- **She remembers, and it matters.** Conversations build a persistent memory and an affinity/relationship system, so the relationship has continuity and changes over time rather than resetting every session.

![NADIA main window](docs/images/overview.png)

> **Project status — alpha.** This is an active, single-developer hobby project in early development. Things move fast and break occasionally. It is shared privately and is not yet intended for general release.

---

## Who built it

NADIA is designed and built by a single engineer — **Spades** — with an AI coding agent as the only other "hand" on the codebase. There is no team and no company behind her; the design choices, the code, and the writing are all one person's.

---

## Features

Each control below corresponds to one of the nine icons in NADIA's right-hand control panel.

### The control panel

A **3×3 grid** of icon buttons sits under the character portrait. A bright/filled icon means *on*; a dim/outline icon means *off*. Left to right, top to bottom:

| # | Control | What it does |
|---|---------|--------------|
| 1 | **Voice** | Turns NADIA's spoken voice on or off. The first time you unmute, the voice model (~4.5 GB) downloads once. |
| 2 | **Narration** | Switches narration mode — plain spoken dialogue vs. added *narration / stage directions* (e.g. *she smiles*). |
| 3 | **Template** | Switches the image style template (**Default** vs. **Alt**) used when she generates a picture. |
| 4 | **Go AFK** | Starts/stops the phone-companion (PWA) web server and shows the address to open on your phone. |
| 5 | **Image gallery** | Opens the grid of pictures she's generated for this character, with save / copy. |
| 6 | **Console** | Hides or shows the background command-prompt window (the eye icon) where download/engine progress appears. |
| 7 | **New conversation** | Starts a fresh chat but **keeps** memory + relationship — she still knows you. |
| 8 | **Quick reference** | Opens the in-app help / keyword cheatsheet. |
| 9 | **ComfyUI** | Starts/stops the local image engine (it also auto-starts the first time you ask for a picture). |

![Control panel](docs/images/control-panel.png)

<!-- If the panel screenshot above is out of date, drop a fresh one in docs/images/control-panel.png (same name) and it updates here automatically. -->

---

### Voice — local TTS with voice cloning

NADIA speaks in a consistent cloned voice using zero-shot voice cloning. Her voice is generated locally and streamed as she replies.

▶️ [Watch the voice demo on YouTube](https://youtu.be/oawfSDF4_gI)

---

### Self-image — she can show you her face
![NADIA self-image](docs/images/selfimage-1.png)

NADIA has a fixed character design and can generate images of herself on request — a portrait, a selfie, the two of you together — using a local image-generation pipeline. Her appearance stays consistent across generations.

![NADIA self-image](docs/images/selfimage-2.png)

<!-- TEMPLATE — add more example renders to show appearance consistency. Copy a line per image:
![example render](docs/images/selfimage-3.png)
![example render](docs/images/selfimage-4.png)
-->

---

### Vision — she sees what you show her

Paste or attach an image and NADIA can look at it and respond to what's there.

![Vision](docs/images/feature-vision.png)

---

### Memory & affinity — the relationship persists

NADIA builds a persistent memory of your conversations and tracks an affinity/favour relationship that changes over time, so continuity carries from one session to the next.

![Affinity panel](docs/images/affinity-1.png)
![Affinity panel](docs/images/affinity-2.png)
![Affinity panel](docs/images/affinity-3.png)

---

### Web reach — she can look things up

When something is beyond what she already knows or remembers, NADIA can reach out to the web to find it.

![Web reach](docs/images/feature-web.png)

---

### Phone / PWA companion client

A companion progressive-web-app client lets you talk to NADIA from your phone, connecting to the desktop app over the local network (via Tailscale).

![Phone / PWA client](docs/images/phone-1.png)
![Phone / PWA client](docs/images/phone-2.png)

---

## Tech stack

| Layer | What's used |
|-------|-------------|
| **Language model** | Local LLM inference, run on-device. |
| **Text-to-speech** | Qwen3-TTS with zero-shot voice cloning. |
| **Image generation** | ComfyUI pipeline (SDXL-class model) for NADIA's self-image. |
| **Speech-to-text** | Whisper (small.en) / Groq. |
| **Vision** | Image understanding for pasted/attached images. |
| **Web** | Web search/retrieval for out-of-knowledge queries. |
| **Desktop client** | Python application packaged as a standalone Windows build. |
| **Companion client** | FastAPI-served progressive web app for phone access. |

> Specific model files, weights, and reference audio are not included in the repository — they download themselves on first use.

---

## Getting started

NADIA ships as a ready-to-run Windows build on the [Releases](../../releases) page — no Python, no manual ComfyUI install. The engines are bundled; the multi-GB model weights download themselves the first time you use each feature.

### 1. Download all parts

The build is larger than GitHub's 2 GB per-file limit, so the download is split. From the latest [Release](../../releases), download **all** of these into one folder:

- `NADIA-Release.zip.001`
- `NADIA-Release.zip.002`
- `NADIA-Release.zip.003`
- `NADIA-Release.zip.004`
- `Rejoin.bat`
- `SPLIT-README.txt`

### 2. Rejoin & extract

Double-click **`Rejoin.bat`** — it stitches the parts back into `NADIA-Release.zip`. Right-click that → **Extract All** to a normal folder (e.g. your Desktop or `C:\`; avoid `Program Files`, and don't run it from inside the zip). You'll get a `Jarvia` folder. *(See `SPLIT-README.txt` for an optional checksum.)*

### 3. First-run setup (once, as Administrator)

Open the folder and double-click **`First-Run.bat`**. Click **Yes** at the Administrator prompt — it unblocks the downloaded files, sets a safe PowerShell policy, fixes folder permissions, and checks the bundled ComfyUI + Qwen3-TTS engines.

### 4. Launch

Double-click **`Jarvia.exe`** (the NADIA launcher). The first start downloads the chat brain (~8 GB, one time — you'll see a console window working), then it's ready: type to chat, or hold **Caps Lock** and talk.

### 5. Add two free keys (optional, ~2 min each)

NADIA uses two free API keys (no credit card) for cloud-assisted features:

- **Groq** (chat vision + speech-to-text): sign up at <https://console.groq.com> → <https://console.groq.com/keys> → "Create API Key" → copy the `gsk_…` key.
- **Tavily** (web search): sign up at <https://app.tavily.com> → copy your `tvly-…` key.

Open PowerShell (Start → type "PowerShell" → Enter) and run, pasting your own keys:

```powershell
setx GROQ_API_KEY "paste-your-gsk-key-here"
setx TAVILY_API_KEY "paste-your-tvly-key-here"
```

Close and reopen NADIA so it picks them up. Typing always works without any keys. Full details are in `Jarvia\_internal\docs\SETUP-KEYS.txt`.

### Optional extras (need an NVIDIA GPU)

- **Pictures** — just ask "show me your outfit" in chat. The first image downloads the art model (~6.5 GB) once.
- **Spoken replies** — click the **Voice** icon on the character panel. The first unmute downloads the voice (~4.5 GB) once.
- **Phone access** — install [Tailscale](https://tailscale.com/download) on PC + phone (free, same account), click **Go AFK** in the app, and open the address it shows on your phone.

### System requirements

- Windows 10/11, 64-bit.
- An NVIDIA GPU for voice and image generation (developed on an RTX 5080; ~12 GB VRAM is the realistic minimum, since image/voice run alongside the chat brain).
- An internet connection for the one-time first-run model downloads.

<!-- TEMPLATE — add a screenshot of the app's first-run / setup screen here if you want:
![first run](docs/images/setup.png)
-->

---

## Roadmap / notes

<!-- Optional: jot near-term intentions here — e.g. voice polish, additional personas,
     logo/branding, packaging. Keep it loose; it's a hobby project. -->

- Ongoing voice quality refinement.
- Additional persona work.
- Branding / app-icon finalisation (the packaged launcher is still named `Jarvia.exe`; a NADIA rename is planned).

---

<div align="center">

*NADIA — a dev-build experiment. Built by Spades.*

`v0.1.0 · alpha` · © 2026 Spades

</div>
