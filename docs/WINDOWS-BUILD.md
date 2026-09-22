# Windows Build Environment

## Validated environment

- Windows 11
- Node.js 24.19.0
- Yarn 1.22.22
- Rust 1.98.1
- Cargo 1.98.1
- Visual Studio 2022 Build Tools 17.14.41
- MSVC v143
- Windows SDK
- x86_64-pc-windows-msvc

## Native build environment

Use the VS2022 Developer Command Prompt and preserve the environment variables required by vcpkg/CMake:

```cmd
set VCPKG_KEEP_ENV_VARS=VSCMD_VER;VisualStudioVersion;VSINSTALLDIR;VCINSTALLDIR
set CMAKE_GENERATOR=Visual Studio 17 2022
set VCPKG_FORCE_SYSTEM_BINARIES=1
set VCPKG_VISUAL_STUDIO_PATH=C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools
set VCPKG_PLATFORM_TOOLSET=v143
set CMAKE_GENERATOR_PLATFORM=x64
```

## Install

```cmd
yarn install
```

## Development

```cmd
yarn dev
```

## Notes

The VS2026 Build Tools installation exists on the research machine, but the validated Hydra native build workflow deliberately uses VS2022 Build Tools to avoid mixing toolchains.
