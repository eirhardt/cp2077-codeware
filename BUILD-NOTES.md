# Local 2.5 build

Fork of [psiberx/cp2077-codeware](https://github.com/psiberx/cp2077-codeware) (MIT).
Branch `fix-reflection-call-return` is [PR #65](https://github.com/psiberx/cp2077-codeware/pull/65).

| Branch | Contents |
|---|---|
| `main` | Upstream as of Oct 23, 2026 (1.20.6, no 2.5 support) |
| `pr63` | Community 2.5 port, [PR #63](https://github.com/psiberx/cp2077-codeware/pull/63) by KelpHect, at `6ef34ff0`. Not merged or reviewed upstream. |
| `local-build` | `pr63` plus one build fix (below). This is what's installed in the game. |

## Build fix

The prebuilt TiltedCore package references `mi_malloc_size`, which mimalloc 3.x removed,
so linking failed. `xmake.lua` pins mimalloc 2.x:

```lua
add_requireconfs("tiltedcore.mimalloc", {version = "2.x", override = true})
```

## Build

Visual Studio 2022 Build Tools (C++) and xmake. Clone to a short path (long SDK file
names exceed the Windows path limit) with `git -c core.longpaths=true clone --recursive`.

```powershell
xmake f -m release -y
xmake -y
pwsh -File tools\dist\package-mod.ps1 -ReleaseBin build\windows\x64\release\Codeware.dll
```

Output: `build\dist\Codeware-1.20.6.zip`, extract into the game folder.

Switch back to the official release once Codeware ships 2.5 support.

## Retired (Oct 31, 2026)

The official release with patch 2.5 support is installed now (Codeware 1.21.2). This branch is kept
for reference only.
