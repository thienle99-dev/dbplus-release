# DB Plus Releases

Binary builds and update feeds for **[DB Plus](https://github.com/thienle99-dev/dbplus)** — a native database IDE for macOS, Windows, and Linux.

This repository holds **distribution artifacts only**. Application source lives in [`thienle99-dev/dbplus`](https://github.com/thienle99-dev/dbplus).

## Features

- **Native desktop apps** — AppKit/Swift on macOS, WinUI 3/C++ on Windows, Qt 6/C++20 on Linux (not Electron).
- **SQL editor & data grid** — Run queries, edit cells, filter, sort, paginate, and export results.
- **Schema browser** — Tables, indexes, foreign keys, views, functions/procedures, and ER diagrams.
- **AI assistant** — Schema-aware chat with Anthropic, OpenAI, Gemini, or local Ollama.
- **MCP server** — Optional Model Context Protocol server with per-connection permissions and activity logs.
- **Safe Mode** — Per-connection write protection (`Off` / `Confirm writes` / `Read-only`).
- **Local credentials** — Passwords in macOS Keychain / Windows Credential Manager; never stored in connection files or logs.
- **External drivers** — Optional sandboxed `.dbplusdriver` packages (DuckDB, Cassandra, CockroachDB, Elasticsearch, …).
- **Auto-update (macOS)** — Sparkle feed hosted on this repository’s Releases.

## Supported databases

### Built-in

| Engine | Highlights |
|---|---|
| **PostgreSQL** | Parameterized queries, SSL/mTLS, schemas, sequences |
| **MySQL** | TLS, charset, reconnect, parameterized queries |
| **SQLite** | Local file, WAL, no server |
| **Redis** | Key browser, SCAN, server info, slow log |
| **MongoDB** | Collections, document edit, aggregation, NDJSON backup |
| **SQL Server** | TDS 7.4, stored procedures, native backup |
| **ClickHouse** | HTTP/HTTPS, mTLS, schema browse |

### Optional reference drivers (`.dbplusdriver`)

| Engine | Notes |
|---|---|
| **DuckDB** | Embedded analytics; package installed into the app |
| **Cassandra** | CQL / column-family model via DriverHost |
| **CockroachDB** | PostgreSQL wire protocol through isolated host |
| **Elasticsearch** | SQL/API access via sandboxed driver package |

Built-in engines ship inside the app. Reference drivers are validated, signed packages loaded at runtime (capability-gated UI).

## Download

Latest builds: **[Releases → Latest](https://github.com/thienle99-dev/dbplus-release/releases/latest)**

| Platform | Asset (typical) | Status |
|---|---|---|
| macOS (Apple Silicon / Intel) | `DBPlus-<version>-<arch>.dmg` | Published |
| Windows | Velopack installer / nupkg | When published |
| Linux | AppImage | When published |

**macOS requirements:** macOS 14+. Current `v1.0.0` ships **arm64** (Apple Silicon).

### macOS first open (unsigned builds)

If the build is **not** notarized with an Apple Developer ID, Gatekeeper may block the app.

**Option A — Finder**

1. Open the DMG and drag **DB Plus** to Applications.
2. In Finder → Applications → **right-click DB Plus → Open** (not double-click).
3. Confirm Open.

**Option B — clear quarantine (Terminal)**

```bash
# After installing to /Applications
sudo xattr -dr com.apple.quarantine /Applications/DBPlus.app

# Or on the DMG before opening it
sudo xattr -d com.apple.quarantine ~/Downloads/DBPlus-*-arm64.dmg
```

`-dr` clears the attribute recursively on the `.app` bundle. Then open DB Plus normally.

## Auto-update (macOS / Sparkle)

Installed builds check:

`https://github.com/thienle99-dev/dbplus-release/releases/latest/download/appcast.xml`

Each macOS release should attach:

- One or more `DBPlus-*.dmg` files
- `appcast.xml` (Sparkle feed; EdDSA-signed enclosures)

The app verifies updates with `SUPublicEDKey` in its Info.plist. Use **DB Plus → Check for Updates…** or **Settings → General → Updates**.

## Maintainers

Artifacts are published from the source repo:

```bash
# in thienle99-dev/dbplus
UNSIGNED=1 ./scripts/release.sh   # or signed/notarized when Developer ID is available
./scripts/publish.sh              # generate_appcast + upload to this repo
```

`publish.sh` defaults to `RELEASE_REPO=thienle99-dev/dbplus-release`.

Do **not** commit Apple signing secrets, Sparkle EdDSA private keys, or notarization credentials here.
