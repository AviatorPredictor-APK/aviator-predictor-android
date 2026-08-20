# Android installation


## Supported Android versions

The migrated application currently has an Android 5.1 / API 22 minimum-SDK baseline. That baseline and the final target SDK must be revalidated on real devices and emulators before release.

| Android/API | Release-test requirement |
|---|---|
| Android 5.1 / API 22 | Minimum-version install and launch test |
| API 28 | Legacy behavior and upgrade test |
| API 34 | Current-baseline behavior test |
| API 35–36 | Modern behavior and compatibility test |

The release notes, not this pre-release table, are authoritative for a specific APK.

## Before installation

1. Open the official repository and select a versioned entry under **Releases**.
2. Download the APK and `SHA256SUMS.txt` from the same release.
3. Verify the checksum, signing certificate, package name, and build provenance by following [VERIFY_APK.md](VERIFY_APK.md).
4. Read that release's permissions and known limitations.

Do not install a binary forwarded through a messenger, file mirror, shortened link, advertisement, or third-party “download” page.

## Install from a browser or file manager

On current Android versions:

1. Open the verified APK.
2. If Android blocks the installation, open the shown settings page.
3. Allow **Install unknown apps** only for the browser or file manager opening this APK.
4. Return to the installer and review the app name and requested access.
5. Complete installation.
6. Remove the temporary **Install unknown apps** permission if it is no longer needed.

Do not globally disable Google Play Protect or other device security controls.

## Install with ADB

After enabling USB debugging and connecting an authorized test device:

```bash
adb devices
adb install aviator-predictor-android-vX.Y.Z.apk
```

To update an existing compatible installation while retaining its local data:

```bash
adb install -r aviator-predictor-android-vX.Y.Z.apk
```

Android accepts an in-place update only when the package and signing identity are compatible. A signature mismatch is a reason to stop and investigate; do not work around it by uninstalling until you understand why the signer changed.

## Verify the installed version

The release notes must publish the package name and version. With ADB, inspect the installed package using:

```bash
adb shell dumpsys package club.aviatorpredictorapk.terminal
```

Check the reported `versionName`, `versionCode`, and package against the release notes.

## Uninstall

Use Android **Settings → Apps → Aviator Predictor Simulator → Uninstall**, or:

```bash
adb uninstall club.aviatorpredictorapk.terminal
```

The final privacy review must document whether Android backup could restore local settings after reinstalling.

## Troubleshooting

### “There was a problem parsing the package”

Confirm that the download completed, the SHA-256 value matches, and the release supports the device's Android version and CPU architecture.

### “App not installed”

Possible causes include insufficient storage, a corrupted download, incompatible Android version, or an installed build with the same package but a different signing certificate.

### Browser reports that the file may be harmful

Android warns about sideloaded APKs because they are installed outside a managed store. A warning is not a reason to skip verification. Check the release origin, checksum, certificate fingerprint, provenance, permissions, and source before deciding whether to install.

### The APK asks for unexpected permissions

Cancel installation and report the mismatch. The requested permissions must agree with the version-specific release notes and [PRIVACY_AND_NETWORK.md](PRIVACY_AND_NETWORK.md).

