# Project Goal

## Primary goal

Maintain a reproducible, evidence-first Windows research workspace for understanding, building, and defensively evaluating the open-source Hydra Launcher project.

The project has two connected tracks:

1. **Build track** — reproduce a working Windows development build with a controlled toolchain.
2. **Research track** — measure runtime behavior and correlate observations with source code without jumping to unsupported security conclusions.

## Scope

### In scope

- official upstream source inspection
- reproducible Windows builds
- dependencies and native build tooling
- Electron/process behavior
- network observations
- filesystem observations
- configuration and integration behavior
- controlled downloads of legitimate free/open-source artifacts
- hashes and static analysis
- Windows Defender/AV observations
- dated findings and evidence

### Out of scope

- DRM bypass
- credential theft or brute-force access
- unauthorized system/account access
- redistribution of copyrighted software
- hiding secrets inside the public guide
- declaring software safe/unsafe without evidence

## Research phases

### Phase A — Build foundation
Status: substantially complete.

### Phase B — Runtime baseline
Status: substantially complete.

### Phase C — Source/API/trust-boundary mapping
Status: active and partially complete.

### Phase D — Controlled legitimate download
Next major research phase.

### Phase E — Artifact analysis
Process, network, filesystem, hash, static inspection, and AV/Defender correlation.

### Phase F — Source correlation
Tie observed behavior to concrete code paths.

### Phase G — Findings
Publish only findings supported by evidence, with limitations and alternative explanations.

## Success criteria

The project is successful when:

- the Windows build is reproducible;
- the runtime baseline is repeatable;
- trust boundaries are clearly separated;
- controlled experiments have dated evidence;
- observations are correlated to source code where possible;
- findings state uncertainty honestly;
- the public repository contains no secrets or sensitive raw evidence;
- the live guide accurately reflects the repository state;
- the project history remains auditable.

## Method

Every substantive research checkpoint follows:

**Fact → Observation → Hypothesis → Finding → Next Action**

The project measures first and concludes second.
