# Hydra Mindustry download and scan checkpoint — 13 November 2026

**Research stream:** Controlled download through Hydra v4.1.4 from an existing configured community source.  
**Experiment performed:** 12 November 2026.  
**Checkpoint prepared:** 13 November 2026.  
**Scope:** Downloaded artifact inventory, Defender scan, and archive-directory metadata only. No extraction, installation, launch, or execution occurred.

## Why this candidate was used

Earlier research did not find an existing Hydra entry whose exact distribution was verified as an official or explicitly authorized release. The user then directed the audit to choose a small game visible in Hydra and approved a download for malware investigation. Mindustry was selected because Hydra displayed one OnlineFix option and the game is a known open-source project. This user decision authorized a security sample; it does **not** establish that the OnlineFix distribution is official or authorized.

## Hydra selection and download

- Hydra version shown: **v4.1.4**.
- Game: **Mindustry**, Steam app ID **1127400**.
- Hydra option: **“Mindustry Build 06032021”**, **103.9 MB**, source **onlinefix**, dated **26/12/2020**.
- Downloader: **Torrent**.
- Download directory shown in Hydra: the user's Downloads folder; reported here as `<Downloads>\Mindustry`.
- Automatic extraction and archive deletion were visibly unchecked before starting.
- Hydra showed one completed download. The torrent progress fluctuated and included periods of very low speed; the transfer eventually completed.
- No full download URI, tracker, peer address, credentials, cookies, or authorization header was recorded.

## Downloaded files and integrity

| File | Size (bytes) | SHA-256 |
|---|---:|---|
| `Mindustry.Build.23122020-OFME.rar` | 104,760,990 | `18d6fb40c1ac8640fc5a40ace080a957e45275eba66fb9df683241d3d1c289ef` |
| `Fix Repair/Mindustry_Fix_Repair_Steam_Generic.rar` | 4,264,926 | `15f40876c6bca6357ad2e02b5adf66484a31409f3390049d22a49a88fc0b5de0` |

Both begin with the RAR 5 signature bytes `52 61 72 21 1A 07 01 00`. Hashes and sizes were checked after Defender scanning; they were unchanged from the initial post-download record. No publisher checksum or signature for these archives was established.

## Source-page cross-check and archive listing

The source's public [Mindustry entry](https://online-fix.me/games/sandbox/16371-mindustry-po-seti.html) states that its package is Build 06032021 and documents a shared archive password. The password value is intentionally not reproduced in this public checkpoint.

Using the already-installed **UnRAR 7.23 x64**, a metadata-only `lt` listing was performed with the source-provided password. Both commands exited 0. This listed archive directory records; no files were extracted and no member file contents were printed. The sanitized command form was:

```text
UnRAR.exe lt -p[redacted] -cfg- <archive>
```

The main archive reports **RAR 5 encrypted headers** and lists `Mindustry.exe`, a bundled `jre` tree, `steam_api64.dll`, `steam_api64.of`, `OnlineFix64.dll`, `OnlineFix.ini`, and `OnlineFix.url`. The separate Fix Repair archive lists the Steam API files and OnlineFix files. These names are consistent with a third-party multiplayer-fix package, but their presence is not evidence that the files are benign or malicious.

**Unresolved build discrepancy:** Hydra's option says Build 06032021, while the main archive filename contains `23122020`; listed file timestamps are primarily from 25 December 2020. The OnlineFix page identifies Build 06032021 and says it was updated on 26 March 2021. These filename/timestamp differences may reflect stale packaging metadata, but the actual game build was not verified from file contents or an official hash.

## Defender scan

The user reported Microsoft Defender real-time protection was on. Its status was not independently read through Windows settings or status APIs during this pass.

The already-installed Microsoft Defender platform tool `MpCmdRun.exe` (platform folder version **4.18.26100.4-0**) ran custom scans on the download folder and on each RAR file:

```text
MpCmdRun.exe -Scan -ScanType 3 -File <Downloads>\Mindustry
MpCmdRun.exe -Scan -ScanType 3 -File <archive>
```

Each scan returned exit code **0** and reported **“found no threats.”** This is a clean result for the files as scanned, not proof that the archives or their contents are safe. The Defender output does not state whether it inspected every encrypted member.

## Evidence handling, preservation, and limitations

- No archive was extracted, installed, launched, or executed. The folder inventory contained the two RAR archives only.
- No signatures or hashes were checked for the archive members because they were not extracted.
- No process/network/filesystem differential was captured during the torrent transfer. Therefore this checkpoint does not establish tracker/peer identities or a complete Hydra runtime network profile.
- No static PE/string inspection of `Mindustry.exe` or the listed DLLs has occurred.
- The OnlineFix entry is a community distribution. The exact payload has not been matched to an official Mindustry release, and source authorization remains unverified.
- Windows Sandbox was not found at `C:\Windows\System32\WindowsSandbox.exe`; common VirtualBox/VMware executable paths checked were also absent. This does not prove no virtual-machine capability exists by another route.
- The local Hydra application checkout and its settings/sources were not edited. Existing app-checkout changes remain preserved.

## Assessment and next action

**Confirmed:** Hydra completed the selected Torrent item; two RAR5 archives are present; Defender reported no threats for the archive files; archive-member metadata identifies a game executable, bundled Java runtime, and OnlineFix components.

**Not established:** safety of archive contents, exact Mindustry build, official/authorized distribution status, runtime behavior, or whether Defender inspected encrypted members.

**Recommendation:** Do not launch the game or extract these archives on the everyday Windows environment. The next meaningful step is to make an isolated, offline analysis environment available, then extract only for static inspection and scan/hash the resulting files there. Execution, if ever considered, remains a separate decision requiring explicit approval and isolation. If isolation is unavailable, preserve the archives unopened or remove them after the evidence-retention decision; do not treat the Defender result as a safety verdict.
