# Research Agenda

## Completed / in progress

### 2026-09-21
- Establish baseline process/network/filesystem observation.
- Identify Hydra Electron processes.
- Identify Hydra-owned HTTPS connections.
- Document configured third-party source as a separate trust boundary.
- Establish research diary methodology.

### 2026-09-22
- Establish dedicated GitHub research repository.
- Preserve research history.
- Formalize repository structure and methodology.
- Publish the repository and sanitized research guide.
- Add GitHub Pages deployment workflow.
- Record and diagnose the first Pages deployment failure.
- Continue controlled runtime testing.

## Next phases

1. ~~Enable/configure GitHub Pages for the public repository.~~ Completed 22 September 2026.
2. ~~Rerun the Pages workflow and verify the deployment workflow.~~ Completed 22 September 2026; latest run #7 succeeded.
3. Verify local Git remote and repository history.
4. Synchronize the validated local Hydra source into the repository without unnecessary generated artifacts.
5. Add reproducible evidence templates and dated checkpoints.
6. Perform controlled download/install observations.
7. Analyze the resulting files and process/network behavior.
8. Correlate observations with source code.
9. Produce dated findings.
10. Review every future commit for credentials, personal data, raw sensitive logs, and other material that should not be public.

### Existing checkpoints
Historical agenda entries and completed milestones are retained in the research diary and dated checkpoints.

### 2026-11-04 — Controlled Hydra download candidate selection
- [x] Preserve prior security observations as historical completed work; repeat only for a defined evidence gap.
- [x] Record OpenTTD's “No downloads available” observation.
- [x] Record Mindustry's OnlineFix option as an unverified candidate, not an approved test artifact.
- [x] Perform a second focused read-only search covering Mindustry, OpenTTD, Hedgewars, Battle for Wesnoth, and SuperTuxKart.
- [x] Record that no checked game met every eligibility requirement.
- [ ] Identify an exact existing Hydra source entry whose specific distribution can be matched to an official release or explicitly authorized distributor.
- [ ] Verify exact publisher provenance and redistribution permission without opening download links or exposing URI values.
- [ ] Only after a qualifying candidate is evidenced, prepare a fresh read-only pre-download baseline and present the exact download-only plan for explicit approval.
- [ ] Perform the approved Hydra download-only experiment; capture sanitized process/network/filesystem deltas and artifact metadata, hashes, signatures, Defender results, and static inspection.
- [ ] Report evidence before considering installation or execution; that requires a separate explicit approval and isolated environment.

**Current disposition:** No test artifact is approved. This is a provenance/authorization blocker, not evidence that Hydra or a source is malicious. Catalogue coverage is not the main workstream unless a targeted read-only check helps identify a qualifying artifact. See [second candidate search](checkpoints/2026-11-04-second-candidate-search.md), [Mindustry review](checkpoints/2026-11-04-mindustry-candidate-review.md), and [security continuation checkpoint](checkpoints/2026-11-04-security-continuation.md).
