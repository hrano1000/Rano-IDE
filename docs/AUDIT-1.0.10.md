# 🔎 Rano IDE 1.0.10 — SDK aliases and verified Xcode source

## 🛠️ Installation correction

A live SDK import in version 1.0.9 passed Xcode product verification and installed both SDKs, then failed its final uniqueness check. Each installer provided a versioned name such as `iPhoneOS27.1.sdk` and an unversioned name `iPhoneOS.sdk` for the same physical directory. Counting those names as separate SDKs incorrectly triggered rollback. The previous working SDKs were restored.

The importer now resolves SDK directory aliases and requires exactly one physical device SDK inside each installed bundle. Broken links, destinations outside the bundle, non-directory entries and multiple distinct SDKs remain errors and retain rollback. The installed SDK must still match the complete source archive before product provenance is recorded.

## ✅ Product identity and verification

This version includes the Xcode product identity correction. It reads `Contents/version.plist → ProductBuildVersion`, checks paired root app metadata and keeps compiler metadata separate. A genuine Xcode 27.1 / 27A9275 archive can contain compiler build 27A9274. Filenames and the selected release do not override the archive's actual product identity.

Regression coverage exercises both SDK replacements with aliases and verifies rollback for external, dangling and distinct targets. A read-only check against the real WSL installations confirms both alias layouts and restored SDK health. Automated regressions, frozen application checks, exact-artifact credential scans, installer/runtime checks and the actual UI import results are retained in private QA.

The established Apple submission, signing, archive and Flutter asset compiler implementations are unchanged. No Apple app upload is part of this SDK maintenance. Apple SDKs, owner projects and account credentials are excluded from release assets. Full clean-Windows-VM installation, universal native/React Native compilation and App Review acceptance are not established by these checks; see [Compatibility](COMPATIBILITY.md).
