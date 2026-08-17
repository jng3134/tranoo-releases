# Tranoo Android beta releases

Tranoo is a real estate marketplace app for browsing, comparing, and transacting on property listings.

**This repository is only for public Android beta APK distribution.** It does not contain application source code. Source code is maintained in a private repository.

## Current beta status

| | |
| --- | --- |
| Status | **Public beta** |
| Platform | Android |
| Minimum Android version | **7.0** (API 24) |
| Distribution | GitHub Releases only |
| Store listing | Not a Google Play Store build |

Beta builds may include unfinished features, change behavior between versions, and contain bugs. Do not use a beta as your only copy of important data.

## Download

Install the current public beta from GitHub Releases. The canonical APK asset name is always:

```text
tranoo-beta.apk
```

**Download the current release:** [GitHub Releases](https://github.com/jng3134/tranoo-releases/releases)

Intended stable asset URL:

```text
https://github.com/jng3134/tranoo-releases/releases/latest/download/tranoo-beta.apk
```

That `/releases/latest/download/` link is provided by GitHub for the repository’s **latest non-prerelease** release. Testers can always use the [Releases](https://github.com/jng3134/tranoo-releases/releases) page if they want a specific tagged beta.

Do not download APKs from the repository file browser. Files in Git are not the distribution channel.

## Install

Android may ask you to allow installation from the browser or file manager (unknown sources). That is expected for a GitHub APK. Allow it only for the app that is installing Tranoo.

Full steps, update behavior, and troubleshooting: [docs/INSTALL.md](docs/INSTALL.md)

## Verify the download

Each release should publish a SHA-256 checksum for `tranoo-beta.apk`. Compare the hash of your file with the value on that release before installing.

```powershell
Get-FileHash .\tranoo-beta.apk -Algorithm SHA256
```

```bash
shasum -a 256 tranoo-beta.apk
```

Details: [docs/VERIFY_DOWNLOAD.md](docs/VERIFY_DOWNLOAD.md)

## Release naming

| Item | Convention | Example |
| --- | --- | --- |
| Git tag | `vMAJOR.MINOR.PATCH-beta.N` | `v1.0.0-beta.1` |
| Release title | `Tranoo MAJOR.MINOR.PATCH Beta N` | `Tranoo 1.0.0 Beta 1` |
| APK asset | `tranoo-beta.apk` | `tranoo-beta.apk` |
| Checksum asset | `tranoo-beta.apk.sha256` | `tranoo-beta.apk.sha256` |

Release notes should include:

```text
Version:
Build:
Release type: Public Beta
Minimum Android version: 7.0 (API 24)
SHA-256:
Known issues:
Changes:
```

Version history: [CHANGELOG.md](CHANGELOG.md)

## Report a beta bug

Use the [beta bug report](https://github.com/jng3134/tranoo-releases/issues/new?template=beta-bug-report.yml) form.

Please include the Tranoo version, Android version, device model, and steps to reproduce. Do not submit passwords, access tokens, personal documents, private conversations, or other sensitive information.

Security issues must **not** go in public issues. See [SECURITY.md](SECURITY.md).

## Source code

Android source code, signing keys, and production configuration stay in a private repository. This public repository exists so testers can download official beta APKs, read release notes, and verify checksums.

## Maintainer publishing

Official betas are built and signed in the private Android repository, then attached to a GitHub Release **here**. Never commit APKs, keystores, or secrets to this Git history.

Publishing flow and what must never be copied into this repository: [docs/PUBLISHING.md](docs/PUBLISHING.md)
