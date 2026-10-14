# 🔐 Privacy and safe problem reporting

Rano IDE builds supported projects locally through WSL. The public repository
contains the release installer, documentation, branding and dependency notices;
it does not publish the desktop application's development source or the
maintainer's projects, accounts, signing material or local build history.

## Stored information

- Project settings, recent paths, build commands and artifact/receipt history
  are stored locally. Build commands may contain whatever you enter; avoid
  storing secrets in scripts that you intend to share.
- App Store Connect API keys, distribution private keys and the optional
  Appetize API key use Windows current-user DPAPI protection. This protection
  is tied to the Windows user and is not a portable backup format.
- Development signing sessions are maintained by the independent build
  tools in the selected local WSL environment.
- Project copies, archives, generated IPAs and logs may contain private
  source, configuration or application data. Protect them independently.

## External connections

Downloads contact the tool/package providers. Apple operations contact Apple.
Selecting Upload explicitly sends the compiled IPA to Apple's upload service.
Optional Appetize operations use the user's provider account. Rano IDE does
not require a build server or credential service operated by the maintainer.

Uncertain uploads are not automatically repeated. A saved receipt or a
completed transfer is not proof of App Review approval.

## Reporting a problem

Open a GitHub issue with the release version, framework/tool versions, failing
stage and a reviewed, sanitized error excerpt or screenshot. Log sanitization
reduces accidental disclosure but is not a guarantee that every secret is
removed. Review the material before posting it publicly.

Never upload passwords, verification codes, API tokens, `.p8` files, `.p12`/`.pfx`
backups, private-key PEM files, provisioning profiles, protected account stores,
full project/configuration directories or unreviewed logs to an issue.

For a security concern, first request a private reporting contact in an issue
without including exploitable details or credentials. Do not publish a
vulnerability report containing another person's private information.

Third-party library modification/source-access rights remain as documented in
DEPENDENCY_SOURCE_ACCESS.md and their licenses.
