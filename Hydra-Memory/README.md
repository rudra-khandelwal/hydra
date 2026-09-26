# Hydra — Master Memory Lane

Last consolidated: 2026-09-26

## Purpose
Canonical handoff record for continuing the user's Hydra Launcher work across future chats. Read this before continuing Hydra work. Do not repeat setup that is already confirmed working. Prefer current repository files over old chat instructions when the project changes. Distinguish confirmed facts from assumptions, reports, and unresolved issues.

## Repository
Official Hydra repository: https://github.com/hydralauncher/hydra
User work repository: https://github.com/rudra-khandelwal/hydra
Memory location: Hydra-Memory/README.md
Default branch: main

## Current official repository state checked on 2026-09-26
Version: 4.1.4
Electron dependency: ^41.10.3
Yarn: 1.22.22
Node.js/TypeScript/React/Vite/Electron architecture with Rust native code.
Current native torrent architecture uses Rust/libtorrent rather than the older Python/libtorrent route.

## User's Windows environment
Windows 11, build 10.0.26200.9457
Main project: C:\Users\rudra\Downloads\hydra
Node.js: 24.19.0
Yarn: 1.22.22
Python: 3.14.6
Rust:
- rustc 1.98.1 (48a229cea 2026-09-01)
- cargo 1.98.1 (797e8a9bc 2026-08-05)
- host x86_64-pc-windows-msvc

VS2022 Build Tools:
- C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
- version 17.14.41
- MSVC 14.44.35207
- compiler 19.44.35229
- MSBuild 17.14.41
- Windows SDK 10.0.26100.0

VS2026 Build Tools also exist at C:\Program Files (x86)\Microsoft Visual Studio\18\BuildTools. Earlier native/node-gyp problems were caused by VS2026/toolchain selection. The confirmed working native setup uses VS2022.

vswhere path:
C:\Program Files (x86)\Microsoft Visual Studio\Installer\vswhere.exe

## Confirmed working native build configuration
Use a VS2022 x64 developer environment.

Known working variables:
CMAKE_GENERATOR=Visual Studio 17 2022
CMAKE_GENERATOR_PLATFORM=x64
VCPKG_VISUAL_STUDIO_PATH=C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
VCPKG_PLATFORM_TOOLSET=v143

Developer command prompt:
"C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\Common7\Tools\VsDevCmd.bat" -arch=x64

Native build detected:
C:/Program Files (x86)/Microsoft Visual Studio/2022/BuildTools/VC/Tools/MSVC/14.44.35207/bin/Hostx64/x64/cl.exe

## Confirmed successful native build
Native build completed successfully.

Observed native packages:
- Boost 1.92.0
- libdatachannel 0.24.5
- libjuice 1.7.2#1
- libtorrent 2.1.1
- OpenSSL 3.6.4
- nlohmann-json 3.12.0#2
- usrsctp 0.9.5.0#4

Outputs included:
- hydra_torrent_bridge.dll
- torrent_bridge_test.exe
- hydra-native/hydra-native.node

Test:
torrent_bridge_ownership passed
100% tests passed out of 1

This is a confirmed-good baseline. Do not recommend reinstalling Rust, VS2022 Build Tools, vcpkg, or the whole project without evidence of a new failure.

## Major problems already solved

### Python/libtorrent
Old attempt using python -m pip install -r requirements.txt failed because a compatible libtorrent package was not found for Python 3.14.6. This was an outdated route relative to the current native Rust architecture. Do not revert to Python/libtorrent unless current source explicitly requires it.

### Rust cargo ENOENT
Initial yarn installation failed with spawn cargo ENOENT. Rustup/toolchain installation fixed this.

### Rust C++ prerequisites
Rust requested C++ build tools. Visual Studio Build Tools with Desktop development with C++ were installed.

### VS2026/CMake generator
CMake could not create the Visual Studio 18 generator during an earlier attempt. CMake listed both Visual Studio 18 2026 and Visual Studio 17 2022. Forcing the VS2022 generator/platform and vcpkg toolset fixed the native build.

### node-gyp/classic-level
Some yarn installs entered electron-builder/@electron/rebuild and classic-level node-gyp work. A failed run showed VS2026 environment contamination. Use the VS2022 developer environment when this appears again.

### vswhere
If vswhere is not recognized, use the full path listed above.

### Non-fatal warnings
Unknown environment-config warnings, peer dependency warnings, the boolean@3.2.0 npm warning, and the npm install -g yarn allow-scripts warning were not themselves build failures.

## Electron version history
An earlier local setup explicitly used Electron 40.9.3. Current live repository state is Electron ^41.10.3. Treat the current repository as the source of truth and do not force Electron 40.9.3 unless investigating a historical issue.

## Runtime and API/catalogue investigation
After the native build, Hydra launched successfully.

A separate problem appeared: no download available for games. This was treated as a catalogue/API/download-source issue, not as evidence that the native build was broken.

MAIN_VITE_API_URL was found in:
- src/main/constants.ts
- src/main/services/game-executables.ts
- src/main/services/hydra-api.ts
- src/main/vite-env.d.ts

An earlier generated output contained:
const isStaging = undefined.includes("staging");
This indicated MAIN_VITE_API_URL was undefined in that build and could break API functionality.

A previous configuration used:
https://hydra-api-us-east-1.losbroxas.org

Important: re-verify this endpoint against current source/config before treating it as the current official endpoint. Do not invent or randomly add download-source URLs.

## Download sources
Separate these concepts:
1. Hydra application source
2. Hydra API/catalogue services
3. Community download sources
4. Torrent/content providers

A download-source problem is not automatically a Hydra build problem. Community sources require their own trust assessment. Do not blindly add unknown URLs, scripts, or binaries.

## Firewall decision
Windows Firewall prompted for torrent_bridge_test.exe. It was a locally built native test executable and its test had already passed. User clicked Cancel. Public-network permission was not necessary merely to complete that local test.

For Hydra itself, do not automatically allow Public network access. Evaluate Private/Public access based on the actual feature that needs networking.

## Security review context
User wants a serious security assessment of Hydra, not a blanket safe/unsafe answer.

Assess separately:
- source transparency
- official repository/release integrity
- build reproducibility
- dependency and supply-chain risk
- Rust/native code
- Electron/Node dependencies
- updater/update infrastructure
- API/catalogue services
- download sources/content providers
- network permissions
- current GitHub issues/security advisories

Previous review found the official repository public and active, and the GitHub Security page showed no published security advisories at that time.

A May 2026 GitHub issue reported an alleged update-infrastructure compromise involving a fake v3.10.x update. Treat this as a reported claim unless independently verified; do not present the allegation as an established fact without supporting evidence.

## Release context checked previously
Latest release checked: v4.1.4, released 2026-09-17.

Release notes included:
- similar-game recommendations
- compressed RetroArch ROM support
- Steam Library indicators/filters
- Steam playtime synchronization improvements
- Steam import/reconnect fixes
- achievement notification fixes
- French translation
- executable catalogue retry
- vcpkg/Rust native dependency caching in CI

Re-check GitHub for current release information when needed.

## Source-of-truth priority
For current technical decisions use this order:
1. Current package.json/source/configuration
2. Current lockfile
3. Current official README/docs
4. Current GitHub issues/PRs
5. This memory lane
6. Older chat logs

If this memory conflicts with the current repository, current repository evidence normally wins and this file should be updated.

## Do not repeat unnecessarily
Do not automatically:
- reinstall Node.js
- reinstall Yarn
- reinstall Rust
- reinstall VS2022 Build Tools
- reinstall the entire repository
- reinstall Python
- switch back to Python/libtorrent
- force Electron 40.9.3
- install the full Visual Studio IDE when Build Tools are sufficient
- allow Public firewall access without a reason
- add random community download sources
- treat warnings as failures

Inspect the current error/state first.

## Build vs runtime distinction
Confirmed build health:
- Rust works
- VS2022 C++ toolchain works
- CMake/vcpkg native build works
- hydra_torrent_bridge.dll built
- torrent_bridge_test.exe built
- ownership test passed
- hydra-native.node built

Runtime/API:
- Hydra launched
- download availability was a separate API/catalogue/source area
- MAIN_VITE_API_URL is important
- download-source trust must be evaluated separately

## Future additions
When the user says "add this to Hydra memory", update this document with:
- date
- problem/change
- evidence
- fix/decision
- current status
- whether it supersedes an older entry

Useful future entries include exact commands that worked, new errors/fixes, package versions, configuration changes, API endpoints, security findings, GitHub commits/PRs/issues, test results, runtime behavior, unresolved issues, and decisions that should be preserved.

## Continuation rule
If the user says "continue Hydra", start from this memory instead of asking them to repeat the entire setup history.

End of Hydra Master Memory Lane.
