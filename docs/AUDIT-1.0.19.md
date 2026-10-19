# 🛠️ Rano IDE 1.0.19 — Apple ID capability request format

The owner's custom Release build completed, but automatic provisioning failed with HTTP409: “The relationship 'capabilities' is required but was not provided with this request.” Version18 correctly stopped installation instead of concealing the rejected permission.

The public App Store Connect API and Apple-ID Developer Services share most request fields, but Developer Services also requires relationships.capability.data with type capabilities and the requested capability identifier. The backend previously sent the public-only body to both providers. The capability payload now includes that relationship only for Developer Services. Public API requests, existing capability settings and Apple sign-in grouping remain unchanged. Version18's capability readback, actual profile grant checks and no-mutation-retry behavior are retained.

Primary references: upstream xtool's [DeveloperServicesAddAppOperation](https://github.com/xtool-org/xtool/blob/main/Sources/XKit/DeveloperServices/App%20IDs/DeveloperServicesAddAppOperation.swift) and [DeveloperAPI schema patch](https://github.com/xtool-org/xtool/blob/main/Sources/DeveloperAPI/patch.js) distinguish the private relationship from the public schema. This is a protocol correction, not fabricated entitlements or SDK metadata.

## Verification and limits

An isolated HTTP endpoint reproduces Apple's exact reported failure for a missing relationship. Tests use the actual Developer Services client and verify its capability relationship, selected bundle resource and team for Apple sign-in, push notifications, associated domains and App Groups. Additional tests assert the public payload and actual API-key client retain their existing schema. Existing conflict, profile-grant, identity, transport, offline and custom-Run suites remain required.

Completed release checks and artifact hashes are retained with the local release evidence. These isolated checks make no live Apple capability mutation, do not configure an owner's primary/grouped App ID and do not establish successful physical iPhone sign-in. Rebuild/run through the new UI to verify the live account and phone. No Apple upload was performed. Full clean-Windows toolchain installation remains unverified.

The established Apple upload/distribution signer/archive/resource compiler implementation files are unchanged. The desktop GUI source stays private; independently licensed backend corresponding sources and exact patch are supplied separately.
