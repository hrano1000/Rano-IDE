# 🎯 Rano IDE 1.0.16 — Exact device Run App ID

## Cause and correction

Workbench displayed the original project bundle ID while Flutter development signing could choose an older registered or saved prefixed identity. The target selector chose Runner correctly but did not choose original versus prefixed development identity.

The new Run App ID selector defaults to the exact project bundle ID. Users can explicitly select the team-prefixed development app. The mode is stored per project and captured before workspace preparation. It travels in the launch protocol as a validated, narrowly scoped field; the bridge sets the backend override only for that operation. It does not modify original project files, global environment variables, other project windows, App Store metadata or distribution signing. Build and Archive do not receive the device override.

The development resolver honors the explicit original choice over saved or registered prefixed identities. Refusal to register the original stops instead of falling back. Offline Run also restricts profile lookup to the exact chosen identity; certificate, expiry, device and entitlement checks remain in place. Existing install/launch code uses the resolved signed ID for the parent app and its extensions. Switching IDs keeps the other installed app and its separate data.

## Verification

Verification evidence is recorded alongside the release. Tests cover project/window isolation, settings-editor preservation, launch propagation, stale original/prefixed choices, online refusal and offline cache mismatch. A real Linux PTY test checks the child process's selected override without contacting Apple. The existing packaged checks include Run App ID visibility, persistence, propagation, themes and narrow layouts.

No owner app was built, installed or uploaded during these checks. Native/React Native device Run remains unavailable; their build/archive compatibility limits are unchanged. Live provisioning and device launch are left for the user's UI test.
