# 4 November 2026 — Mindustry candidate review

## Decision

**No candidate currently meets all five eligibility conditions with the evidence available. Do not approve a Hydra download on the present evidence.**

## Candidate examined: Mindustry

- **Identity:** Mindustry, Steam app ID `1127400`.
- **Official project:** [mindustry.com](https://mindustry.com/) and [Anuken/Mindustry](https://github.com/Anuken/Mindustry).
- **Licence:** GPL-3.0, as reported by the candidate review.
- **Hydra version and listing:** Hydra v4.1.4 showed one download option attributed to OnlineFix.
- **Provenance/authorization:** Not established for this specific OnlineFix entry. The project licence does not authenticate the source entry, its payload, or its distribution route. No evidence matched the specific OnlineFix file/release to an official Mindustry release or established that the route is authorized.
- **Decision:** Does not qualify yet.

The catalogue/game page establishes only that an OnlineFix option is displayed. The download option was not opened and its URI was not exposed. No payload or source file was inspected.

## Other checked title

OpenTTD showed “No downloads available” in Hydra v4.1.4 and therefore did not qualify as an available Hydra test artifact.

## Actions not taken

- No download, installation, or execution.
- No source option was opened and no URI was exposed.
- No Hydra settings, configured sources, application files, or local checkout were changed.
- No source or candidate was treated as authorized based solely on its presence in Hydra.

## Research interpretation

This is a **candidate-selection blocker**, not evidence that Hydra or OnlineFix is malicious, and not evidence that Mindustry itself is unsafe. A project's open-source licence does not, by itself, prove that a third-party listing is an authorized distribution of that project.

A direct download from Mindustry's official release channel could support a separate artifact-analysis exercise. It would not test Hydra's download path and must be labelled separately.

## Next step

Continue looking for an exact free/open-source artifact that is actually available through the existing Hydra configuration and whose specific file/release can be matched to an official publisher/project and an authorized distribution route. Keep the search read-only. Do not weaken the eligibility criteria or change configured sources. Once a qualifying candidate is evidenced, prepare a fresh baseline and a download-only plan for explicit user approval. Installation or execution remains out of scope unless separately approved with an isolated test plan.

## Evidence limitation

This record reflects the supplied candidate-review report. The underlying OnlineFix payload/source file was not independently inspected in this step. No malware/safety conclusion is drawn.
