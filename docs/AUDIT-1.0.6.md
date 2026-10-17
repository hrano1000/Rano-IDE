# 🧰 Rano IDE 1.0.6 — Apple SDK releases and imports

## 📥 What changed

Environment → Apple SDK releases and Dependencies → Update iOS SDK open a shared, project-independent release manager. It reads Apple’s official release RSS and App Store Connect acceptance notes. It prefers the latest stable release explicitly named for App Store submissions, labels prereleases, and does not infer eligibility from the SDK version alone. Checks reuse a dated cache for one day; Check releases forces refresh. Offline users can import a downloaded archive.

Download from Apple opens the existing authenticated embedded browser with a release search. Apple sign-in and license acceptance remain interactive. The app never guesses XIP URLs, captures browser passwords, or persists signed download URLs. Completed downloads preserve their original filename in local download bookkeeping. Import downloaded Xcode selects an existing full .xip from disk.

## 🔎 Identity and recovery

A bounded streaming reader checks XAR/pbzx/CPIO structure and the complete compressed Content stream without executing archive contents. It reads the exact root Xcode Info.plist and the versioned iPhoneOS SDK metadata, ignoring unrelated plug-in build IDs. A selected release’s build ID must match the actual source. File renaming cannot disguise a Release Candidate as stable. This is structural/identity validation, not independent XIP signature verification; users must obtain genuine Apple downloads.

Import updates both installed Swift and Flutter SDKs, even if healthy versions already exist. A shared WSL import lock, replacement journal and previous-SDK backups protect the paired update. Both new installations must pass health checks and agree with the imported device SDK identity before commit. Failed updates restore old SDKs; retry or the installed-SDK check recovers interrupted replacement. Source Xcode and SDK build identities are recorded inside the local SDK roots. No beta identity is relabelled or invented. Compiler compatibility remains checked separately; future SDKs can require a reviewed compiler update.

## ✅ Evidence and limits

The real existing 2,027,369,056-byte Xcode archive was fully read. It declares Xcode27.1 RC build27A9274 and iPhoneOS27.1 SDK build24A94232. Apple’s live feed and acceptance notes list stable Xcode27.1 build27A9275. The importer rejects a mismatching selected build before moving installed SDKs. This finding identifies the downloaded candidate, not the exact historical IPA rejected by App Review or its sole rejection cause.

**660 tests passed; 27 environment-dependent/opt-in tests were skipped.** The affected SDK/setup/Flutter checks passed again after final source-change, lock-inheritance and UI-status hardening. Regression tests exercise exact release/channel matching, offline cache, invalid/truncated/corrupt archives, wrong-build refusal, replacing both healthy SDK roots, failure at either importer, and interrupted recovery. UI diagnostics use isolated fixtures, without SDK replacement or Apple delivery, to check light/dark/narrow presentation, help Escape/close, error and retry/success states. Existing frozen diagnostics, installer runtime and credential checks remain required release gates. Submission, signing, asset and archive implementations remain unchanged.

Live authenticated final Xcode download/import and an App Review resubmission are not proven by these checks. No Apple app upload was performed. No SDK is redistributed. The full clean Windows VM setup remains unverified. Native/React Native support remains experimental as detailed in [Compatibility](COMPATIBILITY.md).
