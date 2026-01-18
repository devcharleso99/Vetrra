# Vetrra Installation and Settings Guide

## Pre-Installation Checklist (Do This First)

Before you install or launch Vetrra, have these ready. Most "it won't save / it won't activate" issues in beta were missing prerequisites.

- **Workspace location**: pick a writable folder with lots of free space (SSD recommended)
- **Plex library paths**: Movies path + TV path (the folders Plex actually scans)
- **SABnzbd** (required):
  - Base URL (example: `http://127.0.0.1:8080`)
  - API key
  - Log directory path (example: `%LOCALAPPDATA%\\sabnzbd\\logs`)
- **Radarr/Sonarr** (required):
  - Base URL + API key for each service you plan to use
- **Metadata keys**:
  - TMDb API key
  - TVDB API key
  - Fanart.tv API key
- **Indexer / Preflight**:
  - Indexer name
  - Indexer base URL + API key (NZBFinder)
- **Poster analysis**:
  - Pick a local Ollama vision model in Settings (required to pass "Test Configuration")

Note on installer size: depending on the release package, the installer may be large because it can include bundled utilities and offline/local AI components. This is intentional (privacy + stability).

## Quick Start
1. Install Vetrra and launch the EXE.
2. On first-ever launch, the Settings window opens automatically.
  - If you ever need it later: Tools > Settings.
3. Configure the required tabs in order:
  - Library Paths
  - Automation & Webhooks
  - Providers (Metadata + OCR + Indexer APIs)
  - External Tools (only if auto-detection fails)
4. Click Save Configuration, then Test Configuration.
5. Go to the Pipeline tab, expand Step 1: Intake, and click Run to start the intake process.

Required tools (installer will detect these)
- FFmpeg: https://www.gyan.dev/ffmpeg/builds/
- MKVToolNix: https://mkvtoolnix.download/downloads.html
- Subtitle Edit GUI: https://github.com/SubtitleEdit/subtitleedit/releases
- Ollama (subtitle OCR and poster analysis): https://ollama.com/download/windows

Optional tools (only needed for specific configurations)
- Tesseract OCR (legacy fallback for Step 7): https://github.com/UB-Mannheim/tesseract/wiki
- Docker Desktop + NVIDIA NIM (optional Step 7 accelerator for NVIDIA users): https://www.docker.com/products/docker-desktop/ and https://catalog.ngc.nvidia.com/

Included
- HandBrakeCLI and SE-CLI is bundled with Vetrra. 

Step 7 Poster OCR - how it works (v1.1.0+)
- Default behavior uses Local AI (RapidOCR/ONNX) for poster text-region detection (no Docker required).
- Local AI uses DirectML GPU acceleration on Windows when available (Intel Arc / AMD / NVIDIA); otherwise it falls back to CPU automatically.
- If you have Docker Desktop + an NVIDIA GPU + a NIM API key, Auto mode can use NVIDIA NIM (PaddleOCR container).
- If no OCR provider is available, Step 7 still runs using edge-density heuristics (worst-case fallback).

Optional: start the NIM container manually (recommended for first-time setup)
1. In Vetrra, set your **NIM API Key** (Tools > Settings > Indexers & OCR) and Save Configuration.
2. Start Docker Desktop.
3. Run the included script from the Vetrra install folder:
   - PowerShell: `powershell -ExecutionPolicy Bypass -File ".\\_internal\\scripts\\start_nim.ps1"`
4. Verify readiness (either option):
   - Browser: `http://localhost:8000/v1/health/ready`
   - CLI: `docker ps` (look for `paddleocr-nim`) and `docker logs paddleocr-nim`

Settings checklist (Tools > Settings)

Tab: Library Paths
- Main Workspace Path: set this first. This is the root folder for all pipeline working folders.
  Keep it on a drive with lots of free space.
- Movies Path: your Plex movies library folder.
- TV Path: your Plex TV shows library folder.
- UI Scale: optional display size tweak.

Tab: Automation and Webhooks
This tab configures the three local services Vetrra talks to:

Install / launch these first (if you don't already have them):
- Radarr (Windows x64): https://radarr.video/
- Sonarr (Windows x64): https://sonarr.tv/
- Prowlarr (Windows x64): https://prowlarr.com/
- SABnzbd (Windows x64): https://sabnzbd.org/downloads

Notes:
- These services usually open a local web UI after install.
- Prowlarr connects directly to Radarr/Sonarr; no Vetrra connection needed.

Radarr (required for Movies)
- URL: full URL including port.
  - Default example: http://localhost:7878
- API key: Radarr UI -> Settings -> General -> Security -> API Key

Sonarr (required for TV Shows)
- URL: full URL including port.
  - Default example: http://localhost:8989
- API key: Sonarr UI -> Settings -> General -> Security -> API Key

SABnzbd (required)
- URL: full URL including port.
  - Default example: http://127.0.0.1:8080
- API key: SABnzbd UI -> Config (gear) -> General -> Security -> API Key
  - Use the API Key (not the NZB Key).

SABnzbd folders (required)
After you confirm the API key, configure SABnzbd's folder paths so it downloads into your Vetrra workspace structure.

1. In SABnzbd, click Config (gear).
2. Go to the Folders tab.
3. Set these three folder paths:
   - Temporary Download Folder:
     - <YOUR_BASE_PATH>\workspace\1_downloading\incomplete
   - Completed Download Folder:
     - <YOUR_BASE_PATH>\workspace\1_downloading\complete_raw
   - Watched Folder (where SABnzbd watches for .nzb files to auto-import):
     - <YOUR_BASE_PATH>\workspace\0_new_requests\watched

Notes:
- <YOUR_BASE_PATH> is the "Main Workspace Path" you set in the Library Paths tab.
- The important part is the ending subpath (the \workspace\... portion). Your drive letter / starting folders may differ.
- Example: if your base path is C:\Vetrra, then your Temporary Download Folder would be:
  - C:\Vetrra\workspace\1_downloading\incomplete

- SABnzbd Log Directory (in Vetrra Settings): required for telemetry validation (Settings won't save without it).
  - Common default (Windows): %LOCALAPPDATA%\sabnzbd\logs
  - If you changed SAB's folders or run it as a service, use the log folder configured in SABnzbd.

One-time setup inside Radarr / Sonarr / Prowlarr

Vetrra can connect to Radarr/Sonarr/SABnzbd, but Radarr/Sonarr still need their own setup so they can actually find releases and send downloads to SABnzbd.
The two big pieces are:
- Indexers (where Radarr/Sonarr search)
- Download client (SABnzbd)

Step A - Root folder (Radarr/Sonarr)
Radarr and Sonarr require at least one "root folder" to be set.

1. Radarr -> Settings -> Media Management (or Library) -> Root Folders
2. Add a root folder path that exists and is writable.
   - Most common choice: your Plex Movies folder
3. Sonarr -> Settings -> Media Management (or Library) -> Root Folders
4. Add a root folder path that exists and is writable.
   - Most common choice: your Plex TV folder

Note: Vetrra does not use Radarr/Sonarr root folders directly. They're mainly required so Radarr/Sonarr can manage content normally.

Step B - Add SABnzbd as the download client (Radarr/Sonarr)
1. Radarr -> Settings -> Download Clients
2. Add a "SABnzbd" download client:
   - Host/URL: your SABnzbd address (often `localhost`)
   - Port: your SABnzbd port (often `8080`)
   - API Key: your SABnzbd API key
3. Save, then use the built-in Test button.

Repeat the same in Sonarr -> Settings -> Download Clients.

Step C - Add indexers (required: do this in Prowlarr)
Prowlarr is the easiest way to manage indexers once and sync them into both Radarr and Sonarr.

1. Install and open Prowlarr
2. Prowlarr -> Settings -> Indexers
3. Click Add Indexer -> choose your Usenet indexer (preset) or use Custom
4. Enter the indexer details, including the Indexer API Key (from the indexer website)
5. Save and Test

Step D - Connect Prowlarr to Radarr and Sonarr (Apps)
This is where you paste Radarr/Sonarr API keys into Prowlarr so it can sync indexers into them.

1. Prowlarr -> Settings -> Apps
2. Add Radarr:
  - URL: Prowlarr often auto-fills a default (commonly `http://localhost:7878`).
    - If it's already filled in, just confirm it matches your Radarr URL/port.
  - API Key: paste your Radarr API key
  - Sync Profile: choose "Standard" for most users (RSS + searches)
3. Save and Test
4. Add Sonarr:
  - URL: Prowlarr often auto-fills a default (commonly `http://localhost:8989`).
    - If it's already filled in, just confirm it matches your Sonarr URL/port.
  - API Key: paste your Sonarr API key
  - Sync Profile: choose "Standard"
5. Save and Test

Sync Profiles note
- Sync Profiles are managed in their own section on the same Apps page.
- If you already have a "Standard" profile, you usually don't need to change it.

After this, your indexers should appear inside Radarr/Sonarr automatically (synced from Prowlarr), and Radarr/Sonarr can use SABnzbd to download.

Telemetry & Webhooks (Radarr + Sonarr -> Vetrra)
- Keep the default port unless you have a conflict.
- Webhook URLs (defaults):
  - http://localhost:8765/webhook/radarr
  - http://localhost:8765/webhook/sonarr

Configure Sonarr webhook
1. Sonarr -> Settings -> Connect
2. Add connection -> Webhook
3. URL: http://localhost:8765/webhook/sonarr
4. Method: POST
5. Triggers: enable these notifications:
   - On Grab
   - On File Import
   - On Import Complete
6. Save

Configure Radarr webhook
1. Radarr -> Settings -> Connect
2. Add connection -> Webhook
3. URL: http://localhost:8765/webhook/radarr
4. Method: POST
5. Triggers: enable these notifications:
   - On Grab
   - On File Import
6. Save

Tab: Providers
Metadata and artwork API keys
- TMDb API Key: https://www.themoviedb.org/settings/api
- TVDB API Key: https://thetvdb.com/api-information
- Fanart.tv API Key: https://fanart.tv/get-an-api-key/

Poster OCR (Step 7)
- Poster OCR Engine is configured in Tools > Settings > Pipeline Stages > Poster Handler.
  - Default: `auto` (recommended)
  - `nim`: use NVIDIA NIM (Docker) if available
  - `rapid_local`: force Local AI (RapidOCR/ONNX)
  - `tesseract`: force legacy Tesseract OCR
- If using `nim`, configure:
  - NIM OCR URL (default `http://localhost:8000`)
  - NIM API Key (create at https://catalog.ngc.nvidia.com/)

Indexer APIs (Preflight)
- Indexer Name: use the exact indexer name as shown inside Radarr/Sonarr.
  - Where to find it: Radarr/Sonarr ->' Settings ->' Indexers (copy the displayed name)
- Indexer Base URL: your indexer's base URL (example: https://nzbfinder.ws)
- Indexer API Key: from your indexer account / API Info page.
- Indexer UID: only required by some Newznab indexers (NZBFinder is a common example).
  - What is it used for: preflight downloads the NZB payload via Newznab `t=get` and sends this as the `uid` query parameter.
  - Where to find it (NZBFinder verified):
    1. Open any release details page on your indexer.
    2. Right-click the "Download NZB" link ->' Copy Link Address.
    3. Paste the URL somewhere safe and look for `uid=...` at the end (example format: `.../getnzb?id=<id>&uid=<uid>`).
    4. Copy just the number/value after `uid=` and paste it into Vetrra.
  - Where to find it (other indexers): check the indexer's API / API Info page for example URLs.
  - If you can't find a `uid` anywhere, leave it blank and run a preflight test; some indexers don't require it.

NNTP Probing (Optional, Preflight)
- If you want real NNTP availability probing ("anti-probe") in preflight, enable it in Tools > Settings > Providers and configure your Usenet provider (this writes `%APPDATA%\\Vetrra\\config\\servers.json`).
- If you leave it disabled/unconfigured, preflight falls back to static analysis.

Tab: Pipeline Stages

Most users should keep defaults here. The settings below are the only ones you might reasonably change.

Stage 01: Intake & Search (Preflight)
- TV Analysis Mode (`standard`, `hybrid`, `reliability`)
  - What it does: controls how TV preflight uses caching.
  - `standard`: uses cache + deduplication (fastest; recommended for most).
  - `reliability`: forces fresh analysis (slowest; best when you suspect stale cache or bad historical decisions).
  - `hybrid`: cache + selective fresh checks (middle ground).
- Movie Analysis Mode: same concept as TV, but for movie preflight.

- Sample Cap (%): default is `2.5%`.
  - What it does: sampling budget for NNTP probing inside a release.
  - Higher = more thorough validation but more load (and higher chance of provider rate limiting).
- Sample Cap Ceiling (segments): hard cap on total segments probed regardless of %.
  - Think of it as a safety limit. If you raise Sample Cap (%), keep an eye on this ceiling.

- TV Accept Threshold (%): default is `50%`.
  - This does NOT mean "50% of the pack must pass."
  - It controls the strategy decision for seasons/packs:
    - `100%`: only allow the hybrid "episodes + pack" strategy when the system can cover 100% of episodes; otherwise prefer season pack.
    - `50%`: allow the hybrid "episodes + pack" strategy when it can cover at least half the season.
    - `0%`: always allow the hybrid strategy (more aggressive; can be noisier).

- Advanced tuning (usually leave defaults):
  - Max Concurrent Preflights, Probe Connections / Server, Global Probe Rate Limit (RPS)
  - If you hit NNTP/provider rate limits or bursty behavior, lower these first.

Stage 05: Subtitle Handler
- Custom Profile Dir (optional)
  - Default location (Windows): `%APPDATA%\Vetrra\_internal\config`
  - The two profile filenames are used inside that folder:
    - `SE-1080p.xml` (1080p)
    - `SE-2160p.xml` (4K)
  - If a profile file is missing, Vetrra will try to bootstrap it from your live Subtitle Edit settings.
- OCR Vision Model
  - Pick any installed vision-capable Ollama model for OCR via Ollama.

Stage 07: Poster Handler
- Analysis Mode
  - `heuristic`: fast, deterministic, no semantic VLM scoring.
  - `semantic`: uses an Ollama vision model to score/rank posters (more accurate, slower).

- Semantic controls (only relevant when `semantic`):
  - Semantic Vision Model: which installed Ollama vision model to use.
  - Bias Preset:
    - Textless priority: penalize heavy credits/billing blocks.
    - Aesthetic priority: allow theatrical credits more often.
  - Semantic Weight (0-1): how much semantic scoring influences the final rank.
  - Semantic Temperature: `0` is deterministic; typical range `0.0-1.0` (higher = more variance).
  - Semantic Seed: integer seed for repeatability (best-effort; depends on backend/model).
  - Ollama Timeout (seconds): how long to wait for a semantic/readability request.
  - Readability scoring + max crops: optional extra scoring pass (higher crops = slower).

Stage 08: Quality Check & Deploy
- Scan Concurrency: `2`, `4`, or `8` threads.
  - Higher = faster scanning, but higher CPU usage and a greater chance of hitting rate limits.
  - Default `4` is a good balance for most systems.

Tab: External Tools
- Set paths only if tools are not on your PATH or not in standard locations.
- Required: ffmpeg.exe, ffprobe.exe, mkvmerge.exe, mkvpropedit.exe, mkvextract.exe, tesseract.exe (fallback OCR), SubtitleEdit.exe (SRT->SUP only).

Config file location
- Windows: %APPDATA%\Vetrra\config\config.ini

Troubleshooting (common first-run blockers)

1) "Save Configuration" / "Test Configuration" fails
- In Tools > Settings, click **Test Configuration** and follow the issue list.

2) FileNotFoundError / "servers.json not found"
Vetrra keeps an optional NNTP probing config here:

- `%APPDATA%\\Vetrra\\config\\servers.json`

If it's missing (or empty), create it with this content:

```json
[]
```

If the file keeps disappearing or won't generate, ensure `%APPDATA%\\Vetrra\\config` is writable for your Windows user.

Support
- https://github.com/devcharleso99/Vetrra/issues

Happy Automating!
