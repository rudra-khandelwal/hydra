# Findings

No final security verdict has been established.

## F-000 — Research framework

**Date:** 21 September 2026  
**Status:** Established

**Fact:** A controlled security research workflow was defined.

**Observation:** The project can be investigated by comparing baseline and post-operation state.

**Hypothesis:** Differential observation will make it easier to distinguish expected runtime behavior from unexpected behavior.

**Finding:** The methodology is suitable for continuing controlled testing.

**Next Action:** Continue with controlled operations and source correlation.

## F-001 — Hydra runtime HTTPS

**Date:** 21 September 2026  
**Status:** Observed; requires continued correlation

**Fact:** Hydra/Electron processes had established HTTPS connections during normal runtime.

**Observation:** The connections were associated with Hydra Electron processes.

**Hypothesis:** These connections support normal application/backend functionality.

**Finding:** Not yet a security finding; endpoint purpose should be correlated with application behavior and source code.

**Next Action:** Map endpoints to documented application functions and source code.

## F-002 — Third-party source separation

**Date:** 21 September 2026  
**Status:** Methodological finding

**Fact:** A community download source was configured in Hydra.

**Observation:** The source is outside the Hydra codebase.

**Finding:** Source configuration, download infrastructure, and downloaded software must be analyzed as separate trust boundaries.

**Next Action:** Perform controlled tests without conflating third-party file behavior with Hydra behavior.

## F-003 — API-mediated download-source metadata

**Date:** 25 September 2026  
**Status:** Observed; architectural finding, not a malware verdict

**Fact:** Hydra requested a game-specific download-sources API path with configured source IDs. The API response included a concrete source record with source ID/name and URI/torrent metadata.

**Observation:** Hydra relies on API-provided source metadata to resolve configured download options rather than embedding every source definition directly in the client.

**Finding:** Source metadata is an important trust boundary between the Hydra client, the Hydra API, configured community sources, and subsequent third-party download infrastructure. The evidence does not by itself establish that Hydra contacted every tracker/peer represented in a returned URI.

**Next Action:** Observe a legitimate controlled download and correlate network/process/filesystem changes with the downloader implementation.

## F-004 — Antivirus/AMSI control interception

**Date:** 25 September 2026  
**Status:** Observed control behavior

**Fact:** The EICAR test string was blocked while being assigned in PowerShell.

**Observation:** PowerShell reported that the script contained malicious content and was blocked by antivirus software. The subsequent capture did not show a Defender threat-history result through the queried cmdlets.

**Finding:** Antivirus/AMSI interception was demonstrated at the command/script-content stage. A valid EICAR test file and quarantine event were not established, so this should not be recorded as a completed file-quarantine test.

**Next Action:** No further EICAR testing is required for this phase. Use normal Defender scanning on the legitimate controlled artifact in the next experiment.

## F-005 — Controlled Hydra download remains unperformed

**Date:** 4 November 2026  
**Status:** Blocked pending a verified authorized artifact

**Fact:** No exact free/open-source artifact with verifiable publisher provenance and clear permission through the existing configured sources has been identified. OpenTTD displayed “No downloads available” in the latest checks.

**Observation:** The current blocker is test-artifact selection through the existing Hydra configuration, not a demonstrated Hydra download failure or malware finding.

**Finding:** The controlled Hydra download and resulting artifact inspection remain the principal unfinished experiment. Catalogue/source investigation should only continue insofar as it helps identify an authorized candidate.

**Limitations:** Defender status, download directory, available disk space, and a fresh process/network/filesystem baseline were not checked during the latest selection pass. No inference can be made about the safety of an artifact that was not downloaded and examined.

**Next Action:** Identify one exact, clearly authorized free/open-source artifact available through the existing Hydra configuration. Verify its publisher and distribution permission. Present the candidate and download-only plan for user approval before downloading. Do not change app settings or sources, or install/execute anything.

## F-006 — Mindustry OnlineFix option is not a verified authorized test artifact

**Date:** 4 November 2026  
**Status:** Candidate rejected pending provenance/authorization evidence

**Fact:** Hydra v4.1.4 displayed one OnlineFix download option for Mindustry (Steam app 1127400). The official project/repository and GPL-3.0 licence were identified, but the specific OnlineFix payload/release was not matched to an official project release and the distribution route was not verified as authorized.

**Observation:** The presence of an option and the project's open-source licence do not establish the provenance or authorization of that particular third-party entry. The option was not opened and its URI was not exposed.

**Finding:** Mindustry does not currently satisfy the test-artifact eligibility criteria. Do not approve a Hydra download based on the available evidence. This is not evidence that Hydra, OnlineFix, or Mindustry is malicious; it is an unresolved provenance/authorization gap.

**Other checked title:** OpenTTD displayed “No downloads available” and is not an available candidate under the current Hydra configuration.

**Limitations:** No payload/source file was downloaded or inspected. No installation/execution occurred.

**Next Action:** Continue read-only candidate identification against the existing configuration. Preserve all eligibility criteria. Once a specific candidate and distribution route are evidenced as authorized, prepare the fresh baseline and request explicit approval for a download-only experiment.

## F-007 — Second candidate search produced no approved artifact

**Date:** 4 November 2026  
**Status:** Candidate search complete for stated scope; Hydra download remains blocked

**Fact:** The supplied second read-only search report checked Mindustry, OpenTTD, Hedgewars, Battle for Wesnoth, and SuperTuxKart against the test-artifact requirements. No game met every requirement. Mindustry remained the strongest lead, with one OnlineFix option displayed, but that specific distribution could not be matched to an official release or otherwise authorized distributor. OpenTTD displayed “No downloads available”; no current downloadable entry was established for Hedgewars, Battle for Wesnoth, or SuperTuxKart.

**Observation:** The focused search does not establish exhaustive coverage of every Hydra catalogue record. A game's public source code or open-source licence does not authorize every third-party repack or distribution entry.

**Finding:** No candidate from this search is approved for download. Keep the controlled Hydra download experiment blocked until an exact existing source record can be tied to official publisher/release evidence or an explicitly authorized distributor. This result is not evidence that Hydra, OnlineFix, FitGirl, Mindustry, or any other named project is malicious.

**Limitations:** The report says no download link was opened and no URI exposed. No download, installation, execution, artifact hash/signature/AV/static analysis, or controlled download-time process/network/filesystem differential was performed.

**Next Action:** Do not continue broad catalogue searching by default. If useful, perform one narrow read-only provenance check of an exact existing source record against official project release data. If that evidence cannot establish authorization, stop candidate selection and preserve the blocker. Any later download requires a fresh baseline and explicit user approval; installation/execution requires separate approval and isolation.


## F-008 — Hydra Mindustry download completed; archive contents remain unverified

**Date:** 12 November 2026  
**Status:** Download and outer-archive scan complete; member analysis pending isolation

**Fact:** Hydra v4.1.4 displayed “Mindustry Build 06032021” (Steam app 1127400), 103.9 MB, from the existing onlinefix source. A Torrent download completed with automatic extraction and archive deletion disabled. It produced two RAR5 files; sizes and SHA-256 values are in the [dated checkpoint](checkpoints/2026-11-13-hydra-mindustry-download-scan.md).

**Observation:** Microsoft Defender custom scans of the folder and each archive returned exit code 0 and “found no threats.” The user reported real-time protection enabled, but this was not independently confirmed during the pass. The archives report encrypted headers. A metadata-only UnRAR listing (existing version 7.23 x64) shows a bundled Mindustry executable/runtime and third-party OnlineFix DLL/configuration files. No member was extracted or executed.

**Finding:** The Defender result applies to the archive files as scanned and does not establish that encrypted members are clean. The OnlineFix source page identifies Build 06032021, while the downloaded filename contains 23122020 and listed member timestamps are primarily 25 December 2020; the exact build remains unresolved. The specific distribution is not verified as an official or authorized release. No malware finding or safety verdict is made.

**Limitations:** No process/network/filesystem differential was captured during the transfer. No member hash, signature, PE/string analysis, or individual member scan was performed. No isolated VM/Sandbox was detected in the checked locations. No extraction, installation, launch, or execution occurred.

**Next Action:** Keep the files unopened on the everyday host. Obtain an isolated offline analysis environment before extraction. Then extract for static inspection and scan/hash each member there; any execution remains a separate explicitly approved experiment.
