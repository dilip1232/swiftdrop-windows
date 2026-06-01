# SwiftDrop for Windows

Windows desktop companion for SwiftDrop — fast peer-to-peer file transfers on
your LAN. Sends files to/from Android, macOS, and other Windows machines running
SwiftDrop.

## Architecture

This is a **platform shell** that imports `swiftdrop-core` (shared Go module)
and adds Windows-specific wiring:

- **Full-window app** that lives in the system tray
- Click the tray icon → show/hide the window
- Native Windows toast notifications (PowerShell)
- `GetDiskFreeSpaceExW` for disk-space checks
- `explorer.exe` to open the download folder
- Built with [Wails v3](https://wails.io/) + WebView2

## Build

```powershell
# On a Windows machine (or GitHub Actions windows-latest):
cd swiftdrop-windows
go mod tidy
.\build-windows.ps1
```

Or cross-compile from macOS/Linux (GUI won't work, but binary is produced):

```bash
GOOS=windows GOARCH=amd64 CGO_ENABLED=0 go build -ldflags "-s -w -H windowsgui" -o SwiftDrop.exe .
```

## Headless mode

Run the server + discovery without any UI (useful for CI/testing):

```
SwiftDrop.exe -headless
```

## Requirements

- Windows 10 (version 1809+) or Windows 11
- WebView2 Runtime (pre-installed on Win10 21H2+ and Win11)
- LAN connectivity (same network as other SwiftDrop devices)

## Status

🚧 **WIP** — `feature/windows-support` branch. Not yet production-tested on
real Windows hardware.
