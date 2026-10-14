# Third-party notices

Rano IDE 1.0.0's optional native setup downloads and compiles Swift Build revision `89af69d6b4effc57993c35181b8726d292749b47` (Apache-2.0 with the Swift Runtime Library Exception, with the project's own license files retained), pinned dependencies, Node.js 22.23.3 (MIT and bundled dependency notices retained), and CocoaPods 1.16.2 (MIT and individual gem licenses retained). These tools live in the user's isolated WSL installation. Their binaries are not bundled in the Windows installer. Sources: https://github.com/swiftlang/swift-build, https://nodejs.org/ and https://github.com/CocoaPods/CocoaPods. The local Swift Build source contains a scoped LLVM libtool version-parser compatibility change. Native source modules and JavaScript dependencies remain the user's project's declared dependencies and licenses.

Rano IDE desktop application and branding: freeware distribution with private application source. Independently licensed helper/component notices remain applicable.

**xtool** is an independently installed backend: MIT, copyright 2024 Kabir Oberai. The GUI calls the installed executable; the desktop ZIP does not bundle xtool, Swift or an Apple SDK. The optional installer retrieves upstream releases. Upstream license: https://github.com/xtool-org/xtool/blob/1.21.0/LICENSE.md

**xcross 2.0.2** is an independently downloaded and invoked CLI, licensed AGPL-3.0. Its binary is not bundled in the desktop ZIP. The desktop includes an **AGPL-3.0 native-runner patch** and its complete license in `xtool_desktop/native`. Native builds compile a separate backend from pinned revision `09636a0b4e9f50ada556eefd4240fc942c6f42a5`; the corresponding source, patch and license remain in `~/.local/share/xtool-desktop/xcross-desktop-native`. Source/license: https://github.com/arxdeus/xcross/tree/v2.0.2. This patch retains its AGPL license separately from the Rano IDE desktop application.

**distribution_signer.dart** is a separately invoked AGPL-3.0 adapter for the pinned apple_developer_kit within xcross. Its source and license ship under `xtool_desktop/native`; setup retains source beside the compiled WSL helper. OpenSSL verifies certificate/profile/CMS signatures using pinned public Apple trust roots. No Apple key, profile or SDK is bundled.

**AssetKit** is separately retrieved at revision `e763558b55fcbb5a443b1d7b2c6f0972d8bd14f7` and compiled locally under MIT. Its source and licenses, including the vendored BSD-3-Clause Apple LZFSE implementation, stay in `~/.local/share/xtool-desktop/asset-compiler`. **swift-png 4.5.0** uses Apache-2.0; its SwiftPM source and notices remain alongside the local driver. The desktop includes its own MIT asset compiler driver and downloads no proprietary actool binary. Sources: https://github.com/xtool-org/AssetKit and https://github.com/tayloraswift/swift-png/tree/4.5.0.

The reviewed **open_filex 4.7.0** SwiftPM adapter preserves that installed plugin's Objective-C source and its upstream license in the separate build copy. Its package layout is adapted; its implementation is unchanged. The backend compiler uses a separately downloaded, checksum-pinned **Dart 3.13.5** SDK under Dart's BSD license. It does not replace the app's Flutter/Dart toolchain. Source/license: https://github.com/dart-lang/sdk/tree/3.13.5.

The reviewed **google_mobile_ads 5.3.1** adapter preserves the plugin's Apache-2.0 license, native channels and source in the separate build copy. It replaces the three checked XIB template loaders with generated UIKit layouts preserving the original views, constraints and outlets. Google Mobile Ads 11.13.0 and User Messaging Platform 2.7.0 are fetched independently using Google's official checksum-bearing Swift packages and SDK terms; proprietary Google SDK binaries are not bundled in this desktop. Source: https://github.com/googleads/googleads-mobile-flutter and https://github.com/googleads/swift-package-manager-google-mobile-ads.

The iOS AOT compiler installer builds **Dart** revision `98116461144f4429ab873f8497023a5ec3b08127` under its BSD license, with pinned upstream ICU, zlib, BoringSSL and GN dependencies. Their source and upstream license files remain in the managed Linux source checkout. The desktop contains the original MIT build adapter, not the resulting snapshot executable. Source: https://github.com/dart-lang/sdk/tree/98116461144f4429ab873f8497023a5ec3b08127.

The optional Flutter setup retrieves **Flutter 3.44.0** (BSD-3-Clause, https://github.com/flutter/flutter/blob/3.44.0/LICENSE), **uv 0.13.0** (MIT/Apache-2.0, https://github.com/astral-sh/uv/tree/0.13.0), **pymobiledevice3 11.27.2** (GPL-3.0, https://github.com/doronz88/pymobiledevice3), and Ubuntu LLVM/device packages under their upstream licenses. These tools remain separate installations, rather than bundled desktop components. xcross and uv archive checksums and Flutter's source revision are pinned.

**Apple Xcode and SDKs** are proprietary and excluded from this project and all release bundles. Each user must obtain access independently under Apple's terms: https://www.apple.com/legal/sla/docs/xcode.pdf. Those terms restrict use to Apple-branded hardware; publishing this binary does not license Windows SDK use or redistribution.

**PySide6 / Shiboken6 / Qt 6.10.3** are dynamically packaged under their applicable LGPLv3 / GPLv3 / commercial terms. This app uses Qt Core, GUI, Widgets, Network and WebEngine under LGPLv3; the libraries stay separate and replaceable in `_internal`. Qt WebEngine also includes Chromium and its third-party components under their respective licenses, including LGPLv2.1 components. Their attribution/license texts are included in `licenses/QtWebEngine-Chromium-notices.html`, collected from the official Qt 6.10.3 documentation. The release includes license texts and links to corresponding upstream source. Users may replace compatible Qt libraries and debug modifications to those libraries as allowed by the LGPL. The Rano IDE freeware notice does not limit those rights.

- PySide/Shiboken source: https://code.qt.io/cgit/pyside/pyside-setup.git/tag/?h=v6.10.3
- Qt source: https://download.qt.io/archive/qt/6.10/6.10.3/submodules/
- Qt licensing: https://doc.qt.io/qt-6/lgpl.html
- Qt WebEngine/Chromium licensing: https://doc.qt.io/qt-6.10/qtwebengine-licensing.html

**Appetize** is an optional externally hosted testing service, not a bundled emulator or an affiliation. Each developer supplies their own account under the provider's terms. This integration uses documented HTTPS APIs and the normal provider browser page; it does not bundle a proprietary Appetize SDK. API documentation: https://docs.appetize.io/rest-api

**Python 3** runtime: Python Software Foundation license, included in the release. Source: https://www.python.org/downloads/source/

**cryptography 50.0.1** supplies ES256 signing for Apple's App Store Connect API under Apache-2.0/BSD-3-Clause. Its bundled OpenSSL and Rust dependency notices are copied from the wheel's license directory. **cffi** uses the MIT license. These libraries are included in the desktop; private Apple keys are not. Source/license: https://github.com/pyca/cryptography/tree/50.0.1 and https://github.com/python-cffi/cffi.

The standalone Windows installer uses **Tcl/Tk** through Python's tkinter, under its permissive upstream license terms. Tk's license text is included. It extracts the Qt-based app into a normal directory with separate, replaceable libraries.

**PyInstaller** bootloader: GPLv2-or-later with an exception permitting distribution of generated bundles under the application's own license. License/exception: https://pyinstaller.org/en/stable/license.html

The Windows release builder copies distribution license texts into `licenses/`. Please report missing notices as a packaging defect.
