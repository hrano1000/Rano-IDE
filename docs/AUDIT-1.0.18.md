# 🛠️ Rano IDE 1.0.18 — Development capability verification

The development clients previously treated every HTTP 409 conflict from capability enablement as success. A rejected request could therefore be reported as enabled, and the signer omitted capability entitlements absent from the resulting profile. The source declaration alone did not prove the installed app had the permission.

Both Apple-ID and API-key clients now accept a conflict as already enabled only after a read confirms the exact capability. Provisioning reads back all requested capabilities before reporting success or creating a profile. Unsupported, rejected or unconfirmed changes stop with the exact App ID and Apple Developer recovery steps. Capability mutations are not retried. Existing primary/grouped Apple sign-in configuration is not changed automatically.

Before development signing and installation, the main app, each declared extension and offline cached signing material must grant the source's known capability entitlements. Empty or missing grants stop Run. Profile-owned identifiers, push environment selection and qualified App Groups remain controlled by the profile. No unsupported entitlement is fabricated locally. The shared supported development signing path applies to projects using that path; this does not expand native/React Native execution support.

The existing App Store upload, distribution signer, archive, SDK and asset/resource compiler files are unchanged. The desktop source stays private. Independently licensed backend source and the exact patch are supplied separately.

## Verification

Isolated HTTP tests cover rejected and already-enabled capability conflicts for both providers and Apple sign-in/push. Provisioning tests check that unsupported or unconfirmed enablement produces no profile and no success message. Grant tests cover Apple sign-in, missing/empty grants, development push, qualified groups, extensions and permission-name-only errors. Existing backend identity, transport, offline, lifecycle and custom-command suites are retained.

Release evidence records the completed Python, compiled-backend, frozen-app, installer and exact-artifact credential checks. These checks do not establish successful sign-in on a physical iPhone. The owner must enable the rejected Apple capability once and rebuild/run online through the UI for that live test. No owner app was built or uploaded by the isolated release checks. Full clean-Windows toolchain setup remains unverified.
