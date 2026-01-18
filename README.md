# Vetrra

Vetrra is a **Windows-first automation pipeline** for Plex power users who want a more reliable, repeatable way to go from "new request" -> "ready in Plex".

This repository contains Vetrra documentation and release notes. Vetrra itself is **proprietary, subscription software** (monthly or yearly; single tier).

## Why Vetrra

- **Built for Windows power users** (GUI-first)
- **No Docker required** for the standard experience (Docker is optional for specific accelerators)
- **Native hardware acceleration** where available (encoding + OCR/vision features)
- **Pipeline orchestration** so your process is consistent from run to run

## What Vetrra Helps With

- **Automated quality control**: reduce failed downloads and "bad release" churn by validating early
- **Subtitle workflows**: extract/convert/OCR (optional) and normalize subtitles as part of the pipeline
- **Poster workflows**: rank/select posters and optionally use OCR/analysis to avoid low-quality artwork
- **Cleaner deploys**: enforce a consistent final output before moving media into Plex libraries

## Start Here

- Install and configure: `INSTALLATION_GUIDE.md`
- System requirements: `SYSTEM_REQUIREMENTS.md`
- Help and bug reports: `SUPPORT.md`

## Pipeline Overview

### Step 1: Intake & Search

Collects new requests and prepares candidates for validation.

### Step 2: Organize

Stages content into a predictable workspace structure.

### Step 3: MKV Processing

Inspects containers and applies safe, consistent MKV transformations.

### Step 4: Video Encoding

Encodes with configurable quality targets (hardware acceleration when available).

### Step 5: Subtitle Handling

Extracts, converts, OCRs (optional), and validates subtitles.

### Step 6: Final Mux

Builds the final deliverable file(s) with the intended streams and metadata.

### Step 7: Poster Handling

Evaluates artwork and can perform OCR/analysis to improve poster selection.

### Step 8: Quality Check & Deploy

Runs final validation and deploys to your Plex library paths.

## Subscription, Updates, and Terms

Vetrra is a subscription product (monthly or yearly; single tier). The subscription funds ongoing development, updates, and support.

- License terms: `LICENSE.md`
- Release notes: `CHANGELOG.md`
- Roadmap (directional): `ROADMAP.md`

## Links

- Discord: https://discord.gg/aX7hdqaq
- Reddit: https://www.reddit.com/r/Vetrra/
- GitHub Issues: https://github.com/devcharleso99/Vetrra/issues
