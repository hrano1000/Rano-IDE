## 🧩 Automatic native plugin preparation

Flutter builds now prepare these verified legacy native releases automatically: `disk_space_plus` 0.2.6, `flutter_inappwebview_ios` 1.1.2, `flutter_local_notifications` 18.0.1, `flutter_secure_storage` 9.2.4 and `video_thumbnail` 0.5.6.

Choose **Build** or **Archive**. Supported packages show **Automatic on build**; no manual native package selection is needed. Real native code, privacy resources and reviewed locked dependencies are preserved. Unknown or modified releases identify the package and reason. Advanced overrides remain optional.

📂 Declared empty Flutter asset folders now survive build-copy preparation; unused empty folders are skipped, fixing the reported Flutter asset-directory failure generally for standalone projects and monorepos.

🔧 Notification extensions retain the native SDK import paths used by the main app, correcting missing SDK-module errors without replacing extension code.

✅ 619 tests passed, 27 skipped. All five plugins compiled together for iOS ARM64 Release, and an actual Workbench release IPA build passed. Ten frozen application checks, isolated installer verification and exact-file credential scans passed. The established Apple upload/signing/archive/asset implementation is unchanged; no Apple upload was performed.

📥 Download **RanoIDESetup-1.0.4.exe** for the installer. The portable Windows ZIP, separate logos, required independently licensed backend sources and **SHA256SUMS.txt** are also included. The desktop application source remains private.

📚 Read the README and `docs/AUDIT-1.0.4.md` for instructions and verified limits. These are reviewed plugin releases, not universal CocoaPods support. Device behavior and Apple acceptance of every plugin combination are not certified by these compilation checks.
