# Vetrra System Requirements (Windows)

This document describes the **hardware + OS requirements** to run Vetrra, plus a short list of **software prerequisites** that affect specific pipeline stages.

For setup instructions, see `INSTALLATION_GUIDE.md`.

## Supported Platforms

- **Windows 10/11 (64-bit)** only (recommended: Windows 11).
- Vetrra is distributed as a standalone EXE (no Python install required).

## CPU / RAM / Storage

### Minimum (Will Run)

- **CPU**: Quad-core recommended
  - Dual-core systems are supported, but **encoding-heavy stages will be slow**.
- **RAM**: 8 GB
- **Storage**: SSD recommended; at least **50 GB free** on the drive hosting your Vetrra workspace

### Recommended (Smooth Experience)

- **CPU**: 6-8 cores (or better) for faster video processing
- **RAM**: 16 GB+
- **Storage**: SSD with **200 GB+ free** for large libraries and temporary files

## GPU & AI Acceleration (Optional)

Vetrra is designed to take advantage of Windows-native acceleration when it's available, and fall back to CPU when it's not.

- **Standard AI (recommended)**: **DirectML** acceleration (any DirectX 12 GPU: NVIDIA / AMD / Intel Arc). **No Docker required.**
- **Hardware encoding (optional)**: supported when available/configured (for example NVENC / QSV / AMF).
- **Advanced AI (optional)**: Docker Desktop + NVIDIA GPU + NIM API key for specific accelerators (for users already comfortable with containerization).

## Network

- Internet is required for metadata/artwork downloads (TMDb/TVDB/Fanart).
- Local-only stages still run offline once prerequisites are installed.

## Required External Tools (Typical End-User Setup)

Vetrra relies on a few external tools that must be installed separately (or be discoverable in common default install locations):

- **FFmpeg**
- **MKVToolNix**
- **Subtitle Edit (GUI)** (used by the subtitle pipeline)
- **Ollama** (subtitle OCR and poster analysis)

Notes:
- Some tools may be bundled with the Vetrra installer/build depending on the release package.
- If you're missing prerequisites, follow `INSTALLATION_GUIDE.md` for direct download links and setup notes.
