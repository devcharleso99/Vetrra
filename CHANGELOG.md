# Changelog

All notable changes to Vetrra are documented in this file.


## [1.5.0-beta.1] - 2026-01-24

### Added

New "Undefeated Organizer" reconciliation engine for deterministic TV episode mapping.

Support for TV Season 00 "bimodal" deployment for specials.

"960p" resolution tier for anime upscales.

Manual mode "loose movie file staging" in Step 2.

Live upscaling progress callbacks in Step 4 telemetry.

**Option 1 — Clean, minimal, UI-native (my top recommendation)**

**Recommended setup:** Run Vetrra, SABnzbd, and Radarr on the same Windows PC for the simplest experience.

*Using Docker, NAS, or remote systems? See [ADVANCED_SETUP.md](ADVANCED_SETUP.md) for path mapping and remote configurations.*

### Changed

Downloads and documentation moved to GitHub.

Installer now includes "OCR Pack" messaging and AppData cleanup options.

Step 5 now validates SRT files by scanning for timecode cues rather than picking the first file.

RapidOCR now supports models installed in AppData.

### Fixed

Resolved GUI crashes in the cleanup tab.

Fixed Windows filename sanitization for extracted audio tracks.

Fixed a bug where process_mode limits were not being enforced correctly in Step 4.

Improved NVIDIA NIM container reliability and cleanup.

---
