# opencode-binaries

Pre-built **OpenCode** CLI binaries, including a build that can run on a phone.

## Downloads (Releases)

| Asset | Platform | Version |
|---|---|---|
| `opencode-v2.0.18-win-x64.zip` | Windows 10/11 (x64) | v2.0.18 |
| `opencode-linux-arm64-v1.18.33.zip` | Linux ARM64 — phones (Android via Termux), Raspberry Pi 64-bit, etc. | v1.18.33 |

## Windows install

1. Download `opencode-v2.0.18-win-x64.zip` from [Releases](../../releases).
2. Extract `opencode.exe` anywhere (e.g. `C:\Tools\`).
3. Optionally add its folder to `PATH`, then run:

```powershell
opencode --version
```

No Node.js/npm required — the executable is self-contained.

## Phone install (Android via Termux)

> Android has no native OpenCode app. The ARM64 Linux build below runs on a
> phone inside **Termux** with a Debian/Ubuntu userland via `proot-distro`.
> (iPhones/iOS cannot run it — Apple's sandbox forbids terminals/executables.)

1. Install **Termux** from [F-Droid](https://f-droid.org/packages/com.termux/) (the Play Store build is outdated).
2. In Termux:

```bash
pkg install proot-distro wget
proot-distro install ubuntu
proot-distro login ubuntu
```

3. Inside the Ubuntu shell, fetch and extract the ARM64 build:

```bash
wget https://github.com/Brainshock246/opencode-binaries/releases/download/binaries-2026-09-28/opencode-linux-arm64-v1.18.33.zip
apt install unzip
unzip opencode-linux-arm64-v1.18.33.zip
chmod +x opencode
sudo mv opencode /usr/local/bin/
opencode --version
```

4. Run `opencode` and follow the login/setup prompts.

Notes:
- Works on any ARM64 Android phone (8 GB RAM recommended for comfortable AI sessions).
- The same binary also runs natively on Linux ARM64 servers (e.g. AWS Graviton).
- If you only have a glibc chroot, the `musl` static build was chosen for maximum portability.

## iOS

Not possible: iOS does not allow spawning terminals or downloading standalone executables outside the App Store.

## Provenance

- Windows zip: the `opencode.exe` from the official npm package `@opencode/cli` (v2.0.18), verified SHA-256 identical after zip round-trip.
- ARM64 zip: repackaged from the official upstream release [`sst/opencode v1.18.33`](https://github.com/sst/opencode/releases/tag/v1.18.33) asset `opencode-linux-arm64-musl.tar.gz` (ELF AArch64 verified).
- Both zips were opened and entry-checked after creation.
