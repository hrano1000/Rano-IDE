# 🎯 Rano IDE 1.0.15 — Workbench application targets

## Visible selection

**Application target** now appears above **Build command** in Workbench rather than being hidden in native-only Project settings or shown as a disabled toolbar box. Its bundle identifier appears underneath for the current build configuration. **Refresh** rereads the project metadata. Native iOS/React Native selections are saved separately per project, using the application name and its project/workspace container. The selected target and container reach the existing build driver.

If a project contains several applications, it requires an explicit choice. A renamed or removed saved target is shown as unavailable; the IDE does not silently build another application. The choice is rechecked before compiling. Native custom commands that select a conflicting target, container or scheme stop with a diagnosis. Reopening a project defaults to Release; switching targets preserves a configuration when that target supports it.

## Scope and limits

Application choices come from application targets, not provisioning-profile names. Notification extensions, tests and libraries are excluded as main applications. Their normal parent-app dependency/signing behavior is unchanged. Bundle IDs are read from target-specific project settings and available configuration files; unresolved values remain unknown until build time.

Flutter shows the existing supported **Runner** application. Additional Flutter app targets are marked unavailable because this change does not implement arbitrary multi-target Flutter compilation or full flavor/scheme support. Swift packages show their configured application. Native and React Native build support remains experimental as documented in the README. Missing generated Pods do not hide an existing main target from the selector; actual dependency installation and compiler compatibility are still required.

## Automatic development provisioning

The desktop bridge enables the patched backend's automatic App ID policy. Explicit saved/one-run choices and IDs already registered to the team keep precedence. For a new app with neither original nor prefixed ID registered, the original project identifier is registered once without another prompt. A failure cannot silently replace that ID with a prefixed one. Existing prefixed choices are not silently migrated; this avoids orphaning installed app data and capabilities.

Apple's development service physically POSTs even logical GET requests. The patch distinguishes the logical operation and retries only GET lookups, up to three attempts, with short bounded delays, fresh headers, closed persistent connections, and a read timeout. Transient connection failures and HTTP 502/503/504 can recover. Authentication refusals, rate limits, malformed successful responses, registrations, certificates, profiles, capability changes and deletions are not automatically replayed. Existing offline-profile validation remains in place. If first-time provisioning cannot reach Apple and no usable cache exists, the UI explains the connection requirement and retains saved material. The patch does not change the App Store Connect transfer client.

## Verification

Focused regression coverage exercises extension exclusion, exact target/container restoration, project isolation, target-specific bundle IDs/configuration files, actual native build arguments, deleted targets, malformed metadata and conflicting custom commands. The packaged application check exercises selection, persistence, project switching, build argument routing, busy-state locking, light/dark/system rendering, narrow layout and contextual help without building or uploading an owner's app.

The development backend is rebuilt from its pinned source and its actual Dart transport/identity tests use mock Apple services; no live registrations or owner uploads are performed. The established App Store transfer, distribution signer, archive and Flutter asset compiler implementations remain unchanged. The genuine SDK-source metadata correction from 1.0.14 is retained. Local checks do not establish universal compiler support, permanent network availability or Apple's acceptance of every app. Complete first-time toolchain installation on a clean Windows VM remains unverified. Release assets exclude the desktop development source, owner projects, credentials and Apple SDKs.
