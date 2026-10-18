# 🔎 Rano IDE 1.0.13 — genuine build toolchain metadata

## 🛠️ What changed

New managed Flutter, Swift package and supported experimental native/React Native archives can retain a bounded build record containing the real Linux host, selected Swift/Clang/LLD versions and executable checksums, the SDK compiler specification, and the imported SDK's recorded Xcode product source. SDK identity is checked against the app and extension Mach-O platform/version before metadata is attached to a fresh build or archive copy, before distribution signing. Vendor frameworks retain their original metadata.

Flutter's original Swift Runner path records the invoked toolchain and binds that record to the compiled Runner checksum. Other paths identify the configured toolchain and explicitly label the evidence as configuration; arbitrary custom scripts and every third-party compiler invocation are not traced. Swiftly launchers are resolved using the selected compiler's own target report rather than mistaking the dispatcher for the compiler. Missing or inconsistent identities stop collection instead of receiving guessed values.

`DTCompiler` records the genuine compiler specification from SDKSettings. This specification is not a claim that the Linux compiler is Apple Clang. Actual tool families, versions and hashes are recorded separately in `RanoBuildMetadata`. Xcode product provenance comes from the imported archive's `Contents/version.plist` identity and is separate from the compiler that built Xcode.app itself. The archive-content checksum identifies the recorded import payload, not the complete outer XIP file.

Linux builds do not receive invented `DTXcode`, `DTXcodeBuild` or macOS `BuildMachineOSBuild` values. Existing IPAs and archives are not silently relabelled. An installed SDK without a verified source record is shown as unrecorded rather than assigned a downloaded release's identity.

## 🪟 Inspect before upload

Build a new archive, export an App Store IPA locally, then select it under **Release IPAs → Export details…**. This opens a read-only metadata report with a keyboard-accessible help drawer. The organizer also shows the available compiler summary. Exporting locally does not transfer the app to Apple. Old builds need a new archive to collect the new record.

## ✅ Verification and limits

Regression checks cover compiler identity and file checksums, Swift dispatcher resolution, changed Runner refusal, malformed identities, SDK-source mismatch, device/simulator separation, app/extension consistency, vendor preservation, archive/export retention, project isolation, and the details/help UI. An isolated real ARM64 iOS Swift compile and Clang/LLD link were exercised on Windows/WSL using the installed SDK. Packaged UI checks cover light/dark appearance, narrow layout, help keyboard behavior and closing without delivery.

The metadata collection gap is repaired. The cause of Apple's beta-Xcode App Review classification has **not** been confirmed. Apple acceptance of a newly built IPA is **not validated** by local metadata checks or TestFlight processing. This update does not promise that the earlier App Review error is resolved, and does not present SDK source provenance as proof that Xcode ran. Apple determines acceptance. Official release information remains available in [Apple Developer releases](https://developer.apple.com/news/releases/) and [App Store Connect release notes](https://developer.apple.com/help/app-store-connect/release-notes/).

Apple transfer/signing and Flutter asset compilation are unchanged. No owner application was rebuilt or uploaded during this verification. Existing WSL environments, SDKs and tool installations were retained. Experimental native/React Native compatibility and clean Windows installation limits documented in the README remain applicable. Desktop source, owner projects, signing credentials and Apple SDK files are excluded from public release assets.
