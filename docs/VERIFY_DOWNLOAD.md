# Verify a Tranoo APK download

Every official beta should publish a SHA-256 checksum for `tranoo-beta.apk`. Comparing hashes confirms the file you downloaded is complete and matches the release.

## 1. Download the APK

Download `tranoo-beta.apk` from [GitHub Releases](https://github.com/jng3134/tranoo-releases/releases).

If the release also includes `tranoo-beta.apk.sha256`, download that file too. It is a text file containing the expected hash.

## 2. Hash the APK on your computer

### Windows PowerShell

```powershell
Get-FileHash .\tranoo-beta.apk -Algorithm SHA256
```

The `Hash` value is the SHA-256 checksum.

### macOS / Linux

```bash
shasum -a 256 tranoo-beta.apk
```

On many Linux systems you can also use:

```bash
sha256sum tranoo-beta.apk
```

## 3. Compare with the published checksum

The hash must match the checksum published with the same GitHub Release. That value may appear in:

- The release notes (`SHA-256:`)
- The `tranoo-beta.apk.sha256` release asset
- The [Validate release](../.github/workflows/validate-release.yml) workflow summary for that release

Comparison is case-insensitive. Ignore spaces. The checksum file typically looks like:

```text
<64-character-hex>  tranoo-beta.apk
```

If the hashes **match**, the download is intact relative to the published beta.

If the hashes **do not match**, delete the APK and download it again from GitHub Releases. Do not install a file whose hash disagrees with the official release.

## 4. Optional: check the `.sha256` file directly

If you downloaded `tranoo-beta.apk.sha256` into the same folder as the APK:

```bash
sha256sum -c tranoo-beta.apk.sha256
```

On macOS (no `sha256sum -c` on some versions), hash the APK with `shasum -a 256` and compare the hex string by eye or with `diff`.

## What a checksum does not prove

A matching SHA-256 hash means your file matches the asset attached to that GitHub Release. It does not replace:

- Downloading only from this official repository
- Trusting the official Tranoo release signing identity

Never use a checksum posted in a chat, email, or third-party website instead of the value on the GitHub Release.
