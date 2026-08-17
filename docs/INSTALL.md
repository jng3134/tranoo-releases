# Install Tranoo (Android beta)

These steps install the official public beta APK from GitHub Releases. This is **not** a Google Play Store install.

## Before you start

- You need a device or emulator running **Android 7.0 (API 24)** or later.
- Download only from this repository’s [GitHub Releases](https://github.com/jng3134/tranoo-releases/releases) page.
- Prefer the canonical asset name: `tranoo-beta.apk`.

## Install

1. Open the [Releases](https://github.com/jng3134/tranoo-releases/releases) page and download `tranoo-beta.apk` from the current beta.
2. Open the downloaded file from your browser’s download list or from Files / Downloads.
3. If Android asks for permission to install from that browser or file manager, allow it **only for that app**, then continue. You do not need to change system-wide unknown-source settings for every app.
4. Confirm **Install**.
5. When installation finishes, tap **Open**, or find **Tranoo** in your app drawer.
6. Later betas can be installed **over** an existing Tranoo install when they use the same application ID (`com.tranoo.app`) and the **same official signing certificate**. You should not need to uninstall first for an official update.

Optional: verify the file hash before installing. See [VERIFY_DOWNLOAD.md](VERIFY_DOWNLOAD.md).

## Updating to a newer beta

1. Download the new `tranoo-beta.apk` from GitHub Releases.
2. Open the file and install it.
3. Android should update the existing Tranoo app in place.

If Android reports that the app is not compatible with an existing installation, see [Signature mismatch](#signature-mismatch) below. Do not mix unofficial or debug-signed builds with official betas.

## Troubleshooting

### Android blocks installation from unknown apps

Android may say the browser or Files app is not allowed to install unknown apps.

- Open the prompt and allow installs **from that one source**.
- Return to the APK and try again.
- Do **not** turn off Play Protect globally. If Play Protect shows a warning, confirm that you downloaded `tranoo-beta.apk` from this official Releases page, then choose the option that lets you keep using an app you trust from this source.

### "App not installed"

Common causes:

- A different Tranoo build is already installed and was signed with another key.
- The download was incomplete or corrupted.
- The device is below Android 7.0.
- The device is low on storage.

Try verifying the checksum, freeing space, and confirming your Android version. If a conflicting install is present, see the next two sections.

### Existing incompatible installation

If you previously installed Tranoo from another channel (Play internal test, a debug build, or a different computer’s local APK), Android may refuse the official beta.

- Uninstall the existing Tranoo app, then install `tranoo-beta.apk` from this Releases page.
- Uninstalling removes that app’s local data on the device.

Only do this when you know the installed copy is not the official beta, or when Android explicitly reports a conflict.

### Signature mismatch

Android will not update an app if the new APK is signed with a different certificate.

Symptoms include “App not installed”, “package appears to be invalid”, or an install conflict after downloading an official beta on top of a local/debug build.

- Uninstall the incompatible copy, then install the official `tranoo-beta.apk`.
- After that, only install later files from this Releases page so updates can continue in place.

### Corrupted download

If the installer fails immediately, or the file size looks far smaller than the release notes suggest:

1. Delete the downloaded file.
2. Download `tranoo-beta.apk` again from GitHub Releases.
3. Compare its SHA-256 hash with the published checksum. See [VERIFY_DOWNLOAD.md](VERIFY_DOWNLOAD.md).

If the hash does not match, do not install the file.

### Unsupported Android version

Tranoo public betas require **Android 7.0** or later. The installer or Play-like system dialogs may refuse the package on older devices. Use a device or emulator that meets the minimum version.

### Still stuck

Open a [beta bug report](https://github.com/jng3134/tranoo-releases/issues/new?template=beta-bug-report.yml). Include the Tranoo version, Android version, and device model. Do not attach passwords, tokens, or personal documents.
