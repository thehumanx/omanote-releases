# omanote-releases

Desktop app releases for [omanote](https://omanote.iambishistha.com) — download installers for Windows, macOS, and Linux from the [latest release](https://github.com/thehumanx/omanote-releases/releases/latest).

| Platform | File to download |
| --- | --- |
| macOS (Apple Silicon & Intel) | `.dmg` |
| Windows | `.msi` or `-setup.exe` |
| Linux | `.deb`, `.rpm`, or `.AppImage` |

Once installed, the app keeps itself up to date — when a new version is out, it offers a one-click "Update & restart" inside the app.

## macOS: ""omanote" Not Opened" warning

The first time you open omanote, macOS may show **"Apple could not verify "omanote" is free of malware"** with only *Move to Trash* and *Done* buttons. This is normal for apps distributed outside the App Store without an Apple Developer subscription — the app is safe, macOS just hasn't seen a paid Apple signature.

To open it (you only need to do this once):

1. Click **Done** (not "Move to Trash").
2. Open **System Settings → Privacy & Security**.
3. Scroll down to the Security section — you'll see *""omanote" was blocked to protect your Mac."*
4. Click **Open Anyway**, then confirm with **Open Anyway** (it may ask for your password or Touch ID).

After that, omanote opens normally forever, including after updates.

<details>
<summary>Terminal alternative (advanced)</summary>

```sh
xattr -d com.apple.quarantine /Applications/omanote.app
```

This removes the quarantine flag from the downloaded app, which skips the warning entirely.
</details>

## Windows: SmartScreen warning

Windows may show **"Windows protected your PC"** when running the installer. Click **More info → Run anyway**. Same reason as on macOS: the installer isn't signed with a paid code-signing certificate.

## Linux

- **Debian/Ubuntu:** `sudo dpkg -i omanote_x.y.z_amd64.deb`
- **Fedora:** `sudo rpm -i omanote-x.y.z-1.x86_64.rpm`
- **AppImage:** `chmod +x omanote_x.y.z_amd64.AppImage` and run it.

### AppImage shows a blank window / "Could not create default EGL display"

The v0.22.0 AppImage bundles an older `libwayland-client` that conflicts
with newer Mesa drivers (seen on Arch with Intel Arc graphics). Launch it
with the system library instead:

```sh
LD_PRELOAD=/usr/lib/libwayland-client.so ./omanote_0.22.0_amd64.AppImage
```

Fixed in releases after v0.22.0 (the AppImage no longer bundles libwayland).
