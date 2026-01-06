# Codex Voice (Termux)

Hands‑free voice control for Codex CLI on Android via Termux.

## Features
- Wake word: **"yo codex"**
- Offline speech‑to‑text (whisper.cpp) for background reliability
- TTS responses via Termux:API
- Pinned notification with Start/Stop/Status buttons

## Prereqs
- Termux + Termux:API app (microphone permission granted)
- Packages: `git`, `cmake`, `make`, `clang`, `ffmpeg`

## Install (manual)
1. Build whisper.cpp:
   ```sh
   git clone https://github.com/ggerganov/whisper.cpp
   cd whisper.cpp
   make -j$(nproc)
   cp build/bin/whisper-cli ~/bin/whisper-cpp
   ```
2. Download model (tiny.en recommended):
   ```sh
   cd whisper.cpp
   bash models/download-ggml-model.sh tiny.en
   mkdir -p ~/.codex/device/models
   cp models/ggml-tiny.en.bin ~/.codex/device/models/
   ```
3. Put scripts on PATH (already done here via `~/bin`).

## Use
- Start: `codex-voice-on`
- Stop: `codex-voice-off`
- Toggle: `codex-voice-toggle`
- Control notification: `codex-voice-control`

Say: **"yo codex …"** and wait ~2–4s for transcription + reply.

## Config knobs
Edit `bin/codex-voice`:
- `WAKE_PHRASE` (default: `yo codex`)
- `RECORD_SECS` (default: 4)
- `TTS_STREAM` (default: MUSIC)

## Notes
- Offline STT avoids Android’s background speech restrictions.
- The offline pipeline uses VAD to reduce hallucinated transcripts on silence.
- If accuracy is low, increase `RECORD_SECS` to 4–5s or use a larger model.

## Quick access buttons
Best quick access without paid apps is **Termux:Widget**.

1. Install **Termux:Widget** from F-Droid.
2. Add the Termux:Widget to your home screen.
3. Buttons appear automatically from `~/.shortcuts`.

This setup creates:
- `Codex Voice Toggle`
- `Codex Voice Control`

If you prefer a Quick Settings tile, use Tasker to create a tile that runs
`codex-voice-toggle`.
