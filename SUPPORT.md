# Support

This page covers how to get help, report bugs, and request features for Vetrra.

## Where To Get Help

- **Discord (recommended)**: https://discord.gg/aX7hdqaq
  - `#announcements` (releases + important notices)
  - `#beta-support` (setup help + troubleshooting for Insider/Beta builds)
  - `#bug-reports` (bugs + reproducible issues)
  - `#general` (questions + discussion)
- **GitHub Issues (bugs + feature requests)**: https://github.com/devcharleso99/Vetrra/issues
- **Reddit (community)**: https://www.reddit.com/r/Vetrra/

## Before You Post

- Confirm you meet `SYSTEM_REQUIREMENTS.md`
- Follow `INSTALLATION_GUIDE.md` (especially "Save Configuration" + "Test Configuration")
- Check `CHANGELOG.md` to see if your issue was already fixed

## Reporting A Bug (Checklist)

Please include:

- **Vetrra version** and channel (**Stable** vs **Insider/Beta**)
- **Windows version** (10/11 + build number)
- **Hardware notes** (CPU, RAM, GPU; especially if the issue involves encoding/OCR)
- **Exact pipeline step** where it fails (Step 1-8)
- **Expected vs actual behavior**
- **Repro steps** (what you clicked, what input you provided)
- **Logs** (see below)
- **Config** (redact secrets)

If the issue is media-specific, include:

- Media type (movie/TV), resolution (1080p/2160p), container (MKV/MP4)
- Whether subtitles were present (SRT/PGS/SUP) and what you expected to happen

## Where Are The Logs?

Vetrra writes logs to your Windows profile:

- **Logs directory**: `%APPDATA%\\Vetrra\\logs`
- **Config file**: `%APPDATA%\\Vetrra\\config\\config.ini`

## Redacting Logs (Important)

Before posting logs publicly, remove secrets and personal information. Common items to search for:

- `api_key`, `apikey`, `token`, `Authorization`
- Radarr/Sonarr/SABnzbd API keys
- Indexer API keys (Newznab)
- TMDb/TVDB/Fanart API keys
- Discord webhooks
- Full local paths you don't want shared

Tip: replace values with `REDACTED` instead of deleting lines so context remains useful.

## Feature Requests

Use GitHub Issues and include:

- What problem you're trying to solve
- What you want Vetrra to do (specific outcome)
- Any constraints (time, storage, preferred workflow)

## Security Issues

If you believe you found a security issue, don't post it publicly first.

- Contact: devcharleso99@gmail.com
