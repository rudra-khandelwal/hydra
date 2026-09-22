# Security Research Methodology

## Phase 1 — Baseline

Record the system state before the controlled test:

- processes
- established network connections
- relevant files
- timestamps
- Hydra version/commit

## Phase 2 — Launch

Start Hydra using the validated development environment and record:

- process tree
- executable paths
- command lines
- network destinations
- local IPC activity

## Phase 3 — Controlled operation

Perform one defined operation at a time and record changes.

Examples:

- opening settings
- authenticating
- browsing configured sources
- initiating a controlled download
- installing a test application
- launching the installed application

## Phase 4 — Differential analysis

Compare before/after:

- processes
- network
- filesystem
- hashes
- configuration changes

## Phase 5 — Validation

Where appropriate:

- inspect source code related to the observation
- calculate hashes
- run Windows Defender/AV checks
- repeat the experiment
- test an alternative explanation

## Phase 6 — Reporting

Record:

**Fact → Observation → Hypothesis → Finding → Next Action**

Do not upgrade an observation to a finding without supporting evidence.
