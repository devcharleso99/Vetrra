# Changelog

All notable changes to Vetrra are documented in this file.


## [1.5.0-beta.1] - 2026-01-24

### Added

New "TV Organizer" reconciliation engine for deterministic TV episode mapping.

Support for TV Season 00 "bimodal" deployment for specials.

"960p" resolution tier for upscales.

Manual mode "loose movie file staging" in Step 2.

Live upscaling progress callbacks in Step 4 telemetry.

### Changed

Downloads and documentation moved to GitHub.

Installer now includes "OCR Pack" messaging and AppData cleanup options.

Settings: "Download AI Packs" now installs OCR + optional ML packs (ML Pack split into multipart assets for GitHub upload).

Step 5 now validates SRT files by scanning for timecode cues rather than picking the first file.

RapidOCR now supports models installed in AppData.

Guided Navigation (preview): improved behavior and auto-scroll handling in Settings.

### Fixed

Resolved GUI crashes in the cleanup tab.

Additional UI fixes in the Settings window (layout/state/preview navigation polish).

Fixed Windows filename sanitization for extracted audio tracks.

Fixed a bug where process_mode limits were not being enforced correctly in Step 4.

Step 4 custom encoding mode: additional robustness fixes and UX polish.

Improved NVIDIA NIM container reliability and cleanup.

---
