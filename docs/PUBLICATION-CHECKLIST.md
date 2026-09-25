# Public Repository Safety Checklist

This repository is already public.

This checklist is therefore an **ongoing publication-safety control**, not a pre-publication gate.

## Every commit

- [ ] No passwords, access tokens, API keys, cookies, private keys, or recovery codes.
- [ ] No raw credential-bearing or privacy-sensitive logs.
- [ ] No unnecessary personal or machine-specific data.
- [ ] No proprietary/copyrighted downloaded software artifacts.
- [ ] No credentials copied from local `.env` files.
- [ ] Public claims are supported by the recorded evidence.
- [ ] Research hypotheses are clearly labelled as hypotheses.
- [ ] Third-party download infrastructure is kept separate from Hydra findings.
- [ ] Build/test output added to Git is intentional and documented.

## Documentation consistency

- [ ] Repository visibility is described as public.
- [ ] Live guide URL is current.
- [ ] Project Memory reflects current operating rules.
- [ ] Repository Map matches the actual tree.
- [ ] Diary/Agenda are updated for substantive changes.
- [ ] Validation status distinguishes implemented, deployed, and live-verified behavior.

## GitHub Pages / Actions

- [ ] Workflow completes successfully.
- [ ] Workflow warnings/annotations are reviewed.
- [ ] Current action/runtime versions are not silently relying on deprecated runtimes.
- [ ] The newest run is used as the deployment status; cancelled superseded runs are treated as historical.

## Research safety

- [ ] Keep Hydra, API/auth, community source, third-party download infrastructure, and downloaded artifact as separate trust boundaries.
- [ ] Do not perform unauthorized access or DRM bypass.
- [ ] Use legitimate free/open-source artifacts for controlled download tests.
