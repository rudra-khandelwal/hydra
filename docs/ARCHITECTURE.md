# Architecture Notes

This document is a living research document.

## Purpose

Map Hydra's major components and runtime boundaries from the source code and controlled observations.

## Initial map

The repository is expected to contain an Electron-based desktop application with a frontend/main-process/native-dependency boundary and remote service integrations. The exact component map should be verified against the synchronized source tree rather than guessed.

## Research questions

- Which process owns each network connection?
- Which modules communicate with Hydra's backend services?
- Which modules handle download-source configuration?
- Which components invoke external download infrastructure?
- Which native dependencies have network/filesystem implications?
- Where are authentication credentials stored and used?
- Which operations run with elevated or privileged Windows behavior?
- Which filesystem locations are read or modified?

## Evidence rule

Add a component to this map only after source inspection or runtime evidence supports it.
