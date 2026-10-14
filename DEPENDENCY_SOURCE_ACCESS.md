# 📜 Third-party source access and library replacement

Rano IDE's desktop application source is private. Its free binary distribution
does not remove the source-access and modification rights of independently
licensed libraries and backend programs.

## Dynamically packaged Qt / PySide / Shiboken

The Windows installer extracts the application into a normal directory, with
separate DLLs and extension modules in `_internal`. The app uses unmodified
PySide6/Shiboken6/Qt 6.10.3 runtime libraries under their applicable LGPL
licenses. They are dynamically loaded; compatible replacement libraries are
not blocked by application signature/hash checks at runtime.

The complete corresponding upstream source for these libraries, including the
upstream build files, is available free of charge at these exact-version
locations, separately from the Rano IDE application source:

- **Qt 6.10.3 source modules:**
  https://download.qt.io/archive/qt/6.10/6.10.3/submodules/
- **Qt WebEngine 6.10.3 including its third-party source tree:**
  https://download.qt.io/archive/qt/6.10/6.10.3/submodules/qtwebengine-everywhere-src-6.10.3.tar.xz
- **PySide6 / Shiboken6 6.10.3 source and build files:**
  https://download.qt.io/official_releases/QtForPython/pyside6/PySide6-6.10.3-src/
- **Exact PySide source tag:**
  https://code.qt.io/cgit/pyside/pyside-setup.git/tag/?h=v6.10.3

Qt's module archives include the corresponding module source, license and build
files. WebEngine includes Chromium and its third-party dependencies; obtain
that complete archive rather than substituting only Qt's wrapper code.
Source-download directions are provided beside the binary release in this
document. See `licenses/` and THIRD_PARTY_NOTICES.md for the included license
texts and component attribution.

### Replace or debug compatible libraries

1. Keep a backup of the installation and close its running application.
2. Obtain/build the desired compatible **Windows x64** Qt/PySide/Shiboken
   libraries using the matching Python/runtime ABI and upstream build guidance.
3. Replace the relevant DLLs, extension modules and dependent resources in the
   extracted `_internal` installation tree. Preserve compatible directory names
   and dependencies; these are not interchangeable with Linux or 32-bit builds.
4. Launch the installed `RanoIDE.exe` directly to run the modified libraries.
   Re-running the installer may replace your local modifications with the
   official release, so keep your own copy separately.

You may modify, replace, re-link and reverse engineer/debug as necessary to
exercise the rights granted for these libraries by their licenses. The Rano IDE
freeware notice does not restrict those rights. Support for an unofficial
library build depends on its compatibility; the upstream build instructions
and LGPL text define the library rights.

Qt's own explanation is available at
https://www.qt.io/development/open-source-lgpl-obligations .

## Independently installed build tools

Rano IDE invokes separate local CLI programs rather than bundling their Linux
executable binaries into the Windows application. Setup obtains the pinned
sources/releases and retains applicable licenses and source checkouts locally.
Relevant sources include:

- xtool 1.21.0, MIT: https://github.com/xtool-org/xtool/tree/1.21.0
- xcross pinned revision `09636a0b4e9f50ada556eefd4240fc942c6f42a5`, AGPL-3.0:
  https://github.com/arxdeus/xcross/tree/09636a0b4e9f50ada556eefd4240fc942c6f42a5
- Flutter 3.44.0, BSD: https://github.com/flutter/flutter/tree/3.44.0
- Swift Build pinned revision `89af69d6b4effc57993c35181b8726d292749b47`:
  https://github.com/swiftlang/swift-build/tree/89af69d6b4effc57993c35181b8726d292749b47
- Node.js 22.23.3: https://nodejs.org/dist/v22.23.3/
- CocoaPods 1.16.2: https://github.com/CocoaPods/CocoaPods/tree/1.16.2
- AssetKit: https://github.com/xtool-org/AssetKit/tree/e763558b55fcbb5a443b1d7b2c6f0972d8bd14f7
- Dart SDK: https://github.com/dart-lang/sdk
- pymobiledevice3: https://github.com/doronz88/pymobiledevice3

The independently licensed **AGPL xcross patch and offline signing adapter**
ship with their source/license in the runtime bundle. A separate
`RanoIDE-1.0.0-backend-sources.zip` release asset provides the corresponding
pinned xcross source, patch, adapter, AGPL license and reproduction directions.
This dependency source asset does **not** publish Rano IDE's desktop GUI source.
The patched backend's source is also retained beside its local WSL executable
under `~/.local/share/xtool-desktop/xcross-desktop-native/source`.

Other dependencies fetched during setup retain their own license files and
source directories. Project-specific libraries are selected by the user's own
project and are not generally bundled in the Rano IDE installer. Apple SDKs
and proprietary project SDKs are excluded from this source distribution.

## Other packaged runtimes

Python, cryptography/OpenSSL/Rust dependencies, cffi, Tcl/Tk and the PyInstaller
bootloader retain their respective licenses/exceptions. Their attribution and
source directions are in THIRD_PARTY_NOTICES.md and the packaged `licenses/`
directory. The PyInstaller bootloader exception permits an application's own
distribution license; it does not remove third-party library obligations.
