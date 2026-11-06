# Sonarr Recyclarr Sync — 2026-11-06

## Execution

- Recyclarr: v8.8.1
- Target: `mini_sonarr_1080p` only, `http://127.0.0.1:8989`
- Command: `recyclarr sync sonarr --config /var/tmp/arr-quality-policy-runtime/config/recyclarr.yml`
- Configuration/data paths: `RECYCLARR_CONFIG_DIR=/var/tmp/arr-quality-policy-runtime/config`, `RECYCLARR_DATA_DIR=/var/tmp/arr-quality-policy-runtime/data`
- Result: exit code 0; completed 2026-11-06 19:03:11 (+05:00).

## Recyclarr result

| Action | Count |
|---|---:|
| Created Custom Formats | 32 |
| Updated existing Custom Formats | 4 |
| Unchanged Custom Formats | 19 |
| Deleted Custom Formats | 0 |
| Updated Quality Profiles | 1 (`1080p RU`) |

The profile update changed score assignments only; Recyclarr reported zero quality changes.

## Post-sync verification

- Live Sonarr Custom Formats: **62** (30 before Sync + 32 created).
- All **55** managed formats are present.
- All **7** pre-existing formats outside the managed catalog remain present: `Bluray-BDRip`, `Bluray-Disk`, `Bluray-Remux`, `HDTV/SDTV`, `SeasonPack`, `WEB-DL`, `WEBRip`.
- No pre-existing Custom Formats were deleted.
- All **55** configured score assignments match the live `1080p RU` profile; zero mismatches.
- The profile's quality structure matches the pre-Sync native backup. Thresholds remain MinFormatScore 0, CutoffFormatScore 0, MinUpgradeFormatScore 1, Upgrades Allowed true.
- Key rules verified live: BDRip +120000; Remux +60000; Blu-ray Disk title -1000000; DVD Disk title -1000000; Dolby Vision +500; DV8.1 +3500.
- Recyclarr debug log: 5 GET, 32 POST, 5 PUT, 0 DELETE; no error/fatal lines. PUTs represent four existing Custom Format updates and the profile score update.
- Native backup remains available in Sonarr and in the project backup folder. SHA-256: `ea41126351730c9085241e9addb640549de79c5e3bd2d5796e602508f6d3cb17`.
- No Radarr Sync was run.

## Initial invocation

The first invocation stopped during configuration parsing because the obsolete `RECYCLARR_APP_DATA_DIR` variable was used. It made no Sonarr API write requests. The successful retry used `RECYCLARR_CONFIG_DIR` and `RECYCLARR_DATA_DIR`.
