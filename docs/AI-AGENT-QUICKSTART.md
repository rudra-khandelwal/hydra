# Hydra AI Agent & Daily Quick Start

Last updated: 2026-10-31

Copy/paste command reference for continuing the Hydra Launcher source-build and runtime investigation with ChatGPT, OpenHands, Cline, VS Code, or a terminal. Read this before starting work.

## 1. Project locations — do not confuse them

- **Actual Hydra application checkout:** C:\Users\rudra\Downloads\hydra
- **Research, memory, and public live guide repository:** https://github.com/rudra-khandelwal/hydra
- **Official upstream application:** https://github.com/hydralauncher/hydra
- **Canonical project memory:** [Hydra-Memory/README.md](../Hydra-Memory/README.md)
- **Detailed current handoff:** [2026-10-29 handoff](../research/checkpoints/2026-10-29-hydra-chat-handoff.md)
- **Research agenda:** [AGENDA.md](../research/AGENDA.md)

The public GitHub repository is a research/documentation workspace, not the actual Hydra application checkout.

## 2. Open Hydra in VS Code

Run in PowerShell or CMD:

~~~powershell
code -r "C:\Users\rudra\Downloads\hydra"
~~~

If code is not recognized, open VS Code manually and choose File → Open Folder.

## 3. Start Hydra from the VS2022 x64 Developer Command Prompt

Open **x64 Native Tools Command Prompt for VS 2022** (or a VS2022 Developer Command Prompt configured for x64), then paste:

~~~bat
cd /d C:\Users\rudra\Downloads\hydra
set CMAKE_GENERATOR=Visual Studio 17 2022
set CMAKE_GENERATOR_PLATFORM=x64
set VCPKG_VISUAL_STUDIO_PATH=C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
set VCPKG_PLATFORM_TOOLSET=v143
yarn dev
~~~

This is the previously preserved development launch sequence. It is not a claim that the app was launched successfully during this documentation update.

## 4. Start Hydra from ordinary PowerShell

This opens a CMD session initialized by the VS2022 x64 developer environment and runs the same command sequence:

~~~powershell
$vsdev = "$env:ProgramFiles(x86)\Microsoft Visual Studio\2022\BuildTools\Common7\Tools\VsDevCmd.bat"
if (-not (Test-Path $vsdev)) { throw "VS2022 VsDevCmd.bat not found: $vsdev" }
$commands = 'cd /d C:\Users\rudra\Downloads\hydra && set CMAKE_GENERATOR=Visual Studio 17 2022 && set CMAKE_GENERATOR_PLATFORM=x64 && set VCPKG_VISUAL_STUDIO_PATH=C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools && set VCPKG_PLATFORM_TOOLSET=v143 && yarn dev'
Start-Process cmd.exe -ArgumentList '/k', "`"$vsdev`" -arch=x64 -host_arch=x64 && $commands"
~~~

## 5. Start Hydra from the VS Code integrated terminal

1. Open the Hydra folder using section 2.
2. Select Terminal → New Terminal.
3. Select Command Prompt as the terminal profile, or run the PowerShell command in section 4 from a PowerShell terminal.
4. Paste the section 3 command sequence into the initialized VS2022 x64 terminal.

Do not assume an ordinary terminal has the correct MSVC environment. The confirmed native-build configuration uses VS2022 Build Tools and v143; do not mix VS2026 into this build.

## 6. Docker / WSL readiness for OpenHands

Last reported machine check:
- WSL default version: 2; default distribution: docker-desktop.
- Docker CLI installed (reported version 29.7.2).
- docker info could not connect to npipe:////./pipe/dockerDesktopLinuxEngine. Docker Linux Engine was not reachable at that time. This does not establish its current state.

Start Docker Desktop from Windows Start, wait for Engine running, then verify:

~~~powershell
docker info
docker run --rm hello-world
~~~

If these succeed, the daemon is reachable and a test container can run. If they fail, troubleshoot Docker Desktop before installing/running OpenHands. Do not reset WSL, delete Docker data, or reinstall Docker as a first response.

### OpenHands session lifecycle

- Docker Desktop must be running whenever the OpenHands container needs to run.
- The OpenHands container must be started for a new working session unless configured to run persistently.
- Open the local Agent Canvas URL only after the container reports ready.
- Persistent application settings/conversation storage must use a persistent volume or host directory; do not rely on a disposable container filesystem.
- Configure the model provider and credentials once where supported; provider usage limits and costs still apply.
- GitHub authentication may need renewal if its session expires.

**Important validation status (2026-10-31):** OpenHands has not yet been successfully installed or launched on this machine in the current setup sequence. The earlier suggested image tag, container arguments, and http://localhost:8000/canvas address are proposed setup details, not machine-verified instructions. Confirm the current official OpenHands Windows/Docker quickstart and image tag before running a container. Do not treat them as validated merely because they appeared in an earlier chat.

## 7. One-click launcher — planned, not yet installed

After the first successful OpenHands launch, create a Windows .bat launcher that:
1. Starts Docker Desktop if it is not already running.
2. Waits for docker info to succeed (with a bounded timeout).
3. Starts the validated OpenHands container with persistent storage and only the Hydra project folder mounted.
4. Opens the verified local Agent Canvas URL.
5. Does not expose the service on the LAN or mount the whole user profile.

Do not create or use this launcher until the exact OpenHands image, container arguments, persistence path, and local URL have been verified against current official instructions.

## 8. Project purpose and immediate task

We are investigating the Windows source build and runtime behavior of Hydra Launcher. The immediate unresolved issue is that Hydra displayed **“No download available” for every game**.

Diagnose the layers separately:
1. Hydra application code and runtime.
2. API endpoint/configuration.
3. Catalogue response.
4. Download-source metadata/configuration.
5. Actual source availability and content delivery.

A successful native build does not prove API/catalogue correctness. A catalogue result does not prove a source is available. A successful download does not prove the downloaded artifact is safe.

## 9. Required agent workflow

Before any code edit:
1. Read Hydra master memory, the dated handoff, agenda, and relevant validation/change-control files.
2. Confirm the actual app checkout path.
3. Inspect branch, HEAD, and git status.
4. Inspect current code/configuration; do not rely on old chat snippets.
5. Present a short investigation plan before substantial changes.
6. Work on a separate branch; do not commit directly to main.
7. Run relevant tests and report exact commands/results.
8. Update diary, findings, validation, agenda, and handoff when evidence changes.
9. Never claim live verification or test success unless actually performed.

## 10. Download and security rules

Until the “No download available” issue is understood:
- Do not download or install any commercial game.
- Use only a legitimate free/open-source test artifact if/when a controlled download is approved.
- Default to download-only, not installation or execution.
- Record baseline and post-download process/network/filesystem observations, timestamps, file metadata, and SHA-256.
- Inspect file type, signature, antivirus results, and static indicators before considering execution.
- Treat execution as a separate explicit decision requiring an isolated disposable VM/Sandbox and monitoring plan.
- Do not run unknown installers or binaries on the daily-use Windows installation.
- Do not publish tokens, cookies, authorization headers, private data, raw sensitive logs, signed URLs, or downloaded game content.

## 11. Copy/paste first message for a new AI coding session

~~~text
Continue the Hydra Launcher engineering investigation. First read:
1. https://github.com/rudra-khandelwal/hydra/blob/main/Hydra-Memory/README.md
2. https://github.com/rudra-khandelwal/hydra/blob/main/research/checkpoints/2026-10-29-hydra-chat-handoff.md
3. https://github.com/rudra-khandelwal/hydra/blob/main/research/AGENDA.md
4. https://github.com/rudra-khandelwal/hydra/blob/main/docs/AI-AGENT-QUICKSTART.md

Actual application checkout:
C:\Users\rudra\Downloads\hydra

The GitHub repository rudra-khandelwal/hydra is the research/documentation workspace, not the application source.

First inspect the local checkout, branch, HEAD, git status, current configuration, and tests. Do not reinstall existing tools without evidence. The immediate issue is Hydra showing "No download available" for every game. Diagnose API configuration, catalogue response, source metadata, and source availability separately.

Do not download/install games or execute downloaded binaries. Do not invent API endpoints. Work on a separate branch, request approval before destructive operations or external downloads, protect credentials, run tests, and report only verified results. Update the GitHub research handoff with sanitized evidence.
~~~

## 12. Current setup status

| Item | Status |
|---|---|
| VS2022 native build environment | Previously confirmed working |
| Hydra development launch command | Preserved; rerun verification still required |
| WSL 2 | Present |
| Docker CLI | Present |
| Docker Linux Engine | Not reachable in last supplied check; retest required |
| OpenHands installation and launch | Not yet verified |
| One-click OpenHands launcher | Planned; not yet created |
| Hydra “No download available” diagnosis | Unresolved |
| Game download | Not performed as part of this setup |

---
Keep this document current. If a command changes, verify it on the actual machine and update this page and canonical project memory together.
