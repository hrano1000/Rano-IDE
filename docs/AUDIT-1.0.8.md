# 🔎 Rano IDE 1.0.8 — installed and latest SDK versions

## 🧭 SDK version status

Apple SDK releases now shows Current SDK (the installed iOS SDK version and build), its recorded Xcode source when available, Latest stable release (from Apple's catalog), and a distinct update status. The release selector is labelled Release to download or import. Changing that selection never changes the current-version display.

The same read-only status logic is used at startup and in SDK settings. Up to date requires both installed source records to agree with the latest stable Xcode version/build. A newer version, a different same-version build, mismatching SDK sources, missing tools, unknown provenance and unavailable checks have separate outcomes. Build identifiers are opaque and are not sorted to guess which same-version build is newer. Latest stable discovery is independent of the selector's recommendation of an App Store-listed release. New SDKs still need compatible compilers and Apple's eligibility rules.

Older installed SDKs without provenance retain their real readable iOS SDK version/build. The UI does not guess an Xcode build or claim they are current. Offline catalog matches say they match saved information and ask for a connected check. No SDK is installed by the status check.

## 🔄 Import refresh

After an import succeeds or fails, the UI reads the installed SDK files again. Completing archive inspection or choosing a release is not proof of installation. The import result remains visible while version status refreshes. A repeated final error is no longer appended twice. Version checks and imports cannot start simultaneously in the same dialog. The existing exact-build refusal and transactional rollback remain in place.

## ✅ Verification and limits

Regression tests cover the status states, current/latest separation, offline truthfulness, newer stable releases without confirmed store eligibility, selection isolation, refresh after import/rollback, duplicate-error suppression and simultaneous-operation exclusion. Isolated Qt diagnostics cover light/dark/narrow layouts, help and error/retry/success states. Fixture imports do not install an Apple SDK. Live SDK/catalog reading, final regression totals, packaged diagnostics, installer verification and credential audit are recorded in private release QA.

The established Apple submission, signing, archive and Flutter asset compiler implementation is unchanged. No app is uploaded and the owner's SDK is not replaced for this desktop update. A genuine stable Apple download and an explicit UI import are still required to change the owner's SDK source. Full clean-Windows-VM toolchain installation and universal native/React Native compilation remain unverified; see [Compatibility](COMPATIBILITY.md). The application source remains private; public distribution contains binaries, documentation and required dependency source/access material.
