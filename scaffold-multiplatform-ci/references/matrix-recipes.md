# Platform and Architecture Recipes

Use these as starting points, then verify current runner, toolchain, SDK, and native dependency support.

| Platform | Typical runner | Target examples | Common artifacts | Notes |
| --- | --- | --- | --- | --- |
| Windows | windows-latest | x86_64-pc-windows-msvc, aarch64-pc-windows-msvc | NSIS .exe, MSI | Install the required SDK. ARM64 may require a dedicated runner or cross-linker. |
| Linux | ubuntu-22.04 | x86_64-unknown-linux-gnu, aarch64-unknown-linux-gnu | DEB, RPM, AppImage, tarball | Native ARM builders or cross toolchains are often needed for GUI libraries. |
| macOS | macos-14, macos-13 | aarch64-apple-darwin, x86_64-apple-darwin | App, DMG, tar.gz | Match runner architecture to target when native frameworks or signing are involved. |
| Android | ubuntu-latest | aarch64-linux-android, x86_64-linux-android | APK, AAB | Use the project's Gradle/NDK toolchain and separate signing job inputs. |

## Matrix design

Start from every platform and architecture the application can reasonably support, then remove entries only for a documented source, dependency, SDK, licensing, runner, or toolchain blocker. Evaluate both x86_64 and ARM64 for Windows and Linux, and both Apple Silicon and x86_64 for macOS. A missing native runner changes the verification level; it does not by itself make a cross-buildable target disappear from CI.

Prefer explicit include entries when installation and packaging differ:

    strategy:
      fail-fast: false
      matrix:
        include:
          - platform: windows
            runner: windows-latest
            target: x86_64-pc-windows-msvc
            cache_key: windows-x86_64
            package: nsis
          - platform: linux
            runner: ubuntu-22.04
            target: x86_64-unknown-linux-gnu
            cache_key: linux-x86_64
            package: deb,appimage
          - platform: macos
            runner: macos-14
            target: aarch64-apple-darwin
            cache_key: macos-aarch64
            package: app,dmg

Use separate jobs instead when a platform needs substantially different prerequisites, signing, or packaging actions. A matrix must not hide missing secrets or unsupported cross-compilers.

## Target verification

For each entry:

1. Install the target with the toolchain action or package manager.
2. Build the exact package format used by users.
3. Inspect artifact filename, architecture metadata, and bundled native runtime.
4. Run a smoke test where the runner can execute the artifact.
5. Record unsupported targets and signing limitations in release notes.

When a runner cannot execute a cross-compiled artifact, require successful compilation, packaging, architecture inspection, and artifact classification in CI. Label native runtime verification as unavailable and keep that limitation visible in documentation.

For cross-compiling GUI/native applications, verify linker, SDK, framework, and system-extension requirements independently; a successful language compilation alone is insufficient.
