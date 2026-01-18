# Vetrra System Requirements (Windows)

This document describes the **hardware + OS requirements** to run Vetrra, plus a short list of **software prerequisites** that affect specific pipeline stages.

If you want full setup instructions, see `docs/INSTALLATION_GUIDE.md`.

## Supported Platforms

- **Windows 10/11 (64-bit)** only (recommended: Windows 11).
- Vetrra is distributed as a standalone EXE (no Python install required).

## Minimum Requirements (Will Run)

- **CPU**: Modern dual-core (4 threads recommended)
- **RAM**: 8 GB
- **Storage**: SSD recommended; at least **50 GB free** on the drive hosting your Vetrra workspace
- **GPU**: Not required
- **Network**: Internet required for metadata/artwork downloads (TMDb/TVDB/Fanart); local-only stages still run offline

## Recommended Requirements (Smooth Experience)

- **CPU**: 6–8 cores (or better) for faster video processing
- **RAM**: 16 GB+
- **Storage**: SSD with **200 GB+ free** for large libraries and temporary files
- **GPU**:
  - Any GPU works; Vetrra adapts automatically.
  - **Intel Arc / AMD / NVIDIA**: Step 7 Local AI OCR can use **DirectML** acceleration when available.
  - **NVIDIA**: Step 4 encoding can benefit from NVENC-capable GPUs (when configured/available).

## Optional “Power User” Requirements (Feature-Dependent)

- **Docker Desktop + NVIDIA GPU + NIM API key**: Optional Step 7 poster OCR accelerator when `Poster OCR Engine = nim`.
- **Tesseract OCR** (legacy fallback for Step 7)

## Required External Tools (Typical End-User Setup)

Vetrra relies on a few external tools that must be installed separately (or be discoverable in the default install locations):

- **FFmpeg**
- **MKVToolNix**
- **Subtitle Edit (GUI)** (used by the subtitle pipeline)
 - **Ollama** (subtitle OCR and poster analysis)

Notes:
- Some tools are **bundled inside the Vetrra install
