# 4 November 2026 — Second read-only candidate search

## Result

**No game checked meets every test-artifact requirement.** No Hydra download is approved.

The search reviewed well-known free/open-source candidates against the existing Hydra v4.1.4 configuration. The required conditions remain cumulative: exact project identity, official publisher/project evidence, licence and redistribution terms, a current Hydra download option, an identified existing source, and evidence that the specific distribution route is official or otherwise authorized.

## Candidate table

| Game | Official project evidence | Hydra observation | Decision |
|---|---|---|---|
| Mindustry (Steam App ID 1127400) | Official site: https://mindustry.com/ ; repository: https://github.com/Anuken/Mindustry ; official releases: https://github.com/Anuken/Mindustry/releases . The supplied report identifies GPL-3.0. | One option displayed under OnlineFix in Hydra v4.1.4. The exact payload/release and OnlineFix authorization were not verified. The option was not opened and its URI was not exposed. | Promising lead, but ineligible. Do not approve download. |
| OpenTTD | Official project licensing/distribution evidence was not reproduced in the supplied report. | “No downloads available.” | Not currently available as a Hydra test candidate. |
| Hedgewars | Official public project/source/licensing information exists, but the supplied report did not establish a current Hydra option. | No current downloadable entry established. | Ineligible: Hydra availability not established. |
| Battle for Wesnoth | Official public project/source/licensing information exists, but the supplied report did not establish a current Hydra option. | No current downloadable entry established. | Ineligible: Hydra availability not established. |
| SuperTuxKart | Official public project/source/licensing information exists, but the supplied report did not establish a current Hydra option. | No current downloadable entry established. | Ineligible: Hydra availability not established. |

## Scope and limitations

- This was a focused search of named, well-known open-source game candidates, not an exhaustive enumeration of every Hydra catalogue record.
- The supplied report states that the observed catalogue had the existing OnlineFix and FitGirl sources.
- A game's open-source licence does not by itself authorize every third-party repack, mirror, or source entry.
- No download option was opened; no download URI was exposed.
- No download, installation, or execution occurred.
- No Hydra settings, source configuration, application files, or local application checkout were changed.
- No inference of malware or safety follows from a candidate failing the provenance/authorization gate.

## Decision

There is still no qualifying test artifact through the existing Hydra configuration. Keep the controlled Hydra download experiment blocked. Do not weaken the eligibility criteria or change sources to manufacture a candidate.

The next useful step is not another broad game-name search. It is to identify an exact existing source record whose distribution can be independently tied to the official publisher/project or an explicitly authorized distributor. Only after that evidence is documented should a fresh read-only pre-download baseline be prepared and a precise download-only plan be presented for approval.

A separate direct-from-publisher artifact examination could be considered as a different experiment, but it would not test Hydra's download path and must be labelled accordingly.
