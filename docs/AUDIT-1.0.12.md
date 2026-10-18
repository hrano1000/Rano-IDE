# 🔎 Rano IDE 1.0.12 — WSL connection and environment identity

## 🛠️ General recovery

Rano IDE retains an app-owned foreground session in the selected WSL environment while open. Every build command sent through the PTY bridge and every provisioning command sent through the shared execution helpers verifies the Linux machine identity in the same invocation before starting its requested command. Healthy compiler discovery pins that identity to the Windows WSL registration GUID. Recreating a distribution produces a new registration; moving its disk preserves its existing identity. Bootstrap checks use the base Linux shell and do not depend on Python being installed first.

The app retries a failed session connection once before any requested job starts. It does not repeat a build, installation or delivery after an unknown outcome. Closing or reconnecting releases only its own stdin/session; it does not run WSL shutdown, terminate, unregister, delete or set-default operations.

A registered selected environment is checked without silently switching to another distribution. Failed probes retain tools and settings. Automatic setup stops on an unreadable registered environment instead of installing a replacement. An unreadable SDK is distinct from a confirmed missing SDK and opens WSL health rather than SDK installation.

## 🪟 Recovery through the UI

**Environment → WSL health…** and Automatic setup's **Check WSL health…** show the registered location, Windows WSL engine version and the result of compiler/SDK probes. **Reconnect and check** reopens only the app-owned connection. Environment changes are saved only after a successful health check. Maintenance is blocked during builds, deliveries or setup workers across project windows. Help opens on demand in a keyboard-accessible sidebar.

**Update WSL…** downloads the supported official Microsoft WSL 3.0.1 engine, checks its pinned SHA-256 and launches the existing narrow administrator helper. It does not reinstall Linux distributions, SDKs or compilers or downgrade newer WSL versions. Microsoft installation can interrupt Linux sessions or request a Windows restart; the user receives that warning before continuing. No restart is silently performed by Rano IDE.

## ✅ Evidence and limits

Focused regression coverage exercises changed-root refusal, retained sessions, failed probes, recreated registrations, corrupt identity records, argument/stdin preservation, UI recovery, update refusal for current/newer engines and worker lifetimes. Packaged verification includes failure/recovery, light/dark, narrow-layout and help-sidebar checks without installing software or contacting Apple.

Private local evidence includes repeated real WSL launches and idle/concurrent probes of two distinct environments, exact guarded-command argument/stdin checks and deliberate identity-mismatch refusal. These checks used the existing WSL 2.5.9 engine without restarting WSL or reinstalling tools. The earlier intermittent wrong-root condition did not recur during the baseline reproduction checks, so its upstream root cause is not established and the new engine has not been proven to cure that condition. Protection and recovery behavior are verified separately from that unresolved reproduction.

This update does not establish a full clean-Windows-VM toolchain installation, universal iOS project compatibility or immunity from Windows/WSL failures. The established Apple upload, distribution signing, archive and Flutter asset compiler implementations are unchanged. No Apple app build/upload, SDK archive, owner project, private credential or private desktop application source is part of this release.
