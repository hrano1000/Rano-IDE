# 🔎 Rano IDE 1.0.5 — automatic release symbols

## 🛠️ Root cause and correction

A release IPA compiled successfully, but creating its archive failed with “A dSYM does not match the archived binaries.” The failure was reproduced using the real project's compiled IPA and genuine matching dSYMs. Windows' ordinary path enumeration silently returned no DWARF files for deeply nested symbol folders. The same folders were readable through extended Windows paths and their UUIDs matched the IPA.

Archive creation now uses extended paths when enumerating and reading dSYMs. It verifies the copied symbol UUIDs again before saving the archive. A genuine mismatch identifies the offending dSYM by name.

## 📦 Automatic collection

The shared collector reads the binaries inside the exact selected IPA, or the selected `.app` itself. An adjacent `.app` is no longer used as a substitute for the IPA. This applies to the supported Flutter, SwiftPM, native and React Native archive workflows; no application name or bundle ID is hard-coded.

Every DWARF file in a candidate bundle must have matching UUIDs and genuine debug information. Matching symbols are copied into a managed cache and rechecked after copying. The archive therefore does not depend on mutable shared SDK/compiler cache files. Symbol folder names include their UUID so targets with the same original dSYM name do not collide. A damaged managed copy can be recovered from valid source symbols.

Where the compiler retained recoverable debugging data, LLVM generates missing dSYMs from the exact binary. The build output reports matched symbols and names binaries whose debug information is unavailable. The IDE does not fabricate symbol files for stripped third-party binaries. A failed collection stops archive creation and retains its diagnostic output.

These changes affect local symbol collection and archive checks. The Apple upload protocol, signing, SDK/distribution metadata and asset compiler are unchanged. No Apple upload is part of this verification or desktop update.

## ✅ Verification

**643 automated tests passed; 27 environment-dependent/opt-in tests were skipped.** Regression coverage includes long Windows paths, stale adjacent apps, mutable caches, multiple targets, duplicate dSYM names, symbols replaced during copying, stripped/mixed DWARF bundles, damaged managed copies, unsafe IPA paths and collector failures. A packaged diagnostic runs the real Qt archive worker with synthetic deeply nested main-app and extension symbols.

The actual Qt Workbench **Archive open project** action rebuilt the reported application and saved its archive. All **6 binary UUIDs** had matching genuine symbols, including the notification extension, plugin library and Flutter frameworks. Original project inputs were unchanged and **zero Apple requests** were made. Replaying the previous frozen archive implementation with those genuine symbols reproduced the original failure; the corrected archive flow accepted them.

## 🚧 Scope

Correct symbol matching does not guarantee runtime behavior or Apple acceptance of an application. Third-party binary symbols can only be included when genuine matching debug information is available. Native/React Native compiler and clean-machine setup limits remain in [the compatibility report](COMPATIBILITY.md).
