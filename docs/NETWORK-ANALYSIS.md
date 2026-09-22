# Network Analysis

## Goal

Document network activity attributable to Hydra and distinguish it from unrelated applications and normal local IPC.

## Baseline

The September 2026 baseline showed Hydra/Electron processes with established HTTPS connections and multiple localhost connections.

Localhost connections are not automatically suspicious; Electron applications commonly use local IPC.

## Required evidence

For a connection, record:

- process ID
- executable path
- local address/port
- remote address/port
- timestamp
- DNS/domain information when available
- operation being performed
- whether the connection can be correlated with source code

## Interpretation

An IP address alone is insufficient to establish intent. Correlate network observations with the process, operation, source code, and timing.
