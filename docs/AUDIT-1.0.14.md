# 🔎 Rano IDE 1.0.14 — standard Xcode product identity

## 🛠️ Generation fix

Version 1.0.13 collected compiler and SDK-source information but left the standard `DTXcode` and `DTXcodeBuild` product fields absent. That was insufficient to reproduce the development-product entries expected by App Store tooling. New managed Flutter, Swift package and supported experimental native/React Native builds now populate these entries **before signing**, using the matching verified import identity from the genuine Xcode archive's `Contents/version.plist`. The numeric Xcode version is derived from the recorded product version; no current stable build identifier is hardcoded or inferred from a filename.

Xcode's platform Info.plist supplies these fields through product-version macros. [Swift Build's core](https://github.com/swiftlang/swift-build/blob/main/Sources/SWBCore/Core.swift) reads a containing development product's `version.plist` in its Xcode developer-path mode, while its standalone Swift-toolchain mode uses an arbitrary testing product identity. [Its Info.plist processor](https://github.com/swiftlang/swift-build/blob/main/Sources/SWBTaskExecution/TaskActions/InfoPlistProcessorTaskAction.swift) merges platform entries and expands the macros. Our slim SDK retains the verified source product record rather than a full Xcode installation. The earlier omission is corrected in the shared bundle generator.

This product identity is distinct from the actual compiler and host. The real Linux Swift/Clang/LLD versions and checksums remain recorded separately. No macOS `BuildMachineOSBuild` is borrowed or invented, no Mach-O compiler versions are disguised, and vendor frameworks retain their own provenance. Existing IPAs are not relabelled. A missing or inconsistent source cannot receive guessed product values.

## 🪟 Local checks and UI test

**Check before upload** now checks the standard product fields in the app and every embedded extension. Missing fields, testing identities, source conflicts and a beta explicitly listed without App Store acceptance stop locally. The same guard runs again before the UI starts a transfer. External IPAs with their own valid standard entries do not need a Rano-specific record. Unknown or uncached release eligibility stays unconfirmed; it is not reported as acceptance.

Create a new archive with this version, choose **Export App Store IPA locally**, then inspect **Release IPAs → Export details…**. The organizer shows the Xcode SDK product alongside the genuine compiler summary. Use **Check before upload** to test without transferring the app. Signing, transfer and asset compilation implementations are retained; the new delivery change is a local tooling guard before the existing upload client.

## ✅ Evidence and limits

Regression coverage includes all managed product paths, app/extension consistency, derived version encoding, vendor preservation, absent and conflicting product fields, known beta refusal, accepted release candidates, stable build identifiers with lowercase suffixes, external IPAs, unchanged old artifacts and refusal before an Apple client is created. A real ARM64 iOS compiler/linker check verifies the generated standard fields against the installed SDK's verified source. Packaged UI and installer checks use isolated projects and fixtures; they do not send builds to Apple.

The [Godot issue for this exact App Review message](https://github.com/godotengine/godot/issues/74154) documents missing standard fields as one cause of a beta-Xcode classification. That supports this fix but does not reveal Apple's private classifier or establish acceptance of our user's particular build. The bundle-generation defect is fixed and locally verified. **Apple App Review acceptance of a new build still requires an Apple-side result.** TestFlight processing alone does not establish it. No owner project was rebuilt or uploaded during this verification, and older uploaded builds remain unchanged.

Current experimental native/React Native and clean-Windows-installation limitations remain as documented in the README. Public assets exclude desktop development source, owner projects, credentials and Apple SDK files.
