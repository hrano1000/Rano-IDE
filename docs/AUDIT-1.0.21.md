# 🛠️ Rano IDE 1.0.21 — Developer capability readback

The latest owner run built its custom Release application successfully, but the IDE incorrectly reported Apple sign-in and push as unconfirmed. A subsequent authenticated, read-only Developer Services request confirmed both were enabled on the exact project App ID. Apple's private response omitted `attributes.capabilityType` and capability relationship data. The old parser consequently returned an empty set.

The Apple-ID provisioning client now reads explicitly enabled capability resources from their exact App ID resource prefix. It also supports a supplied capability relationship and retains legacy public-shaped responses. Disabled entries are excluded. The resource-ID fallback rejects unscoped, malformed, unrelated App ID and wrong resource-type identifiers. API-key provisioning retains its public response schema. No project bundle ID or developer team is hardcoded into the implementation.

Existing capability creation relationships, first-time primary consent settings, conflict confirmation, actual provisioning-profile grant checks, cached-profile protections and custom-command handoff remain in place. Existing enabled Apple sign-in is not regrouped. This is a response-reading fix, not a replacement for checking the profile used to sign the app.

## Verification and limits

Regression coverage uses the anonymized structure observed from Apple's response and checks legacy responses, disabled and malformed entries, exact App ID isolation, pagination and conflict readback. The corrected parser is also checked against a fresh read-only request on the owner's exact App ID. Release verification records the backend executable version, automated regression results, frozen application checks, isolated installer checks and credential scan of the release artifacts.

The agent does not create or replace owner profiles, mutate Apple capabilities, install an owner app on a physical iPhone or upload it to Apple during these checks. The next online Run through the UI must obtain a profile with the required grants, install the app and verify actual sign-in. Full clean-Windows toolchain installation remains unverified. Build success, portal enablement, profile grants, device behavior and App Review are separate outcomes.

Established App Store transfer, distribution signer, archive and resource compiler implementations remain unchanged. The GUI development source stays private. Corresponding sources for the independently licensed backend and the exact patch are supplied separately.
