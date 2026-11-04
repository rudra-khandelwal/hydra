# Official-Publisher Static-Analysis Candidate Review

**Date:** 4 November 2026  
**Status:** Candidate research documented; no artifact approved or downloaded

## Context and separation of experiments

The controlled Hydra download-path experiment remains blocked. The focused checks of existing Hydra v4.1.4 entries did not identify an exact artifact whose distribution could be independently matched to an official free/open-source release or an explicitly authorized distributor. Mindustry's OnlineFix option remains unapproved because the specific distribution was not linked to or authorized by the official project.

This checkpoint covers a different possible experiment: analysis of an artifact obtained directly from its official publisher. Such an experiment can inform analysis of that artifact, but **does not test Hydra's download path and does not remove the existing Hydra experiment blocker**.

## Candidate evidence (based on the current research report)

The details below are the evidence gathered in the supplied candidate report. A field not verified there is explicitly left unresolved; this checkpoint does not imply a fresh independent verification of the linked pages.

### 1. PuTTY 0.85 — provisional preferred candidate

- **Official release source:** [PuTTY latest release page](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
- **Release date reported:** 16 August 2026.
- **Licence:** MIT, according to the supplied report and linked official licence page: [PuTTY licence](https://www.chiark.greenend.org.uk/~sgtatham/putty/licence.html).
- **Windows package formats reported:** MSI, EXE, and ZIP.
- **Signature verification guidance:** Official project guidance for GPG and Authenticode was identified: [PuTTY keys and signature guidance](https://www.chiark.greenend.org.uk/~sgtatham/putty/keys.html).
- **Package size:** Not verified.
- **Specific package signature/checksum:** The report identifies verification guidance, but does not establish a signature/checksum result for a particular package file.
- **Publisher identity:** Official project release page is the identified distribution source; the exact signing identity and expected certificate details still need to be recorded against the selected package before any download is approved.
- **Assessment:** Strong provisional candidate because the reported licence is clear and the project documents signature-verification procedures. Package size and exact package-specific signature details remain open.

### 2. 7-Zip 26.05 — viable alternative with licensing caveat

- **Official download page:** [7-Zip downloads](https://www.7-zip.org/download.html)
- **Official repository:** [ip7z/7zip](https://github.com/ip7z/7zip)
- **Release/date reported:** Version 26.05, dated 21 October 2026.
- **Windows package reported:** x64 EXE installer, approximately 1.6 MB.
- **Licence:** Reported as mostly LGPL, with some BSD-3-Clause code and an unRAR restriction for some parts.
- **Specific installer signature/checksum:** Not verified in the supplied report.
- **Publisher identity:** Official project website and repository identified; package-specific signing evidence remains unverified.
- **Assessment:** Compact package and clear official location, but the licence is mixed and the specific installer’s signature/checksum has not been established. The installer format also means static inspection should be planned carefully without executing it.

### 3. Notepad++ 8.9.8.1 — incomplete verification

- **Official repository and releases:** [Notepad++ repository](https://github.com/notepad-plus-plus/notepad-plus-plus)
- **Release/version reported:** 8.9.8.1.
- **Licence:** GPL, as identified in the official repository.
- **Windows packages and SHA-256:** Official release metadata was reported to list Windows packages and SHA-256 digests.
- **Release date/current stable status:** Not confirmed in the supplied report.
- **Package size:** Not confirmed.
- **Publisher/signature identity and Authenticode status:** Not confirmed.
- **Assessment:** Plausible candidate, but too many package-level details remain unresolved for a recommendation at this stage.

## Provisional comparison

| Candidate | Reported package size | Licence evidence | Package signature/checksum evidence | Current assessment |
|---|---:|---|---|---|
| PuTTY 0.85 | Not verified | MIT | Official GPG/Authenti­code guidance reported; exact package result not verified | Provisional preference |
| 7-Zip 26.05 | ~1.6 MB x64 EXE | Mixed LGPL/BSD-3-Clause with unRAR restriction | Specific installer signature/checksum not verified | Viable alternative |
| Notepad++ 8.9.8.1 | Not verified | GPL | Release metadata reportedly lists SHA-256; exact package/signature details incomplete | Lead only |

## Recommended next candidate

**PuTTY 0.85 is the provisional preferred candidate, not an approved download.** The reason is the reported MIT licence and official documentation for GPG and Authenticode verification. The missing package size and package-specific verification details must be resolved before asking for approval.

No candidate is declared safe. Open-source licensing, official hosting, a checksum, or a digital signature each provides only limited evidence and must not be treated as a complete security verdict.

## Proposed read-only and static-analysis procedure

### Before any download (read-only baseline)
1. Record Windows Defender state and relevant protection settings without changing them.
2. Record the intended download directory's existing contents and metadata.
3. Record available disk space.
4. Capture process and established network-connection baselines.
5. Record the exact official release page, package filename, package type, expected size, publisher/signing identity, and published checksum/signature instructions for the one specifically selected package.
6. Present the exact candidate and proposed action for explicit user approval.

### After a separately approved official download
1. Record the downloaded filename, size, timestamp, and source page.
2. Calculate SHA-256 locally and compare it with an independently obtained official published digest, if one exists.
3. Verify Authenticode signature and signer identity where applicable; separately verify GPG signatures where the publisher supplies them and the verification process is appropriate.
4. Record Microsoft Defender scan results and any detections without disabling protections or creating exclusions.
5. Inspect the package statically: file type, archive/container structure, member names, embedded executables, scripts, manifests, unexpected payloads, and suspicious paths or file extensions.
6. Preserve hashes and sanitized inspection output. Do not execute installer code, scripts, binaries, or embedded payloads.

### Evidence limits
- A matching hash establishes byte-for-byte correspondence with the referenced digest, not that the digest source is trustworthy or the file is harmless.
- A valid digital signature links a file to a signing identity and indicates integrity since signing; it does not establish benign behavior.
- A clean Defender result is not proof that a file contains no malware.
- Static inspection can identify suspicious structure/content but cannot establish all runtime behavior.
- A direct official-publisher download does not test Hydra's downloader, source metadata, peer/HTTP behavior, or Hydra-created filesystem/network effects.
- Installation or execution testing remains out of scope and requires separate explicit approval plus an isolated environment.

## Actions not performed

- No package or installer was downloaded.
- No installation or execution occurred.
- No Hydra application source, settings, configured source, or local application checkout was modified.
- No file was scanned or statically inspected in this phase.
- No candidate is approved for download.

## Decision gate

The immediate next task is to close the evidence gaps for PuTTY 0.85 using official sources only: confirm the precise package choice and size, establish the expected signing identity and package-specific verification route, and then present the exact proposed artifact to the user. Stop before download and wait for explicit approval.
