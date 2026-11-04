# PuTTY 0.85 embedded-help metadata checkpoint — 4 November 2026

**Research stream:** Direct official-publisher artifact analysis. This is separate from the blocked Hydra download-path experiment.  
**Target:** Official PuTTY 0.85 64-bit x86 standalone `putty.exe`.  
**Scope:** Read-only static inspection; no execution, launch, installation, or loading.

## Artifact identity and integrity

- File size: **1,706,136 bytes**.
- SHA-256: `d01fdb5aae8f112526040a39b0bfb9e27d813003178645e65f8d1cfdb2a26c87`.
- The SHA-256 was reported unchanged across the PE, strings, entropy, resource, and embedded-help inspections.
- Earlier reported verification: exact match to the official `w64/putty.exe` entry in the official SHA-256 manifest; Windows Authenticode status Valid with signer Simon Tatham; executable GPG signature Good signature; clear-signed `sha256sums.gpg` Good signature. GPG fingerprint: `1A07 DAC0 F220 CF12 248E A719 5C67 D0F8 8BC3 E5B5`. Local GPG key trust was not certified, so an independent trust path remains unestablished.
- Windows Defender command-line scan reported no threats; Defender real-time status was not independently confirmed because the status cmdlet failed.

## Completed static inspection

### PE structure

The existing `dumpbin` inspection completed successfully for `/HEADERS`, `/IMPORTS`, and `/EXPORTS`, each with exit code 0. The tool was the already-installed Visual Studio Build Tools `dumpbin.exe` (reported file metadata version 14.44.35229.0).

- Machine type: x64 / `0x8664`.
- PE characteristics: `0x22`.
- Subsystem: Windows GUI.
- Sections: `.text`, `.rdata`, `.data`, `.pdata`, `.00cfg`, `.gxfg`, `.tls`, `_RDATA`, `.rsrc`, and `.reloc`.
- Imports include GDI32, IMM32, OLE32, USER32, KERNEL32, SHELL32, COMDLG32, and ADVAPI32, with ordinary GUI, file, process, registry, and shell-related functions.
- Static import listing did not directly list WS2_32 or Wsock32. String extraction found those library names alongside `LoadLibraryA/ExA/W` and `GetProcAddress`. This is consistent with possible dynamic loading, but does not establish runtime loading or network activity.
- No exports were listed.

### Printable strings

A PowerShell/.NET raw-byte scan extracted 10,241 ASCII strings and 1,045 UTF-16LE strings (minimum five printable characters, with byte offsets).

Reviewed examples included the official PuTTY project URL, project support email, Sectigo/UserTrust certificate CRL/OCSP metadata, the placeholder `demo-server.example.com`, `0.0.0.0`, socket DLL names, `Running pre-connect command: %s`, process/shell API names, registry API names, and dynamic-loader API names. The reviewed strings had plausible PuTTY/contextual explanations; the scan did not identify an unexplained production endpoint or clearly malicious indicator. Strings alone do not prove behavior.

### Section entropy

Shannon entropy was calculated over section raw bytes using PowerShell/.NET read-only byte-array parsing:

| Section | Raw offset | Raw size | Entropy (bits/byte) |
|---|---:|---:|---:|
| `.text` | `0x400` | `0xED400` | 6.4480 |
| `.rdata` | `0xED800` | `0x42C00` | 5.4388 |
| `.data` | `0x130400` | `0x1000` | 2.0664 |
| `.pdata` | `0x131400` | `0x7200` | 5.9162 |
| `.00cfg` | `0x138600` | `0x200` | 0.5092 |
| `.gxfg` | `0x138800` | `0x2C00` | 5.1442 |
| `.tls` | `0x13B400` | `0x200` | 0.0000 |
| `_RDATA` | `0x13B600` | `0x200` | 3.2645 |
| `.rsrc` | `0x13B800` | `0x5C600` | 7.8331 |
| `.reloc` | `0x197E00` | `0x2200` | 5.4436 |

High entropy in `.rsrc` was initially unresolved. The subsequently identified compiled HTML Help payload provides a plausible explanation; entropy alone is not proof of packing or maliciousness.

### PE resources

A raw-byte PE resource parser found **24 resource leaves**, all language ID 1033 (`0x0409`, English–United States), with no malformed or out-of-bounds branches reported:

- 12 ICON image leaves.
- 2 GROUP_ICON leaves.
- 7 DIALOG leaves.
- 1 VERSION resource.
- 1 MANIFEST resource.
- 1 numeric resource type ID 2000 (365,163 bytes).

The VERSION resource reports FileVersion and ProductVersion `0.85.0.0`, describes PuTTY as “SSH, Telnet, Rlogin, and SUPDUP client,” and includes “Release 0.85 (with embedded help)” and Simon Tatham.

The UTF-8 XML manifest declares Microsoft Common Controls 6.0, `dpiAware=true`, and PerMonitorV2 DPI awareness. It has no explicit `requestedExecutionLevel` and no compatibility/`supportedOS` element. No elevation behavior was inferred from that absence.

### Embedded HTML Help metadata

The type ID 2000 resource begins at file offset `0x13DCF0`, is 365,163 bytes, and begins with `ITSF`. Its validated raw range is `[0x13DCF0, 0x196F5B)`, within the executable.

The raw-byte parser reported:

- ITSF v3, header length `0x60`.
- Language ID `0x0809`.
- Section 0 at relative offset `0x60`, length `0x18`.
- Directory at relative offset `0x78`, length `0x6054`.
- Data offset `0x60CC`.
- ITSP v1, header length `0x54`, chunk size 4096, index depth 2, root index chunk 5.
- PMGL listing chain chunks 0 through 4; six directory chunks total, comprising five PMGL listing chunks and one PMGI index chunk.
- **561 PMGL directory entries**.
- 9 entries in section 0 marked uncompressed; 552 entries in section 1 marked MSCompressed/LZX. Section 0 offsets were mapped and range-checked against the resource. Section 1 offsets/lengths remain logical section coordinates; no compressed raw mapping was attempted.
- Names include `/index.html` (landing-page candidate by filename only) and `/chm.css`; 542 HTML files and one CSS file are listed. No common executable/script filename extensions were present.
- The ITSF timestamp field was recorded as raw `0x78563412`; interpretation remains uncertain. Unknown header fields remain marked unknown.

ITSF/ITSP/PMGL layouts and directory entry encoding were cross-checked against Wine's CHM parser, Apache Tika's CHM directory-entry documentation, and CHMLib section definitions. No internal HTML, CSS, image, or other file contents were read, rendered, extracted, decompressed, or executed. The PMGI index payload was not decoded. The `#SYSTEM` metadata was not read, so the actual default topic was not confirmed. The `/index.html` label is only a filename-based candidate.

## Evidence files reported locally

All are under the local, non-public evidence directory for PuTTY 0.85; their local paths are intentionally omitted from this public checkpoint:

- `dumpbin-headers.txt`, `dumpbin-imports.txt`, `dumpbin-exports.txt`
- `strings-ascii.txt`, `strings-utf16le.txt`
- `resource-inventory.txt`, `resource-parser.ps1`
- `embedded-help-metadata.txt`, `embedded-help-parser.ps1)

The Codex reports state the target was never loaded, launched, installed, or executed. No Hydra application files, settings, configured sources, or app checkout files were changed. No new analysis tool was installed.

## Assessment and limitations

The inspected evidence has not identified a clearly malicious indicator. Several observations are consistent with expected PuTTY behavior and embedded help. This is **not a safety verdict** and does not prove the program is safe.

Remaining gaps include:
- No execution/dynamic behavior analysis.
- No observation of actual network connections or API calls.
- No decoding/rendering or content-level inspection of the embedded help payload.
- No confirmation of the help system's default topic.
- No independent local GPG key trust certification.
- Defender real-time status was not independently confirmed.
- Static imports and strings cannot establish which code paths execute or whether dynamic libraries are actually loaded.

## Hydra experiment boundary

The Hydra download-path experiment remains **blocked**. No exact existing configured Hydra source entry was matched to an official release or explicitly authorized distribution. This PuTTY artifact was obtained directly from its official publisher and must not be counted as a Hydra-mediated download test. Do not expand catalogue searching by default; resume the Hydra path only if new exact-source provenance/authorization evidence becomes available.

## Five-message cadence

This is an early checkpoint because materially new static-analysis evidence arrived. The prior handoff counter was 0/5; this user message is counted as **1/5**. Continue counting future Hydra research messages and perform the full cadence update at 5/5. The cadence is manual, not automatic.
