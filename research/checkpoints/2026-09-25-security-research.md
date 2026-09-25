# 25 September 2026 — Hydra Security Research Checkpoint

## Scope

This checkpoint records observations from the fresh 25 September 2026 Hydra runtime session. It covers download-source synchronization/API metadata and the antivirus control test. It does **not** include an actual third-party game/software download or execution test.

## Evidence summary

### Download-source API

Hydra issued requests to:

`GET /games/steam/1817070/download-sources`

with:

`downloadSourceIds: ['BVnaGLvo', 'w4nVajB6']`

The API returned a download-source record containing a generated result ID, title, reported file size, URI fields, `downloadSourceId: 'w4nVajB6'`, `downloadSourceName: 'FitGirl'`, and `unavailableUris: []`.

The returned URI data included magnet/torrent metadata. The complete magnet URI and tracker list are intentionally **not reproduced in this public checkpoint** because they are unnecessary for the security finding and would publish redistribution metadata for copyrighted material.

### Source/client architecture

Source inspection showed that Hydra maintains a local `downloadSources` database and contains logic to synchronize source definitions with the Hydra API. The client can POST a source URL to `/download-sources`, store the returned definition locally, and synchronize local source IDs with API-provided definitions.

The evidence therefore supports this trust-boundary model:

```text
Hydra client
    |
    | source IDs / API requests
    v
Hydra API
    |
    | download-source metadata
    v
Configured community source records
    |
    | URI / torrent metadata
    v
Third-party download infrastructure
```

This does **not** establish that Hydra itself contacted every tracker or peer named inside a returned URI. That requires a separate controlled download observation.

## Antivirus control

The EICAR test string was blocked by Windows antivirus/AMSI while the PowerShell variable assignment was being parsed. The intended file-writing operation therefore did not establish that a valid EICAR test file was created.

The PowerShell output did not show a Defender threat-history record through the queried `Get-MpThreatDetection` / `Get-MpThreat` commands.

### Correct interpretation

- Defender/AMSI interception of the EICAR string: **observed**
- Valid EICAR test file creation: **not established**
- Defender quarantine/threat-history entry: **not observed in the captured cmdlet output**
- No further EICAR attempt is required for this research phase.

## Current research status

| Area | Status |
|---|---|
| Fresh Hydra runtime baseline | Complete |
| Download-source synchronization | Complete |
| Source IDs observed | Complete |
| Source names observed | Complete |
| API download-source response | Complete |
| Concrete URI/torrent metadata observed | Complete |
| Client source-synchronization code correlation | Complete |
| Actual third-party download | Not performed |
| Downloaded-file static analysis | Not performed |
| Executable/process test | Not performed |

## Finding status

No malware or safety verdict is established by this checkpoint.

The strongest current architectural finding is that **download-source metadata is an API-mediated trust boundary**: Hydra's client consumes source definitions and game-specific download metadata supplied through the Hydra API, while the eventual third-party download infrastructure remains a separate boundary.

## Next action

Use a small, legitimate free/open-source artifact for a controlled download experiment. Record:

1. pre-download process state
2. pre-download network state
3. pre-download filesystem state
4. download-time process/network changes
5. created/modified files
6. hashes of the resulting artifact
7. Defender/AV observations
8. static properties before any execution
9. execution only if the artifact is appropriate for a controlled test

Do not use the FitGirl/OnlineFix commercial-game records as the test artifact.
