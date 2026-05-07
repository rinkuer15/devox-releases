# Devox Releases

Binary releases for the [Devox CLI](https://github.com/rinkuer15/Devox) — a remote agentic coding platform to control AI assistants (Claude, Codex, Copilot) from Slack, Telegram, GitHub, and a Web UI.

---

## Installation

### Quick Install (Recommended)

**macOS / Linux**
```bash
curl -fsSL https://raw.githubusercontent.com/rinkuer15/Devox/main/scripts/install.sh | bash
```

**Windows (PowerShell)**
```powershell
irm https://raw.githubusercontent.com/rinkuer15/Devox/main/scripts/install.ps1 | iex
```

---

### Manual Installation

Download the binary for your platform from the [latest release](https://github.com/rinkuer15/devox-releases/releases/latest).

#### macOS (Apple Silicon — M1/M2/M3)
```bash
curl -fsSL https://github.com/rinkuer15/devox-releases/releases/latest/download/devox-darwin-arm64 -o /usr/local/bin/devox
chmod +x /usr/local/bin/devox
```

#### macOS (Intel)
```bash
curl -fsSL https://github.com/rinkuer15/devox-releases/releases/latest/download/devox-darwin-x64 -o /usr/local/bin/devox
chmod +x /usr/local/bin/devox
```

#### Linux (x64)
```bash
curl -fsSL https://github.com/rinkuer15/devox-releases/releases/latest/download/devox-linux-x64 -o /usr/local/bin/devox
chmod +x /usr/local/bin/devox
```

#### Linux (ARM64)
```bash
curl -fsSL https://github.com/rinkuer15/devox-releases/releases/latest/download/devox-linux-arm64 -o /usr/local/bin/devox
chmod +x /usr/local/bin/devox
```

#### Windows (x64)

1. Download [`devox-windows-x64.exe`](https://github.com/rinkuer15/devox-releases/releases/latest/download/devox-windows-x64.exe) from the latest release
2. Rename it to `devox.exe`
3. Add it to your PATH using one of these methods:

**Option A — Drop into System32 (easiest, requires admin)**
```powershell
Move-Item "$env:USERPROFILE\Downloads\devox-windows-x64.exe" "C:\Windows\System32\devox.exe"
```

**Option B — Add a dedicated folder to PATH (recommended)**
```powershell
New-Item -ItemType Directory -Force "C:\devox"
Move-Item "$env:USERPROFILE\Downloads\devox-windows-x64.exe" "C:\devox\devox.exe"

[Environment]::SetEnvironmentVariable(
  "PATH",
  $env:PATH + ";C:\devox",
  "User"
)
```
Then **close and reopen your terminal**.

**Option C — Test without any PATH changes**
```powershell
& "$env:USERPROFILE\Downloads\devox-windows-x64.exe" version
```

---

### Homebrew (macOS / Linux)
```bash
brew install rinkuer15/devox/devox
```

### Docker
```bash
docker run --rm -v "$PWD:/workspace" ghcr.io/rinkuer15/devox:latest workflow list
```

---

## Verify Installation

Run these commands to confirm the binary is working correctly.

### 1. Check version
```bash
devox version
```
**Expected output:**
```
Devox v1.0.0
Build: binary
Commit: abc12345
```
> ⚠️ If you see `Build: source` or `Failed to read version` — the binary is broken, re-download.

### 2. List bundled workflows
```bash
devox workflow list
```
**Expected:** A list of built-in workflows including `devox-assist`.
> ⚠️ If the list is empty or errors — re-download from the latest release.

### 3. Get help
```bash
devox --help
```

### 4. Full smoke test (requires a git repo)
```bash
# Run from inside any git repository:
devox workflow run devox-assist --no-worktree "What files are in this repo?"
```

---

## Verify Checksums

Every release includes `checksums.txt` with SHA-256 hashes for all binaries.

**macOS / Linux:**
```bash
curl -fsSL https://github.com/rinkuer15/devox-releases/releases/latest/download/checksums.txt -o checksums.txt
sha256sum --check checksums.txt --ignore-missing
```

**Windows (PowerShell):**
```powershell
$file = "$env:USERPROFILE\Downloads\devox-windows-x64.exe"
$checksums = (Invoke-WebRequest "https://github.com/rinkuer15/devox-releases/releases/latest/download/checksums.txt").Content
$actual = (Get-FileHash $file -Algorithm SHA256).Hash.ToLower()
if ($checksums -match $actual) { "OK: checksum matches" } else { "MISMATCH: do not use this binary" }
```

---

## Troubleshooting

| Error | Cause | Fix |
|-------|-------|-----|
| `command not found: devox` | Binary not on PATH | Follow PATH setup steps above |
| `Build: source` in version output | Binary built incorrectly | Re-download from latest release |
| `Failed to read version` | Binary built without embed flag | Re-download from latest release |
| `workflow list` returns nothing | Bundled defaults missing | Re-download from latest release |
| Permission denied (macOS/Linux) | Missing execute permission | `chmod +x /usr/local/bin/devox` |

---

## Links

- **Source:** [rinkuer15/Devox](https://github.com/rinkuer15/Devox)
- **Issues:** [rinkuer15/Devox/issues](https://github.com/rinkuer15/Devox/issues)
