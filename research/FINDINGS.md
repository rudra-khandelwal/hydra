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

**Fact:** Hydra requested `GET /games/steam/1817070/download-sources` with source IDs `BVnaGLvo` and `w4nVajB6`.

**Observation:** The API response included a concrete record with `downloadSourceId: 'w4nVajB6'`, `downloadSourceName: 'FitGirl'`, and URI/torrent metadata.

**Hypothesis:** Hydra relies on API-provided source metadata to resolve configured download options rather than embedding every source definition directly in the client.

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

**Fact:** The latest report states that Hydra v4.1.4 showed “No downloads available” for OpenTTD. No alternative artifact with verifiable official publisher provenance and clear permission through the existing configured sources was identified. No download was started.

**Observation:** The current blocker is test-artifact selection through the existing Hydra configuration, not a demonstrated Hydra download failure or malware finding.

**Finding:** The controlled Hydra download and resulting artifact inspection remain the principal unfinished experiment. The catalogue/source investigation should only continue insofar as it helps identify an authorized candidate.

**Limitations:** Defender status, download directory, available disk space, and a fresh process/network/filesystem baseline were not checked in the latest artifact-selection pass. No inference can be made about the safety of an artifact that was not downloaded and examined.

**Next Action:** Identify one exact, clearly authorized free/open-source artifact available through the existing Hydra configuration. Verify its publisher and distribution permission. Present the candidate and download-only plan for user approval before downloading. Do not change app settings or sources, or install/execute anything.


## F-006 — Mindustry OnlineFix option is not a verified authorized test artifact

**Date:** 4 November 2026  
**Status:** Candidate rejected pending provenance/authorization evidence

**Fact:** The supplied read-only candidate report states that Hydra v4.1.4 displayed one OnlineFix download option for Mindustry (Steam app 1127400). The official project/repository and GPL-3.0 licence were identified, but the specific OnlineFix payload/release was not matched to an official project release and the distribution route was not verified as authorized.

**Observation:** The presence of an option and the project's open-source licence do not establish the provenance or authorization of that particular third-party entry. The option was not opened and its URI was not exposed.

**Finding:** Mindustry does not currently satisfy the test-artifact eligibility criteria. Do not approve a Hydra download based on the available evidence. This is not evidence that Hydra, OnlineFix, or Mindustry is malicious; it is an unresolved provenance/authorization gap.

**Other checked title:** OpenTTD displayed “No downloads available” and is not an available candidate under the current Hydra configuration.

**Limitations:** No payload/source file was downloaded or inspected. No installation/execution occurred.

**Next Action:** Continue read-only candidate identification against the existing configuration. Preserve all eligibility criteria. Once a specific candidate and distribution route are evidenced as authorized, prepare the fresh baseline and request explicit approval for a download-only experiment. See [Mindustry candidate review](checkpoints/2026-11-04-mindustry-candidate-review.md).
