# Security

## Reporting a vulnerability

**Do not report security vulnerabilities through public GitHub issues.**

Public issue trackers are visible to everyone. Do not post exploits, tokens, account details, personal documents, or steps that could harm other testers.

Use one of these private channels instead:

1. **GitHub Private vulnerability reporting** on this repository, if it is enabled  
   (`Security` → `Advisories` → `Report a vulnerability`)
2. **Private security contact (placeholder):** replace this with a dedicated address before inviting testers, for example `security@example.com`

If neither channel is configured yet, contact the repository owner privately through a non-public method. Do not open a public issue as a fallback.

Please include:

- The Tranoo beta version (GitHub Release tag or in-app version)
- A clear description of the issue and impact
- Steps to reproduce, if it is safe to share privately

We will not ask you to send signing keys, keystores, or production credentials.

## What this repository is allowed to contain

This repository is a **public distribution surface** for official Tranoo Android beta APKs. It must never contain:

- Signing keys, keystores, certificates, or passwords
- GitHub tokens, GitHub App private keys, or CI secrets
- API keys, backend credentials, or production `.env` files
- Firebase `google-services.json`, Supabase keys, or similar vendor secrets
- Android application source code

APK files belong on **GitHub Releases**, not in Git history.

## Release signing

APK releases published here must be signed by the **official Tranoo release signing identity**.

Testers should only install builds downloaded from this repository’s GitHub Releases page. A build signed with a different certificate will not update over an official installation and should be treated as untrusted.

If you receive an APK from any other website, chat message, or file-sharing link, do not install it. Verify the SHA-256 checksum against the value published with the official release. See [docs/VERIFY_DOWNLOAD.md](docs/VERIFY_DOWNLOAD.md).
