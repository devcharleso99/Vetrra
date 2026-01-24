# Vetrra User Guide

This guide focuses on day-to-day usage once Vetrra is installed and configured.

If you haven't installed and configured Vetrra yet, start with:

- `INSTALLATION_GUIDE.md`
- `SYSTEM_REQUIREMENTS.md`

## First Run (Expected Flow)

1. Launch Vetrra.
2. Tools -> Settings.
3. Configure the tabs in order:
   - Quick Start (recommended)
   - Library Paths
   - Automation & Webhooks
   - Providers
   - Indexers & OCR (advanced)
   - Pipeline Stages (advanced)
   - External Tools (only if auto-detection fails)
4. Click **Save Configuration**, then **Test Configuration**.

If "Test Configuration" reports missing fields for a service you don't use, disable that integration in Settings first.

## In-App Help (Context-Aware)

Each Settings tab includes a **Help** button that opens the built-in documentation viewer directly to the relevant section. Use the Help window's search bar to quickly find topics like "API key", "path mappings", and "OCR".

## What The Pipeline Does (High Level)

Vetrra runs a staged pipeline (Steps 1-8) so your workflow stays consistent:

- Step 1: Intake & Search
- Step 2: Organize
- Step 3: MKV Processing
- Step 4: Video Encoding
- Step 5: Subtitle Handling
- Step 6: Final Mux
- Step 7: Poster Handling
- Step 8: Quality Check & Deploy

Tip: If you plan to add screenshots to the GitHub docs, `README.md` contains placeholders for each step.

## Common Workflows

### Movie Workflow (Typical)

1. Add a request (or import a request) via your intake workflow.
2. Run Step 1 and confirm candidates.
3. Let Steps 2-6 normalize, encode, subtitle, and mux.
4. Let Step 8 deploy into your Plex Movies folder.

### TV Workflow (Typical)

1. Ensure Sonarr is configured (only if you enable it).
2. Run Step 1 and confirm candidates.
3. Let Steps 2-6 produce a consistent final output.
4. Let Step 8 deploy into your Plex TV folder.

## Logs, Status, and Diagnostics

Vetrra stores config and logs under your Windows profile:

- Logs: `%APPDATA%\\Vetrra\\logs`
- Config: `%APPDATA%\\Vetrra\\config\\config.ini`

When requesting support, include the exact step where a failure occurs and the relevant log snippet.

## Getting Help / Reporting Bugs

See `SUPPORT.md`.
