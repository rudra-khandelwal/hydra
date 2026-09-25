# Hydra Launcher — Complete Chat Continuation / AI Handoff

Prepared: 2026-09-25

This is a consolidated technical handoff for starting a new AI/ChatGPT conversation without losing the important history from the previous Hydra Launcher setup. It is a reconstructed continuation packet, not a verbatim export of every message.

## 1. Project and repository

User: Rudra.

Goal: build and run Hydra Launcher from source on Windows 11.

Official upstream repository:
https://github.com/hydralauncher/hydra

User GitHub fork:
https://github.com/rudra-khandelwal/hydra

Local project path:
C:\Users\rudra\Downloads\hydra

GitHub handoff branch created:
chat-handoff-2026-09-25

## 2. Instructions for the next AI

Read this document before giving setup instructions.

The difficult Windows native build has already been solved. Do not restart from zero unless a new log proves the environment is broken.

Use the user's latest terminal output as the source of truth.

Do not casually:
- delete all of node_modules
- reinstall Visual Studio
- switch toolchains
- downgrade/upgrade random dependencies
- edit generated out/main/index.js as a permanent fix
- install old Python/libtorrent dependencies
- disable Windows Defender

Keep fixes targeted and explain the exact cause of a new error.

## 3. Known environment

OS: Windows 11 x64.

Node.js previously installed:
Node 24.19.0

For a fresh reproducible setup, Node 22 LTS was recommended. Do not change Node just because this handoff says so; use the current version unless a new error shows a compatibility problem.

Yarn:
1.22.22

Rust:
rustc 1.98.1
cargo 1.98.1
target x86_64-pc-windows-msvc

Visual Studio:
VS2022 Build Tools 17.14.41
MSVC 14.44.35207
toolset v143

Windows SDK:
10.0.26100.0

CMake generator:
Visual Studio 17 2022

Electron:
40.9.3

Historic Hydra version context:
4.1.4

## 4. Why VS2022 is important

VS2026 Build Tools was also installed on the machine, but it caused problems because node-gyp/CMake/vcpkg selected VS2026 when VS2022 was required.

Problems seen included:
- node-gyp rejecting Visual Studio 18
- CMake trying to use Visual Studio 18 18
- unresolved __std_* linker symbols caused by mixing VS2026/MSVC 14.51-built libraries with the VS2022/MSVC 14.44 final build

The proven working native toolchain is VS2022 + v143.

Always use a VS2022 Developer Command Prompt for the native build.

## 5. Required VS2022 environment

Run:

~~~cmd
cd /d C:\Users\rudra\Downloads\hydra

set CMAKE_GENERATOR=Visual Studio 17 2022
set CMAKE_GENERATOR_PLATFORM=x64
set VCPKG_VISUAL_STUDIO_PATH=C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
set VCPKG_PLATFORM_TOOLSET=v143

where cl
msbuild -version
~~~

Expected compiler family:
MSVC 14.44 / Visual Studio 17 2022.

Do not mix VS2026 and VS2022 native dependency caches.

## 6. Old Python/libtorrent path

An old setup attempted:

~~~cmd
python -m pip install -r requirements.txt
~~~

The user had Python 3.14.6 and the old dependency list had no compatible libtorrent distribution.

Do not return to that old pip/libtorrent route for the current native torrent bridge.

Important caveat: the project still contains a separate build:python-rpc script, so Python can still matter during the full Windows production build. The failed pip/libtorrent route was not the correct solution for the native bridge.

## 7. Build scripts that matter

Relevant project scripts observed:

~~~text
build = npm run typecheck && electron-vite build
build:win = npm run build:native && npm run build:python-rpc && electron-vite build && electron-builder --win
build:unpack = npm run build && npm run build:python-rpc && electron-builder --dir
dev = electron-vite dev
start = electron-vite preview
build:native = node ./scripts/build-native-addon.cjs
build:python-rpc = python3 python_rpc/setup.py build || python python_rpc/setup.py build
~~~

For normal development use:
~~~cmd
yarn dev
~~~

Do not use yarn start as a substitute for development unless specifically testing preview mode.

## 8. Installation/build history

### Error: spawn cargo ENOENT

Cause: Rust/Cargo was not installed or not on PATH.

Fix: Rust stable MSVC was installed and verified with rustc --version and cargo --version.

### Error: node-gyp Visual Studio unsupported

Cause: node-gyp saw VS2026.

Fix: VS2022 Build Tools were installed and the build was moved to the VS2022 Developer Command Prompt.

### Error: CMake generator Visual Studio 18 18

Cause: VS2026 was selected by CMake.

Fix:

~~~cmd
set CMAKE_GENERATOR=Visual Studio 17 2022
set CMAKE_GENERATOR_PLATFORM=x64
set VCPKG_VISUAL_STUDIO_PATH=C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
set VCPKG_PLATFORM_TOOLSET=v143
~~~

### Error: unresolved __std_* linker symbols

Cause: mixed MSVC toolchains. vcpkg/native dependencies had been built with VS2026/MSVC 14.51 while Hydra's final project was using VS2022/MSVC 14.44.

Fix: force the entire native/vcpkg/CMake build to VS2022/v143.

## 9. Proven native-build success

With VS2022 consistently selected, vcpkg detected:

~~~text
C:/Program Files (x86)/Microsoft Visual Studio/2022/BuildTools/VC/Tools/MSVC/14.44.35207/bin/Hostx64/x64/cl.exe
~~~

CMake detected:
MSVC 19.44.35229.0

The following were successfully built:
- hydra_torrent_bridge.dll
- torrent_bridge_test.exe

The native test:
torrent_bridge_ownership

passed.

Final test result:
100% tests passed out of 1

The staging area contained:
- hydra_torrent_bridge.lib
- hydra_torrent_bridge.dll

This proves the native toolchain works on the machine.

## 10. Electron failure and repair

At one point Electron was broken/missing and postinstall reported:

Electron failed to install correctly, please delete node_modules/electron and try installing again

The user removed node_modules\electron.

A later run then produced:
Cannot find module 'electron'

For the known Hydra 4.1.4 environment, the working repair was:

~~~cmd
yarn add electron@40.9.3 --dev
~~~

This installed Electron 40.9.3 successfully.

When the command was first run from normal CMD, CMake fell back to VS2026 and tried to use Visual Studio 18. The command therefore needs to be run from the correctly configured VS2022 environment.

## 11. Successful yarn install

After using the VS2022 Developer Command Prompt with the environment above, yarn install completed successfully.

The run successfully handled:
- vcpkg dependency checks
- CMake configure/generate
- native build
- native test
- Electron native dependency rebuild
- classic-level rebuild
- ludusavi v0.29.0 win64 package
- Husky postinstall

Final result:
Done in 218.76s.

## 12. Electron startup crash

The first yarn dev run successfully built the Vite main and preload bundles and started the renderer dev server at:

http://localhost:5173/

Electron then crashed with:

TypeError: Cannot read properties of undefined (reading 'includes')

at approximately:
out/main/index.js:92:62

The generated file was inspected with:

~~~cmd
powershell -Command "$p='out/main/index.js'; $l=Get-Content $p; $l[85..98]"
~~~

It showed:

~~~js
const isStaging = undefined.includes("staging");
~~~

## 13. Exact root cause: missing MAIN_VITE_API_URL

Source search showed:

~~~text
src\main\constants.ts:7:export const isStaging = import.meta.env.MAIN_VITE_API_URL.includes("staging");
src\main\services\game-executables.ts:15: MAIN_VITE_API_URL used for catalogue/steam/executables
src\main\services\hydra-api.ts:190: baseURL: import.meta.env.MAIN_VITE_API_URL
src\main\vite-env.d.ts:4: readonly MAIN_VITE_API_URL: string
~~~

Therefore import.meta.env.MAIN_VITE_API_URL was undefined during Vite build.

The fix was to create a .env file containing the required API URL.

Known working value:

~~~text
MAIN_VITE_API_URL=https://hydra-api-us-east-1.losbroxas.org
~~~

Known command used:

~~~cmd
(
echo MAIN_VITE_API_URL=https://hydra-api-us-east-1.losbroxas.org
echo MAIN_VITE_AUTH_URL=
echo RENDERER_VITE_REAL_DEBRID_REFERRAL_ID=
echo RENDERER_VITE_TORBOX_REFERRAL_CODE=
echo MAIN_VITE_LAUNCHER_SUBDOMAIN=
) > .env
~~~

A later guide also included empty:
MAIN_VITE_WS_URL=
MAIN_VITE_NIMBUS_API_URL=

Do not edit out/main/index.js as the permanent fix. Fix .env/source configuration instead.

## 14. Successful development run

After setting .env, yarn dev worked.

Observed:
- Vite dev server at http://localhost:5173/
- Hydra API catalogue data returned
- Steam metadata/images loaded
- Work Wonders SDK initialized
- Electron launched
- DevTools opened, normal in development mode

Therefore the source build and development run were both proven working.

## 15. "No download available"

After Hydra launched, the user saw:
No download available

This is separate from the source compilation.

The important distinction is:
catalogue / metadata != configured download sources.

The catalogue can work while no download sources are configured.

A community source directory was discussed:
https://hydralinks.cloud/

This is a third-party site, not the official Hydra source repository. There is no confirmed record in this chat that the user installed a particular third-party source.

Do not interpret "No download available" as proof that the build failed.

## 16. Windows Firewall prompt

For the local development Electron/Vite process:
- Private: allow only if needed
- Public: do not allow
- Cancel/Block is acceptable if unsure

Do not expose the Vite development server publicly.

## 17. Production build

Once yarn dev is verified, stop it with Ctrl+C and run:

~~~cmd
yarn build:win
~~~

Remember that build:win also invokes build:python-rpc. If a future failure occurs inside python_rpc, diagnose that separate component rather than reinstalling old libtorrent packages.

## 18. Full reproducible setup

~~~cmd
cd /d C:\Users\%USERNAME%\Downloads
git clone https://github.com/hydralauncher/hydra.git
cd hydra
git fetch --tags
git checkout v4.1.4
~~~

Then from VS2022 Developer Command Prompt:

~~~cmd
cd /d C:\Users\%USERNAME%\Downloads\hydra

set CMAKE_GENERATOR=Visual Studio 17 2022
set CMAKE_GENERATOR_PLATFORM=x64
set VCPKG_VISUAL_STUDIO_PATH=C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
set VCPKG_PLATFORM_TOOLSET=v143

node --version
yarn --version
rustc --version
cargo --version
where cl

yarn install
~~~

Create .env:

~~~cmd
(
echo MAIN_VITE_API_URL=https://hydra-api-us-east-1.losbroxas.org
echo MAIN_VITE_AUTH_URL=
echo MAIN_VITE_WS_URL=
echo MAIN_VITE_NIMBUS_API_URL=
echo RENDERER_VITE_REAL_DEBRID_REFERRAL_ID=
echo RENDERER_VITE_TORBOX_REFERRAL_CODE=
echo MAIN_VITE_LAUNCHER_SUBDOMAIN=
) > .env
~~~

Run:

~~~cmd
yarn dev
~~~

Package after testing:

~~~cmd
Ctrl + C
yarn build:win
~~~

Version caveat: these exact versions/endpoints are historical troubleshooting context. For a future Hydra release, inspect its current package.json, env example, README and build scripts first.

## 19. Diagnostic bundle

When something genuinely fails, run this from the Hydra directory in the VS2022 Developer Command Prompt:

~~~cmd
echo ===== SYSTEM =====
ver
echo ===== NODE/YARN =====
node --version
npm --version
yarn --version
echo ===== RUST =====
rustc --version
cargo --version
rustup show
echo ===== MSVC =====
where cl
msbuild -version
echo ===== CMAKE =====
cmake --version
echo ===== ENVIRONMENT =====
echo CMAKE_GENERATOR=%CMAKE_GENERATOR%
echo CMAKE_GENERATOR_PLATFORM=%CMAKE_GENERATOR_PLATFORM%
echo VCPKG_VISUAL_STUDIO_PATH=%VCPKG_VISUAL_STUDIO_PATH%
echo VCPKG_PLATFORM_TOOLSET=%VCPKG_PLATFORM_TOOLSET%
echo ===== ELECTRON =====
if exist node_modules\electron\dist\electron.exe (echo Electron OK) else (echo Electron MISSING)
echo ===== HYDRA ENV =====
if exist .env (type .env) else (echo .env MISSING)
echo ===== PACKAGE =====
if exist package.json (findstr /N /I "\"version\"" package.json) else (echo package.json MISSING)
~~~

Before sharing it publicly, remove secrets, private URLs, tokens, referral codes, and credentials from .env.

## 20. Files from the previous chat

A self-contained HTML guide was generated locally:

/mnt/data/Hydra_Windows_Build_Guide.html

It contains:
- portable context
- AI handoff instructions
- architecture
- requirements
- tool installation
- source checkout
- VS2022 configuration
- dependency installation
- Electron repair
- env setup
- development run
- verification
- known failure history
- security notes
- diagnostic bundle
- production packaging
- version caveats
- copy buttons and clickable navigation

Relevant uploaded logs from the previous conversation existed and contained the exact successful native build and the undefined.includes crash investigation.

## 21. Final proven state

At the end of the previous troubleshooting:

YES:
- Hydra source installed
- Rust installed
- VS2022 Build Tools installed
- MSVC 14.44 / v143 working
- CMake using Visual Studio 17 2022
- vcpkg dependencies working
- hydra_torrent_bridge.dll built
- native test passed
- Electron 40.9.3 installed
- Electron native dependencies rebuilt
- yarn install completed
- Vite main/preload build completed
- yarn dev launched Hydra
- API/catalogue data loaded
- Steam metadata/images loaded
- missing MAIN_VITE_API_URL issue fixed

Separate unresolved/application-level matter:
- download sources were not configured, hence "No download available"

## 22. Resume message for a new AI

Use this exact intent:

"Use this document as the complete technical context. My Hydra native build and development run already work. Do not restart from zero. I will provide the newest terminal output if there is a new error."

Then, when continuing locally:

~~~cmd
cd /d C:\Users\rudra\Downloads\hydra

set CMAKE_GENERATOR=Visual Studio 17 2022
set CMAKE_GENERATOR_PLATFORM=x64
set VCPKG_VISUAL_STUDIO_PATH=C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
set VCPKG_PLATFORM_TOOLSET=v143

yarn dev
~~~

For production packaging:

~~~cmd
yarn build:win
~~~

## 23. One-screen summary

Machine: Windows 11 x64
Repo: rudra-khandelwal/hydra
Upstream: hydralauncher/hydra
Local path: C:\Users\rudra\Downloads\hydra
Historic Hydra version: 4.1.4
Node: 24.19.0 previously installed; Node 22 LTS recommended fresh
Yarn: 1.22.22
Rust: 1.98.1 MSVC
VS: VS2022 Build Tools 17.14.41
MSVC: 14.44.35207 / v143
CMake: Visual Studio 17 2022
Electron: 40.9.3
Critical env: MAIN_VITE_API_URL
Native build: proven working
Native test: 100% passed, 1/1
Development run: proven working
Major old issue: VS2026/VS2022 toolchain mixing
Old runtime issue: missing MAIN_VITE_API_URL
Separate application issue: No download available

End of handoff.

The main rule for continuation is: the difficult Windows native build has already been solved; troubleshoot the newest concrete error rather than rebuilding the whole environment.
