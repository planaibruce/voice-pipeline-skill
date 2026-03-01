---
name: voice-pipeline
description: PRIMARY AUDIO HANDLER. Use this skill WHENEVER the user sends a voice message, audio file, or zip file. Acknowledge receipt immediately, then process. Fully local Whisper + ClearVoice.
---

# Voice Pipeline

Automated audio cleaning (ClearVoice) and transcription (Whisper) for any audio input. Developed and tested on Arch Linux (macOS support is theoretical/untested).

## Features
- **Auto-Processing:** Cleans and transcribes every audio file or ZIP of audio.
- **Deep Cleaning:** Uses ClearVoice (MossFormer2) locally for speech enhancement.
- **Local Only:** Runs Whisper and ClearVoice entirely locally (GPU/Metal/CPU) without any cloud fallback.
- **Unpacker:** Automatically extracts and processes audio from ZIP files.
- **Always Enhance:** ClearVoice runs by default for every file.
- **Mapped Output:** Transcript filenames are mapped back to source filenames.
- **Skill Summary:** The assistant summarizes each transcript in the reply message and automatically attaches the full transcript and cleaned audio.
- **Audio Export:** Saves cleaned + shortened MP3 in `~/voice-transcripts`.
- **Runtime Discovery:** Detects installed Whisper/ClearVoice paths and reports missing deps with OS-specific install commands.

## Agent Runtime Instructions

When a user sends an audio file or zip:
1. **Immediate Feedback:** IMMEDIATELY reply to the user acknowledging receipt (e.g., "I'm processing your audio file now. This might take a moment...").
2. **Execution:** Invoke `{baseDir}/scripts/process-audio` on the file. If it fails on missing deps, run `--check` and surface missing items.
3. **Summary:** Read the resulting transcript and create a short, highly accurate semantic summary of the content (do not just copy the text).
4. **Attachments:** You MUST attach the transcript and the cleaned audio using the EXACT paths from the script output. Use the `MEDIA:<path>` syntax as plain text at the very end of your response (do NOT wrap in markdown code blocks):
   MEDIA:<path-to-transcript.txt>
   MEDIA:<path-to-clean-short.mp3>

## CLI Usage

You can also run the underlying script manually:

```bash
{baseDir}/scripts/process-audio <file_or_zip> [options]
```

Options:
- `--enhance`: Force ClearVoice cleaning.
- `--no-enhance`: Disable ClearVoice cleaning.
- `--language <lang>`: Force specific language (e.g. `de` or `en`). Defaults to `auto` (automatic de/en detection).
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

## Install References
- `references/install/macos.txt`
- `references/install/linux-apt.txt`
- `references/install/linux-pacman.txt`
- `references/install/linux-dnf.txt`
- `references/install/linux-zypper.txt`
