# ConnMTP

[Tiếng Việt](docs/vi/README.md) · [About](docs/ABOUT.md) · [User Guide](docs/USER_GUIDE.md)

Browse and transfer files between a Mac and an Android phone, a camera or any other MTP device. No ADB or USB debugging needed.
Written in pure Swift: the PTP/MTP protocol is implemented directly on top of libusb, with no Go backend and no libmtp.

## Layout

```
Sources/
├── CLibUSB/          Module map for libusb (built by scripts/build-libusb.sh)
├── MTPKit/           Core library: USB transport, MTP protocol, browsing and transfers
└── ConnMTP/          SwiftUI app
    ├── App/          App entry point, menus, windows
    ├── Models/       TransferJob (state of one transfer)
    ├── Resources/    AppIcon.png (1024×1024; Dock icon for `swift run`, AppIcon.icns in the .app)
    ├── Services/     Worker (background queues), FileIcons
    ├── ViewModels/   BrowserModel (+Transfers: the transfer queue)
    └── Views/        Sidebar/, Browser/ (list, grid, menus), Switch/ (DBI), Sheets/,
                      Transfers/ (progress sheet, Transfers window), Common/
Tests/                Unit tests for MTPKit
scripts/              build-libusb.sh, build-app.sh
docs/vi/              Vietnamese README
```

| Product | Kind | Contents |
|---|---|---|
| `MTPKit` | library | `MTPDeviceManager`, `MTPDevice` (session), `MTPObject`, `MTPStorage`, recursive pull/push, safe cancellation |
| `ConnMTP` | executable | GUI app |

## Build

Building requires Xcode (or its Command Line Tools). Homebrew is not needed. The app runs on macOS 13+, on both Apple silicon and Intel Macs.

```bash
make deps         # build libusb once (universal, macOS 13+) into build/deps/libusb
make build        # debug build
make test         # unit tests
make app          # build/ConnMTP.app: universal (arm64 + x86_64), libusb and the app icon bundled inside
make run-app      # run the app directly (swift run ConnMTP)
```

`make deps` downloads the libusb 1.0.30 release (checksum-verified) and builds it for arm64 and x86_64 with a macOS 13 deployment target. `make build`, `make test`, `make run-app` and `make app` run it first when needed. If you build with plain `swift build` or from VS Code, run `make deps` once beforehand. libusb is LGPL-2.1: the app ships it as a separate dylib in `Contents/Frameworks`, with its licence in `Contents/Resources/libusb-COPYING`.

In VS Code, the **Launch ConnMTP.app (bundle)** configuration builds the app bundle with `scripts/build-app.sh` and starts it under the debugger. Use **Debug ConnMTP** to step through code, since the bundle is a release build.

> **Mixed toolchains.** If you have more than one Swift toolchain (for example Xcode's and one installed with swiftly), build with the same one everywhere. `.build/` is shared, so mixing them gives *"Module compiled with Swift X cannot be imported by the Swift Y compiler"*. To fix it, run `rm -rf .build` and build again.

## ConnMTP app

- The sidebar shows devices and their storages (with a usage bar). Devices are detected when plugged in or out, and connected automatically when there is only one.
- The file table sorts by name, date and size. It uses macOS file-type icons and has a breadcrumb path bar and a filter field.
- Two views: **List** (table) and **Icons** (grid, with photo/video thumbnails read from the device). Switch with the toolbar button or ⌘1 / ⌘2. The grid has a sort menu and an icon-size control, and the chosen view is remembered.
- Double-click opens a folder, or opens a file with its default app (after downloading it to a temporary folder).
- Drag files or folders from Finder into the app to upload them. Drag rows from the app to Finder to download them (files are downloaded only when dropped).
- ⌘C in Finder, then ⌘V in the app uploads into the open folder.
- ⌘C / ⌘X, then ⌘V between folders on the device copies / moves on the device itself (`CopyObject` / `MoveObject`). On a name clash the copy is named “… copy”. If the device can't copy by itself, the app downloads and uploads again.
- Download into a chosen folder or straight into Downloads.
- New folder, rename, delete (with confirmation), Copy Path.
- On a name clash the app asks Replace / Skip.
- **Transfer progress.** While a transfer runs, a sheet over the main window shows the current file, overall progress, file count, speed and time left. Its buttons:
  - **Cancel** stops the current transfer.
  - **Cancel All** appears when more transfers are waiting.
  - **Hide** (Esc) keeps the transfer going in the background. The sheet comes back with the next transfer.
  - **Show Details** opens the Transfers window.
- **Transfers window** (Window ▸ Transfers, ⌘⌥T): the queue and history of transfers. Transfers run one at a time, and each one lists its files with their status. You can cancel each transfer, and finished downloads can be shown in Finder. The status bar also shows the running transfer; click it to open this window.
- Shortcuts: ⌘↑ enclosing folder, ⌘[ / ⌘] back / forward, ⌘R refresh, ⌘⇧. show hidden files, ⌘U upload, ⌘⇧D download selection, ⌘⌥T Transfers window, ⌫ delete.

## Nintendo Switch (DBI)

When a Switch running [DBI](https://github.com/rashevskyv/dbi) in MTP mode is connected, the app recognises DBI's storages by name ("Installed games", "SD Card install", "NAND install", "Saves", "Album"; DBI changes the numbers between versions) and opens a **Nintendo Switch** section in the sidebar:

- **Installed Games**: the games DBI lists, with their size and NSP files (base, update and DLC). Each game shows an image: the folder thumbnail if DBI provides one, otherwise its newest screenshot from the Album. DBI doesn't expose the game icon itself, because it sits inside the encrypted NSP. **Dump to Mac…** copies the selected games as NSP files.
- **Install**: drop NSP / NSZ / XCI / XCZ files (or folders containing them), or choose them, and pick the SD card or internal memory. DBI installs each file when its transfer completes. Names with accents, CJK or Cyrillic letters make DBI fail with "Nothing to install", so the app offers to send them under a plain name.
- **Saves**: back up the selected games' saves to the Mac, or restore a backup into a game.
- DBI reads the installed games once per MTP session. After installing, click **Reconnect**; if the new games still don't appear, leave MTP mode in DBI and start it again.
- Storages turned off under `[MTP Storages]` in `dbi.config` don't appear. The raw storages stay available under **Storage**.

## Technical notes

- Devices are matched by interface: Still Image class (6/1/1), or a vendor-class interface named "MTP" (Android).
- Large folders are listed with `GetObjectPropList` (depth 1). If the device doesn't support it, the app falls back to `GetObjectInfo` for each file.
- Files over 4 GB: the size is read from `ObjectSize` (64-bit).
- Data is streamed in 512 KB chunks, handling ZLPs and responses appended to the end of the data phase. Cancelling mid-transfer uses the `Cancel` class request, so the session stays usable.
- If the device accepts a command but doesn't answer, the app sends a `Device Reset Request` and retries once.
- Environment variables: `MTP_DEVICE_TIME_ZONE=Europe/Berlin` sets the device's time zone, and `MTP_DEBUG=1` prints a USB/MTP trace to stderr.

## Troubleshooting

| Symptom | Fix |
|---|---|
| *MTP service is not answering* | Unlock the phone. Choose "File transfer" again in the USB notification (turn it off and on if needed). |
| *interface is in use* | Quit Android File Transfer, OpenMTP, SwiftMTP or Image Capture. You can also run `killall ptpcamerad`. |
| No device in the sidebar | Check that the cable carries data and the phone's USB mode. |
| Connected, but no files (Android) | Unlock the phone and tap **Allow** to give access to phone data, then click the device or **Rescan**. |
| *Module compiled with Swift X cannot be imported…* | Two Swift toolchains share `.build/`. Run `rm -rf .build` and build with a single toolchain. |

## Support

If ConnMTP is useful to you, you can buy me a coffee on [Ko-fi](https://ko-fi.com/lodo1410) or [MoMo](https://me.momo.vn/1WfmfQFyUpipImim), or open **About ConnMTP** and click **Donate**.
