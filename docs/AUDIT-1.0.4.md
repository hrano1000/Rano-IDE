# 🧩 Rano IDE 1.0.4 — automatic Flutter native preparation

Verified **17 October 2026**. The fix belongs to the shared IDE build pipeline and applies to every project using the supported native releases. No application name or bundle ID is hard-coded.

## 🛠️ What changed

The previous build stopped after `pub get` and sent users to Project Settings for five native packages. Builds now prepare those packages automatically in the separate managed workspace:

| Package | Verified native release |
| --- | --- |
| `disk_space_plus` | 0.2.6 |
| `flutter_inappwebview_ios` | 1.1.2 |
| `flutter_local_notifications` | 18.0.1 |
| `flutter_secure_storage` | 9.2.4 |
| `video_thumbnail` | 0.5.6 |

Preparation checks the published source fingerprint, preserves the actual implementation and license, and creates a SwiftPM layout. Registration-only Objective-C bridges become equivalent Swift registration classes. The webview sources receive the explicit imports previously supplied by CocoaPods; its verified empty navigation storyboard becomes an instance of the same navigation-controller class. Its existing programmatic browser UI remains intact. Video thumbnails retain PNG/JPEG and the real WebP encoder dependency. Privacy resources are copied into the built app.

OrderedSet is pinned to 6.0.3. The WebP adapter supports the verified 1.3.2 and 1.6.0 selections, preserving a matching existing lock selection. Unsupported native dependency locks stop explicitly instead of silently changing the SDK version.

Empty directories declared as Flutter assets are preserved during staging, including `assets/animations/` and `assets/icons/` folders. The previous file-only copy omitted them and caused Flutter asset bundling to fail. The fix applies to standalone projects and nested checkouts while respecting generated/ignored directory exclusions. Unused empty folders are skipped. YAML aliases, flow lists, quoted paths and flavored asset declarations are read by the safe YAML parser. Directories absent from the source are not invented. Explicit before-build generators can still create their assets. If assets are genuinely missing, restore them or remove the unused declaration in pubspec.yaml.

Notification extensions now receive the same native SDK module maps and qualified public-header import paths as Runner. The compiler previously passed only Swift module paths, so an extension importing an Objective-C SDK such as FirebaseMessaging failed despite the SDK already being compiled. This shared correction retains the original extension code.

Project Settings displays **Automatic on build** for reviewed sources. Manual package replacement remains under **Advanced native package overrides**. Unknown or modified native releases produce a named package/reason report; the old generic instruction to fill in Project Settings is removed. The Help guide explains the automatic flow and update options.

## ✅ Verification

- **619 automated tests passed; 27 environment-dependent/opt-in tests skipped.** Focused regression checks cover source preservation, unknown/modified packages, repeat preparation, locked native dependencies, bundled helper transport and beginner-facing failure handling.
- Official package archive checksums were verified against pub.dev metadata. The installed native contents match those archives after line-ending normalization.
- All five actual plugins compiled together in an isolated **iOS ARM64 Release** application on Windows/WSL. Both default native dependency selection and a second build preserving libwebp **1.3.2** compiled successfully.
- The compiled plugin library contains all five native registration classes and the real WebP encoder. Four original privacy resource bundles are present in the resulting app. Original Pub package source fingerprints and app version/build were retained.
- The actual Qt Workbench **Build project** action completed a release IPA build using all five plugins. Its Project Settings view showed automatic preparation for every package. No manual native package selection was made.
- Empty-directory regressions cover standalone/nested projects, repeat builds, exclusions and actionable permission failures. The reported real project was restaged with both empty source asset folders retained.
- All eight protected Apple upload, signing, archive and Flutter asset compiler files match their pre-change SHA-256 baseline. **No Apple request or upload was performed for this work.**

The release process also requires frozen application checks, isolated installer verification, an exact-file credential scan and public download size/SHA-256 verification before completion. Downloadable assets include SHA-256 checksums.

## 🚧 Scope

This is source-verified support for the releases above, alongside existing adapters and upstream SwiftPM packages. It is not a universal CocoaPods converter and does not automatically port arbitrary macOS build tools, storyboards or unknown plugin versions. Packages are never silently dropped or upgraded to make a build pass.

Compilation and packaging do not prove these plugins' runtime behavior on a device or Apple acceptance of every project. No new device runtime test was performed. Native Xcode/React Native support and complete clean-machine toolchain setup retain the limits in the [compatibility report](COMPATIBILITY.md).
