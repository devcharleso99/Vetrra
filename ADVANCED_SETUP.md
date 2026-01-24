# Vetrra Advanced Setup (Docker / NAS / Remote Clients)

This guide is for setups where Vetrra and your download clients do **not** share the same filesystem view.

Examples:
- SABnzbd / Radarr / Sonarr running in Docker
- Unraid / NAS download client paths
- Mapped drives / UNC paths (`\\server\share`) used by one component but not the other

## The Problem: “Split-Brain” Filesystems

When a download client runs in Docker, it often reports container paths (example: `/data/downloads`) that do not exist on Windows.

Vetrra must be able to translate:
- “What SAB/Radarr says the path is” → into → “The Windows path where the files actually live”

## Use Remote Path Mappings

In Vetrra:
- Tools → Settings → (Advanced) Remote Path Mappings

Create mappings like:
- Remote: `/data/downloads` → Local: `D:\Downloads`
- Remote: `/data/media` → Local: `D:\Media`

After saving mappings:
- Re-run **Test Configuration**
- Run **Step 1: Intake** again

## NAS / UNC Guidance

Prefer one consistent path style everywhere:
- Either all components use a mapped drive (example: `Z:\Downloads`)
- Or all components use the UNC path (example: `\\NAS\Downloads`)

Mixing UNC + mapped drive paths often breaks “file found” checks.

