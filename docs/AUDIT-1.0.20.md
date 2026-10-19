# 🛠️ Rano IDE 1.0.20 — First-time Apple sign-in configuration

Version19 corrected Developer Services capability relationships. The next live owner attempt passed that request validation and Apple then required an explicit Sign in with Apple configuration. The app compiled; installation correctly stopped on the rejected capability request.

First-time APPLE_ID_AUTH creation now supplies the APPLE_ID_AUTH_APP_CONSENT setting with the PRIMARY_APP_CONSENT option enabled. Both developer provisioning providers use the selected configuration; only Apple-ID requests include the private capability relationship. Existing enabled Apple sign-in is skipped and never reconfigured or regrouped. Other capability requests retain their previous fields. Progress and account help describe the first-time primary default.

Apple recommends a primary App ID for a new app or first-time enablement. To attach a new related app to an existing primary App ID, configure that grouping in Apple Developer before Run. Existing groupings are preserved. See [Apple's configuration guide](https://developer.apple.com/documentation/signinwithapple/configuring-your-environment-for-sign-in-with-apple), [CapabilitySetting](https://developer.apple.com/documentation/appstoreconnectapi/capabilitysetting) and [CapabilityOption](https://developer.apple.com/documentation/appstoreconnectapi/capabilityoption).

## Verification and limits

Real-client isolated HTTP checks require the complete selected consent option as well as the Developer Services relationship and team. The fixture rejects missing configuration with the exact reported409. Public developer API tests check primary consent without the private relationship; other capability bodies remain unchanged. Provisioning regression verifies an existing Apple sign-in capability generates no enable request or primary-configuration progress message. Existing readback, actual profile-grant, offline, App ID, custom command and lifecycle checks remain required.

Completed test/build/installer/privacy reports and exact artifact digests are retained with this local release. No live Apple account mutation, profile generation, physical-device installation, sign-in or App Store upload was performed by the agent's isolated checks. The owner must test a new online Run through the UI. Full clean-Windows toolchain installation remains unverified.

Established App Store transfer, distribution signer, archive and resource compiler implementation files remain unchanged. The GUI development source stays private; independently licensed backend corresponding sources and exact patch are provided separately.
