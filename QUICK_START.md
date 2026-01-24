# Vetrra Quick Start (Golden Path)

Goal: Go from zero to your first successful **Step 1: Intake** run in under ~20 minutes.

STOP & READ
- This guide assumes **Windows 10/11** with **SABnzbd + Radarr (+ Sonarr optional)** installed **natively on the same PC** as Vetrra.
- If you use **Docker / Unraid / NAS / remote download clients**, stop and use `docs/main/ADVANCED_SETUP.md` (Remote Path Mappings).

## Phase 1 — System Prep (Install Dependencies First)

Vetrra coordinates several external tools. Install these before launching Vetrra so **Tools → Settings → Test Configuration** can pass immediately.

### 1) Install FFmpeg (required)
1. Download: https://www.gyan.dev/ffmpeg/builds/
2. Get: `ffmpeg-git-full.7z`
3. Extract and rename the extracted folder to `ffmpeg`
4. Move to `C:\ffmpeg\bin` (final folder should be `C:\ffmpeg\bin`)
5. Add to System PATH:
   - Windows key → “Edit the system environment variables”
   - Environment Variables
   - System variables → `Path` → Edit → New
   - Add: `C:\ffmpeg\bin`
   - OK → OK → OK

### 2) Install MKVToolNix + Subtitle Edit (required)
- MKVToolNix: https://mkvtoolnix.download/downloads.html (install defaults)
- Subtitle Edit: https://github.com/SubtitleEdit/subtitleedit/releases (install defaults)

### 3) Install Ollama + pull the Qwen 2.5 vision model (recommended)
1. Download: https://ollama.com/download/windows
2. Install it
3. Confirm it’s running (white Llama icon in the system tray)
4. You can pull the model either from the command line or via the Quick Start UI:
   - Command line: `ollama pull qwen2.5vl`
   - Quick Start button: Open Settings → Quick Start → **Pull Qwen 2.5 Model**
   - Note: Clicking the Quick Start **Pull** button requires Ollama to be installed; if Ollama is not found the app will open the Ollama download page for you.
5. Wait for success before proceeding (the app will auto-select `qwen2.5vl:latest` once pulled)

## Phase 2 — Create the Workspace (Do Not Use Your Plex Library Folder)

Vetrra needs a dedicated staging area. Create a folder named **exactly**:
- `Vetrra_Workspace`

Recommended locations:
- `C:\Vetrra_Workspace` (if you have admin rights), or
- `D:\Vetrra_Workspace` (if you prefer a large data drive)

## Phase 3 — Configure SABnzbd to Match the Workspace (Critical)

Open SABnzbd (usually `http://localhost:8080`) → **Config (gear) → Folders**

Set these paths (adjust drive letter if you didn’t use `C:`):
- Temporary Download Folder: `C:\Vetrra_Workspace\1_downloading\incomplete`
- Completed Download Folder: `C:\Vetrra_Workspace\1_downloading\complete_raw`
- Watched Folder: `C:\Vetrra_Workspace\0_new_requests\watched`

Click **Save Changes**.

Then go to **Config → General** and copy your **API Key** (not the NZB key).

## Phase 4 — Copy API Keys from Radarr/Sonarr

Radarr (movies): `http://localhost:7878` → Settings → General → API Key

Sonarr (TV, optional): `http://localhost:8989` → Settings → General → API Key

## Phase 5 — First Launch & Activation

1. Install and launch Vetrra.
2. On first run, the Settings dialog opens automatically.

### Tab: Library Paths
- Main Workspace Path: select your `C:\Vetrra_Workspace`
- Movies Path: select your Plex Movies library folder (example: `D:\Media\Movies`)
- TV Path: select your Plex TV library folder (example: `D:\Media\TV`)

### Tab: Automation & Webhooks
- SABnzbd: URL `http://localhost:8080` + your API key
- Radarr: URL `http://localhost:7878` + your API key
- Sonarr (optional): URL `http://localhost:8989` + your API key

### Tab: Providers
- Metadata: set your **TMDb API key** (required)
- AI: select **Ollama (Local)** and choose `qwen2.5vl` as the vision model

### Validate
1. Click **Test Configuration**
2. Fix any red items before proceeding
3. Click **Save Configuration**

## Phase 6 — Run Step 1 (Activation)

1. Go to the **Pipeline** tab
2. Expand **Step 1: Intake**
3. Click **Wishlist**
4. Add a test movie, then **Add to Intake**
5. Back in Step 1, click **Run**

If everything is configured correctly:
- Vetrra preflights releases and sends the best candidate to SABnzbd
- When SAB finishes, Vetrra detects the completed download in the workspace and advances it to Step 2

