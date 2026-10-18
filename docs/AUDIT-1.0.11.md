# 🔎 Rano IDE 1.0.11 — installation drive and environment discovery

## 🗂️ Installation drive

Automatic setup includes **Drive for new installations**, showing available local fixed disks and their free space. The choice is remembered. A new dedicated WSL environment is installed on the selected drive; its Linux compilers, SDKs and caches live there. Existing distributions are reused at their registered locations, including environments moved using WSL. Selecting a drive never relocates or deletes an existing installation. Windows projects, saved archives, the application and its Windows download cache retain their existing locations.

Setup checks free space on the destination disk. Resuming a partially installed environment checks its registered location rather than a newly selected drive. SDK setup likewise checks the installed environment's disk.

## 🛠️ Discovery correction

A temporary WSL startup failure previously looked like missing tools. Discovery now makes one bounded retry for failed launches, timeouts or malformed probe results. If a registered environment still cannot be checked, setup reports that failure before creating another installation. A verified Linux user is retained with the detected environment.

When a Flutter compiler check fails, the workbench first searches for a verified existing environment. It saves and reuses that environment before offering installation. Recovery is bounded; a repeated compiler failure opens the normal repair flow. Cancelling setup releases the pending archive action instead of leaving its organizer busy.

## ✅ Scope and evidence

Regression tests cover startup recovery, failed-check refusal, selected-drive placement, registered-location disk checks, remembered selection, unavailable disks and workbench recovery/cancellation. Release verification and actual local environment/UI evidence are retained in private QA. A full clean-Windows-VM toolchain installation and arbitrary iOS project compatibility are not established by these checks.

Apple upload, distribution signing, archive and Flutter asset compiler implementations remain unchanged. No Apple app build or upload is part of this update. No SDKs, owner projects, account credentials or private desktop development source are published.
