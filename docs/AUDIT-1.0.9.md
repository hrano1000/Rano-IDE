# 🔎 Rano IDE 1.0.9 — correct Xcode product identity

## 🛠️ False SDK release mismatch

The SDK reader previously treated Xcode.app/Contents/Info.plist → DTXcodeBuild as the Xcode product release. That key records the tools used to build Xcode.app and can differ from its product build. This caused a genuine 27A9275 archive to be reported as 27A9274 and refused before installation. Downloading the same Apple archive again did not resolve the reader defect.

The reader now takes the product build from Xcode.app/Contents/version.plist → ProductBuildVersion and checks its version/revision against the same application's root Info.plist. Compiler metadata is retained separately for diagnostics. The SDK reader does not relabel an archive, alter its contents, infer a release from a filename or bypass an actual product-build mismatch. New source records identify the product-reader format; older compiler-based records require verification through a fresh import.

## 🔒 Import checks

The entire compressed archive is still read and checked before either installed SDK is moved. Missing or invalid product metadata, duplicate root or SDK records, metadata mixed across Xcode applications, differing app/product versions, incomplete payloads and mismatched selected product builds are refused. Nested plugin version records cannot override the root product identity. Swift and Flutter SDK replacement retains its transactional health/source checks and rollback.

## ✅ Verification and limits

Focused regression tests cover a stable product built with earlier compiler tools, genuine product mismatch despite matching compiler metadata, installed provenance, malformed/missing/duplicate/mixed root records and legacy record handling. The genuine downloaded archive was inspected read-only to compare its root metadata and then checked using the corrected reader. Automated regressions, packaged application checks, exact-artifact credential scan, installer/runtime checks and the local UI import results are recorded in private release QA.

The Apple submission, signing, archive and Flutter asset compiler implementations are unchanged. No Apple app upload is part of this SDK maintenance. Apple SDKs are not included in release assets; account credentials and owner projects remain private. Full clean-Windows-VM toolchain installation and universal native/React Native compilation remain unverified; see [Compatibility](COMPATIBILITY.md). XIP structure/identity validation does not independently establish Apple's archive signature or guarantee App Review acceptance.
