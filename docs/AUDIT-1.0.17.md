# 🛠️ Rano IDE 1.0.17 — Custom commands for device Run

## Cause and correction

The desktop invoked the custom command adapter only for Build/Archive. Flutter device Run bypassed it, rebuilt defaults and omitted definitions supplied by the user's script. The selected development App ID was correct but the application could still lack its runtime configuration.

Run now saves and executes the same project-specific command. Bash expands variables and runs the entire script. An opt-in compiler receipt records the actual app, original bundle ID, selected project, mode, target and resolved Dart defines. Each attempt uses a new random token and private0600file. The script must finish successfully and compile exactly one app for the selected project. Failed attempts remain failures even when shell code suppresses their exit status. Missing/stale/multiple outputs and mismatched project or bundle identity stop before installation.

The backend's opt-in Run handoff reads and verifies that completed output, then uses the existing development signing/install/launch operation. It skips default options resolution and compilation. Debug hot reload receives the actual target and definitions; Release launches the compiled AOT app. Device/App ID choices remain scoped to the Workbench operation. Default Run does not use this receipt path. App Store transfer, archives, distribution signing, SDK metadata and protected asset/resource compiler files are unchanged.

Configuration values are private build artifacts. New status/error text does not display the command, receipt contents or definition values. Receipts are removed after the Run session, and interrupted receipts cannot be reused by another attempt. User-authored scripts can still print their own output and run with normal WSL permissions. This is not a security sandbox.

## Verification and limits

Tests use actual Bash with an isolated recording compiler to verify expansion, one-build handoff, selected device, mode override and failure paths. The compiled pinned backend's Dart checks verify private receipt parsing, exact artifact/identity, definition preservation and stale/malformed/missing output rejection. Python UI tests and packaged checks cover custom Run routing and the preserved original/prefixed App ID choice. Full release hashes, frozen checks, installer results and the exact credential scan are recorded with the release evidence.

No owner application was built, installed or uploaded by these checks. The user's physical-device UI test remains necessary to confirm their app's configured screens. Native/React Native device Run and custom cloud simulator Run remain unavailable; documented build/archive limits are unchanged. Swift package custom device Run also stops with an explicit diagnosis instead of silently ignoring the selected command; default Swift Run and custom Build remain available. The desktop GUI source remains private; the independently licensed backend patch and corresponding source are included separately.
