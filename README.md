# DB Plus Releases

Binary builds and update feeds for **[DB Plus](https://github.com/thienle99-dev/dbplus)** — a native database IDE.

This repository holds **distribution artifacts only**. Application source lives in [`thienle99-dev/dbplus`](https://github.com/thienle99-dev/dbplus).

## Download

Latest builds: **[Releases → Latest](https://github.com/thienle99-dev/dbplus-release/releases/latest)**

| Platform | Asset (typical) |
|---|---|
| macOS (Apple Silicon / Intel) | `DBPlus-<version>-<arch>.dmg` |
| Windows | (Velopack installer / nupkg — when published) |
| Linux | (AppImage — when published) |

Website download buttons also point here.

### macOS first open (unsigned builds)

If the build is **not** notarized with an Apple Developer ID, Gatekeeper may block the app. Use:

1. Open the DMG and drag **DB Plus** to Applications.
2. In Finder → Applications → **right-click DB Plus → Open** (not double-click).
3. Confirm Open.

## Auto-update (macOS / Sparkle)

Installed builds check:

`https://github.com/thienle99-dev/dbplus-release/releases/latest/download/appcast.xml`

Each release should attach:

- One or more `DBPlus-*.dmg` files
- `appcast.xml` (Sparkle feed; EdDSA-signed enclosures)

The app verifies updates with the public key embedded as `SUPublicEDKey` in its Info.plist.

## Maintainers

Artifacts are published from the source repo:

```bash
# in thienle99-dev/dbplus
UNSIGNED=1 ./scripts/release.sh   # or signed/notarized release when Developer ID is available
./scripts/publish.sh              # generate_appcast + upload to this repo
```

`publish.sh` defaults to `RELEASE_REPO=thienle99-dev/dbplus-release`.

Do **not** commit Apple signing secrets, Sparkle EdDSA private keys, or notarization credentials here.

## Links

- Source: https://github.com/thienle99-dev/dbplus
- Issues / PRs: use the source repository
- License: see the source repository
