# 🔎 Windows build and setup audit — Rano IDE 1.0.4

Rano IDE can build supported iOS projects locally on Windows through WSL, without executing macOS. **It is not a universal replacement for every Xcode compiler, resource tool, simulator or test runner.** Framework detection, package installation, archive creation and Apple upload are different capabilities.

## 📋 Current support

| Workflow | Current evidence and boundary |
| --- | --- |
| Flutter | Pinned Flutter 3.44.0, matching Linux-host iOS ARM64 AOT compiler, supported native plugins, Debug/Release builds and connected-device Run. The owner has confirmed successful TestFlight processing, app launch and icon display for tested builds. This does not verify every third-party plugin. |
| SwiftPM iOS application | xtool-compatible applications use the Linux Swift compiler and imported Apple SDK. Device signing/install/run uses the existing xtool account and device workflow. A generic library Package.swift is not automatically an installable iOS app. |
| Native Swift / Objective-C / C++ | Experimental Xcode project/workspace import, native compilation, package resolution, configurations and archives. A SwiftUI example with a local Swift package was compiled and archived through the Windows UI. General native device Run and XCTest execution remain unimplemented. |
| React Native / Expo | Experimental Node/package-manager installation, native generation, CocoaPods/codegen and native release bundling. React Native 0.87.1 compiled with a separate QA programmatic launch configuration. The stock launch storyboard remains a blocker. Device execution and Apple acceptance of this path are unverified. |
| Unity, .NET MAUI, Kotlin/Compose and other source frameworks | No verified end-to-end local adapter. An exported native project may have additional compiler/generation requirements. An existing compatible App Store IPA can be inspected and delivered irrespective of its original source framework. |

## 🧩 Automatic native preparation and asset staging in 1.0.4

The shared Flutter build flow automatically prepares verified releases of `disk_space_plus` 0.2.6, `flutter_inappwebview_ios` 1.1.2, `flutter_local_notifications` 18.0.1, `flutter_secure_storage` 9.2.4 and `video_thumbnail` 0.5.6. No project-specific adapter list or manual settings change is needed. Upstream SwiftPM packages and existing reviewed adapters remain supported.

All five actual implementations compiled together for iOS ARM64 Release using Windows/WSL. The resulting library contains their native registration classes and the real WebP encoder; four privacy resource bundles were retained. OrderedSet 6.0.3 and libwebp 1.6.0 resolved as exact package dependencies; a second release build also compiled with the preserved libwebp 1.3.2 lock selection. This verifies compilation and packaging, not these plugins' device behavior or Apple acceptance.

Source fingerprints are checked against the official published package contents. Changed/unknown source releases remain explicit support gaps. Unsupported lock selections stop with a native dependency diagnosis; the IDE does not silently pick another version. The webview adapter replaces its verified empty navigation storyboard with the same native navigation-controller class; its browser UI was already built programmatically by the plugin. This is a specific reviewed conversion, not a general storyboard compiler.

Empty folders explicitly declared as Flutter asset directories are preserved; unused empty folders are skipped. Previously these folders disappeared from the build copy, causing Flutter to reject otherwise valid asset declarations. Missing directories in the original source are not manufactured.

See [the 1.0.4 verification report](AUDIT-1.0.4.md).

## 🛠️ What 1.0.2 fixes generally

- Extended Windows paths are used for copying, folder traversal and cleanup. Large file comparisons use bounded memory.
- Generated build/tool caches are excluded. For monorepos, ignored output outside the selected app is pruned while its local configuration and declared Flutter path packages are preserved. A home-directory dotfiles repository is not mistaken for the app's checkout.
- The formerly failing real Flutter workspace staged successfully in about 15 seconds. Its ignored output/release caches were excluded. This is staging evidence, not a new iOS build or Apple submission.
- Staging failures report the reason and affected file without dumping source/configuration contents. A free-space check avoids filling the drive, partial copies remain recognizable by Clean Build, and preparation can be cancelled.
- New projects keep the default build selected; custom commands remain optional and project-specific.
- **Dependencies** provides checks, compatible update previews and explicit Apply with manifest/lockfile backups. Flutter, npm, pinned pnpm/Yarn Classic and Swift package update actions are supported. Checks run in separate copies; a real npm update through the UI passed with the source lockfile retained during preview and the previous file verified in its backup.
- **Help** and **About** use Rano IDE documentation and official GitHub links. Required third-party notices are retained.
- The protected Apple upload, signing, archive and Flutter asset compiler files are unchanged.

For the deeper runtime, installer and workspace audit, see [AUDIT-1.0.2.md](AUDIT-1.0.2.md).

## 🧰 Previous 1.0.1 setup improvements

- The installer shows **Create a desktop shortcut**, checked by default, and honors the selected preference.
- **Check compatibility** is visible in the Workbench and Product menu. It reads project metadata, explains build/testing support and identifies referenced native resources that require unavailable compilers. It does not run scripts or upload anything.
- Automatic setup checks that essential tools actually run, instead of assuming an executable file is healthy because it exists.
- SDK checks follow the declared ARM64 device target and verify required headers, UIKit, Swift/Clang resources and the selected host Swift identity. Incomplete imports and an SDK tied to another Swift compiler lead back to the in-app SDK import step.
- Damaged cached Node installations are replaced only after a checksum-verified download and version check. A broken native engine stamp/executable triggers recompilation rather than being trusted or producing an unrecoverable JSON error. Incomplete native engine extraction can be downloaded again.
- CocoaPods setup is serialized and retries installation when its command fails version verification. Missing native prerequisites include the actual Darwin linker and archive tools in the repair step.
- Native dependency scripts can ask `xcrun` for the imported SDK's actual version and build identifier. No fictional Xcode host version is supplied.
- The existing Apple upload/signing/archive and Flutter asset compiler implementations were left unchanged.

## 📱 Testing without a Mac

Supported local device workflows require a real iPhone/iPad, trust, development permissions and the appropriate signing account. Windows/WSL does not run Apple's local iOS Simulator. Appetize is an optional external cloud simulator provider; it is not required for local compilation or App Store delivery and is not a local Windows simulator.

A successful build is not proof of launch, feature correctness, XCTest coverage or App Store acceptance. Test the resulting application on a device before publishing it. Existing TestFlight success for one workflow does not certify a different framework or plugin combination.

## 🚧 Remaining compiler work

General storyboard/XIB compilation, Core Data model compilation, Metal compilation, string catalogs, newer icon formats, some dependency/extension asset catalogs and App Intents metadata extraction still require implementation and real-device validation. The native build stops rather than silently dropping those inputs. Installing packages or changing a command cannot manufacture those missing tools.

The regular upstream workflows have different requirements: [Apple's Xcode system requirements](https://developer.apple.com/xcode/system-requirements) list supported macOS hosts; [React Native's standard setup](https://reactnative.dev/docs/set-up-your-environment) uses Xcode/CocoaPods for iOS; [Flutter's standard iOS deployment guide](https://docs.flutter.dev/deployment/ios) uses macOS/Xcode. Rano IDE's alternate compilers cover a tested subset of those operations.

[xtool](https://github.com/xtool-org/xtool) supplies cross-platform SwiftPM application tooling. [Swift Build](https://github.com/swiftlang/swift-build) supplies the open native build engine; it does not by itself provide all Apple's proprietary developer tools. [xcross](https://github.com/arxdeus/xcross) supplies the independently licensed Flutter pipeline; Rano IDE uses a pinned version and its distributed backend patch, rather than automatically replacing it with upstream main.

For other frameworks, see the owning vendors' requirements: [.NET MAUI deployment](https://learn.microsoft.com/en-us/dotnet/maui/deployment), [Unity's iOS build process](https://docs.unity.com/en-us/engine/6000.7/manual/platform-specific/iphone/ios-building-and-delivering/build-process), and [JetBrains' multiplatform tooling](https://blog.jetbrains.com/kotlin/2025/05/kotlin-multiplatform-tooling-now-in-intellij-idea-and-android-studio/). Recognizing their projects does not establish a Windows compiler port.

## 🪟 Installer evidence

The EXE includes the Windows application runtime; the in-app setup installs the supported development tooling. Users still handle Windows administrator/restart prompts, Apple login/license acceptance and device trust. Those steps are not bypassed.

The updated readiness check and cached compiler setup passed against the installed Windows/WSL environment. A real damaged Node runtime was repaired using the verified vendor download inside a disposable WSL test folder; the owner's runtime was retained. The EXE also installed its runtime and passed startup/setup UI checks inside a clean Windows Sandbox, with only the installer and an empty results folder mapped from the host. Automated tests and frozen application/isolated installer checks cover the reported repair cases and UI.

**A completely fresh Windows installation with the full WSL-to-SDK-to-device workflow is not yet verified.** Hyper-V management was denied to this session. An isolated folder or Windows Sandbox runtime check does not establish complete prerequisite installation across a Windows restart. Machine policy, hardware virtualization and network restrictions can still block setup and require administrator assistance.

## 🔐 Release updates

Verified updates are published as new versions in the public [Rano IDE GitHub releases](https://github.com/hrano1000/Rano-IDE/releases). The desktop development source remains private. Public files contain documentation, branding, Windows binaries and independently licensed third-party source/license material where required. Release artifacts are checked against locally saved credentials before publication, then GitHub asset sizes and SHA-256 digests are verified.
