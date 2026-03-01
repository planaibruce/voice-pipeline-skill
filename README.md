# Voice Pipeline

Self-contained, local-only audio enhancement and transcription.

## Installation

Clone this repository into your OpenClaw skills directory:
```bash
git clone https://github.com/mariozechner/voice-pipeline-skill.git ~/.openclaw/workspace/skills/voice-pipeline
```

## Setup
```bash
./scripts/process-audio --install
```
`--install` prints OS-specific commands for manual execution.

Diagnostics:
```bash
./scripts/process-audio --doctor
```

Dependency discovery:
```bash
./scripts/process-audio --check
```

Recommended OpenClaw health check:
```bash
openclaw doctor
```

## Use
```bash
./scripts/process-audio <audio_or_zip>
```
Default enhancement mode is always-on ClearVoice.
Default language is German (`de`).
Use `--language auto` for automatic German/English detection.
Default model is `large-v3` for higher accuracy.
Whisper runs GPU-only by default; CPU fallback is opt-in via `--allow-cpu-fallback`.

Outputs in `~/transcripts`:
- `<name>_<timestamp>.txt` (full transcript)
- `<name>_<timestamp>.clean-short.mp3` (cleaned and shortened audio)

First run order:
1. `openclaw doctor`
2. `./scripts/process-audio --doctor`
3. `./scripts/process-audio --install` (copy commands and run manually)
4. `./scripts/process-audio <audio_or_zip>`
