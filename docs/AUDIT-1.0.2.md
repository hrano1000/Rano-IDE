# 🔎 Rano IDE 1.0.2 audit

Audit date: **14 October 2026**. These fixes apply to the shared IDE workflows, without app names or bundle IDs hard-coded for the owner's projects.

## 🛠️ Confirmed problems corrected

| Area | Problem and resulting behavior |
| --- | --- |
| Build copies | Long Windows paths failed during traversal/copy. Staging now uses extended paths and streamed, atomic file replacement. A failed copy retains the previous complete file. Read-only cached files can be refreshed. |
| Monorepos | Generated/ignored output could consume the destination drive. Staging excludes generated caches and ignored directories outside the app, retains declared local Flutter/Swift packages and Xcode package references, and stops checkout discovery at user-profile boundaries. Windows projects work when Git is available only through WSL. |
| Recovery | Disk-space/access failures were too vague and incomplete copies were difficult to clean. Preparation now checks free space, reports the affected file and cause, supports cancellation and records cleanup ownership before copying. |
| Default commands | New projects use the default build; custom commands are optional and saved for that project. The Workbench exposes both choices. |
| Dependency updates | The new **Dependencies** menu checks updates, previews compatible changes in a separate copy and applies changes only after an explicit click. It backs up the correct workspace manifest/lockfile, including nested workspace roots, and invalidates a preview if source metadata changes. Package-manager versions must be exact official versions. |
| Beginner tooling | Dependency commands now find the Node installation created by Automatic setup. Readiness checks execute npm, npx and Corepack as well as Node, so missing runtime modules trigger repair. |
| Window lifetime | A window cannot close while its dependency worker is running. Device scanning must stop successfully before the window can be destroyed. |
| Installer upgrades | Existing Rano IDE desktop shortcuts follow the new version even when creating a new shortcut is unchecked. Unrelated shortcuts are preserved. Creation remains checked by default. |
| Help | Built-in Rano IDE documentation, project update guidance and official GitHub/support links replace upstream product links in the user-facing Help/About flow. Required third-party attribution remains available. |
| Packaged runtime | The release uses Python 3.13.16, OpenSSL 3.5.9 and PySide6/Qt 6.11.2. Build guards require the reviewed runtime and pinned direct dependency versions. The bundle records its runtime versions and includes matching source-access/license notices. No Apple SDK is bundled. |

## ✅ Verification completed

- **590 automated tests passed; 27 environment-dependent or opt-in tests were skipped.** The suite covers project/window isolation, staging, commands, setup, recovery, distribution diagnostics and existing workflows.
- The previously failing real Flutter monorepo staged in approximately **15 seconds**, excluding its ignored output. This verifies preparation, not a new Apple submission.
- An isolated npm project completed **Check → Preview → Apply** through the actual Qt interface using the managed Node path. Check/Preview left its source lockfile intact; Apply changed `is-odd` from 3.0.0 to compatible 3.0.1 and retained a verified backup.
- A native SwiftUI example compiled and archived through the Windows interface and WSL. Its archive had one matching symbol UUID and no missing dSYM UUIDs. This does not establish general native device execution or App Store acceptance.
- The installed WSL environment passed the real toolchain readiness/setup check. Installer shortcut behavior was exercised using Windows COM in isolated folders, without changing the owner's desktop.
- The eight protected Apple upload/signing/archive/Flutter asset implementation files match the pre-audit SHA-256 baseline. **No Apple upload was made during this audit.**
- Release packaging additionally requires frozen application smoke checks, isolated installer verification and a credential scan of the exact publication files. The release provides SHA-256 checksums for its downloadable assets.

## 🚧 Remaining limits

This audit is not proof that every possible error has been eliminated. A completely fresh Windows-to-WSL-to-SDK-to-device setup across a Windows restart remains unverified. Administrator permissions, virtualization policy, downloads, Apple account access and device trust can still affect setup.

Flutter's tested path is established, but not every plugin is supported. Native Xcode and React Native/Expo support remain experimental. General storyboard/XIB, Core Data, Metal, string catalog and App Intents compilation, native device Run and XCTest execution still have gaps. Other source frameworks do not yet have verified complete local adapters. See [the compatibility matrix](COMPATIBILITY.md).

The dependency updater supports Flutter, npm, pinned pnpm, Yarn Classic and Swift packages. Modern Yarn and native containers without a Swift package manifest require further update integration. Managed compiler upgrades remain reviewed IDE releases rather than arbitrary toolchain replacement.

The runtime versions and licensing/source access were checked against [Python's release information](https://www.python.org/downloads/release/python-31316/), [Qt's 6.11.2 sources](https://download.qt.io/archive/qt/6.11/6.11.2/submodules/) and [Qt WebEngine's license documentation](https://doc.qt.io/qt-6.11/qtwebengine-licensing.html). Advisory database checks are a snapshot, not a guarantee of security.
