# Vetrra Troubleshooting (First-Run)

This guide is optimized for first-run activation: getting a successful **Step 1: Intake** run.

## “Test Configuration” Failed

### FFmpeg / MKVToolNix not found
Check:
- Open Command Prompt, run: `ffmpeg`
- Do you see version info?

Action:
- If NO: add `C:\ffmpeg\bin` to your System PATH, then restart Vetrra
- If YES: ensure you installed the 64-bit build (reinstall FFmpeg / MKVToolNix if needed)

### Cannot connect to Radarr / SABnzbd
Check:
- Open the service URL in your browser (example: `http://localhost:7878`)
- Does the UI load?

Action:
- If NO: the service isn’t running; start it and retry
- If YES: re-copy the API key (watch for leading/trailing spaces)
- If using Docker: `localhost` from Vetrra may not work; use your PC’s LAN IP (example: `http://192.168.1.5:7878`)

### Ollama model not found / connection refused
Check:
- Is the Ollama tray icon visible?
- In PowerShell, run: `ollama list`
- Is `qwen2.5vl` listed?

Action:
- If NO: run `ollama pull qwen2.5vl`
- Restart Vetrra to refresh the model list

## “Step 1 Run” Failed

### Logs show `REJECT_UNREPAIRABLE`
Meaning:
- The release is broken/incomplete/passworded.

Action:
- None — Vetrra prevented a bad download. Try a different title or wait for a better release.

### Download completes in SABnzbd but Vetrra stays “Downloading”
Check:
- SABnzbd → Config → Folders
- Do these match your Vetrra workspace exactly?
  - `...\1_downloading\incomplete`
  - `...\1_downloading\complete_raw`

Action:
- Fix SABnzbd folder paths to match
- If using Docker: configure Remote Path Mappings (see `docs/main/ADVANCED_SETUP.md`)

