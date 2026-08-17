# Publishing official Tranoo betas

This document is for maintainers. Testers should use [INSTALL.md](INSTALL.md) and [GitHub Releases](https://github.com/jng3134/tranoo-releases/releases).

The **private Android repository** builds, tests, and signs the app. This **public** repository only hosts GitHub Releases, checksums, and tester documentation.

```text
Private Android repository
        ↓
tests
        ↓
assembleRelease
        ↓
release signing
        ↓
rename APK to tranoo-beta.apk
        ↓
calculate SHA-256
        ↓
publish APK to this public repository's GitHub Release
```

## What this repository must never receive

Do not push, attach, or paste any of the following into `tranoo-releases`:

- Application source code
- Signing key material or keystore files (`.jks`, `.keystore`, `.p12`, `.pem`, `.key`)
- Signing passwords or aliases
- GitHub secrets, tokens, or GitHub App private keys
- Production `.env` files
- Backend credentials
- Firebase `google-services.json` or Supabase keys
- Build trees, Gradle caches, or unsigned intermediates committed to Git

APKs belong on **GitHub Releases**, not in Git.

## Release convention

| Field | Value |
| --- | --- |
| Git tag | `vMAJOR.MINOR.PATCH-beta.N` (example: `v1.0.0-beta.1`) |
| Release title | `Tranoo MAJOR.MINOR.PATCH Beta N` (example: `Tranoo 1.0.0 Beta 1`) |
| APK asset | `tranoo-beta.apk` |
| Checksum asset | `tranoo-beta.apk.sha256` |
| Release type | Public Beta |

Every release body should include:

```text
Version:
Build:
Release type: Public Beta
Minimum Android version: 7.0 (API 24)
SHA-256:
Known issues:
Changes:
```

Mark a build as a **pre-release** when you want it kept out of GitHub’s “latest” pointer. GitHub’s stable URL:

```text
https://github.com/jng3134/tranoo-releases/releases/latest/download/tranoo-beta.apk
```

points at the latest **non-prerelease**, non-draft release. To make that URL serve the current tester APK, publish that release **without** the Pre-release flag (the title and notes can still say Beta). Historical tags such as `v1.0.0-beta.1` remain on the Releases page.

## First release (manual)

From a trusted machine, using an APK signed with the official Tranoo release identity:

1. In the private Android repo, run tests, then `assembleRelease` with the official upload/release keystore.
2. Copy the signed APK to `tranoo-beta.apk`.
3. Generate a checksum:

   ```powershell
   Get-FileHash .\tranoo-beta.apk -Algorithm SHA256
   ```

   ```bash
   shasum -a 256 tranoo-beta.apk | tee tranoo-beta.apk.sha256
   ```

4. Create and push the distribution tag on **this** repository (not a source tag dump):

   ```bash
   git tag -a v1.0.0-beta.1 -m "Tranoo 1.0.0 Beta 1"
   git push origin v1.0.0-beta.1
   ```

5. GitHub → **Releases** → **Draft a new release**
   - Tag: `v1.0.0-beta.1`
   - Title: `Tranoo 1.0.0 Beta 1`
   - Attach `tranoo-beta.apk` and `tranoo-beta.apk.sha256`
   - Fill in Version, Build, SHA-256, known issues, and changes
6. Publish the release. The [validate-release](../.github/workflows/validate-release.yml) workflow should run, confirm the canonical APK name, and record the hash.

Or with GitHub CLI from this repository:

```bash
gh release create v1.0.0-beta.1 \
  tranoo-beta.apk \
  tranoo-beta.apk.sha256 \
  --title "Tranoo 1.0.0 Beta 1" \
  --notes-file notes.md
```

Add `--prerelease` only when you intentionally do **not** want `/releases/latest/download/tranoo-beta.apk` to point at this build.

## Future CI from the private repository

The preferred architecture is:

- Private repo Actions builds and signs the APK.
- A **narrowly scoped** GitHub App or fine-grained token, stored **only** in the private repository’s Actions secrets, publishes the release to `jng3134/tranoo-releases`.
- That credential should allow contents write (releases/tags) on **this** public repo only. It must not have access to the private source repo’s secrets, keystores, or broader org admin scopes.

Do not:

- Embed tokens in this public repository
- Reuse a personal access token with `repo` scope across many repositories if a GitHub App or fine-grained token can be limited to `tranoo-releases`
- Echo signing passwords, keystores, or tokens in workflow logs
- Check out private source into this public repo

This repository’s own workflow only **validates** published release assets. It does not build the Android app and must not be given signing secrets.
