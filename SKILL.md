---
name: voice-pipeline
description: Pipeline for cleaning and transcribing voice messages and audio files (including ZIPs). Fully local Whisper + ClearVoice on macOS/Linux.
---

# Voice Pipeline

Automated audio cleaning (ClearVoice) and transcription (Whisper) for any audio input.

## Features
- **Auto-Processing:** Cleans and transcribes every audio file or ZIP of audio.
- **Deep Cleaning:** Uses ClearVoice (MossFormer2) for speech enhancement.
- **Local Only:** Runs Whisper locally (GPU/Metal/CPU) without cloud fallback.
- **Unpacker:** Automatically extracts and processes audio from ZIP files.
- **Always Enhance:** ClearVoice runs by default for every file.
- **Mapped Output:** Transcript filenames are mapped back to source filenames.
- **Skill Summary:** The assistant summarizes each transcript in the reply message.
- **Audio Export:** Saves cleaned + shortened MP3 in `~/transcripts`.
- **Runtime Discovery:** Detects installed Whisper/ClearVoice paths and reports missing deps with OS-specific install commands.

## Usage
The agent uses this skill automatically when audio is detected. You can also run it manually:

```bash
{baseDir}/scripts/process-audio <file_or_zip> [options]
```

Options:
- `--enhance`: Force ClearVoice cleaning.
- `--no-enhance`: Disable ClearVoice cleaning.
- `--language <lang>`: Language (`de` default). Use `auto` for automatic `de/en` detection.
- `--model <model>`: Whisper model (default: large-v3).
- `--allow-cpu-fallback`: Optional fallback to CPU if all GPU model attempts fail.
- `--check`: Verify dependencies.
- `--doctor`: Print detected runtime paths/devices.
- `--install`: Print OS-specific install commands (manual execution only).

## Requirements
- Python 3.9+
- FFmpeg
- unzip
- 4GB+ RAM (8GB+ recommended for large models)
- NVIDIA GPU or Apple Silicon (optional for speed)

## Install Resources
- `resources/install/macos.txt`
- `resources/install/linux-apt.txt`
- `resources/install/linux-pacman.txt`
- `resources/install/linux-dnf.txt`
- `resources/install/linux-zypper.txt`
