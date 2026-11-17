# ConnMTP User Guide

ConnMTP lets you browse and copy files between a Mac and an Android phone, a camera or any other MTP device over a USB cable. You don't need to install ADB or turn on USB debugging.

New to ConnMTP? Read [About ConnMTP](ABOUT.md) for what the app does and which devices it supports.

[Download](https://github.com/LinhDinhDev/ConnMTP/releases/tag/Release)

## Contents

1. [Installing](#1-installing)
2. [Connecting a device](#2-connecting-a-device)
3. [The main window](#3-the-main-window)
4. [Browsing files](#4-browsing-files)
5. [Copying files from the Mac to the device](#5-copying-files-from-the-mac-to-the-device-upload)
6. [Copying files from the device to the Mac](#6-copying-files-from-the-device-to-the-mac-download)
7. [Managing files on the device](#7-managing-files-on-the-device)
8. [Following transfers](#8-following-transfers)
9. [Nintendo Switch (DBI)](#9-nintendo-switch-dbi)
10. [Keyboard shortcuts](#10-keyboard-shortcuts)
11. [Troubleshooting](#11-troubleshooting)

---

## 1. Installing

**Requirements:** macOS 13 (Ventura) or later, on an Apple silicon or Intel Mac.

1. Open `ConnMTP-<version>.dmg`.
2. Drag **ConnMTP** into the **Applications** folder.
3. Open ConnMTP from Launchpad or the Applications folder.

**The first time you open it**, macOS may block the app because Apple hasn't notarized it. See [Opening ConnMTP when macOS shows a warning](ABOUT.md#opening-connmtp-when-macos-shows-a-warning) for the steps on each macOS version.

## 2. Connecting a device

### Android phones

1. Connect the phone to the Mac with a USB cable that **carries data** (some cables only charge).
2. **Unlock** the phone.
3. Pull down the notification shade, tap the USB notification and choose **File transfer** (on some phones, *File transfer / Android Auto*).
4. If the phone asks *Allow access to phone data?*, tap **Allow**.

### Cameras and other devices

Connect the cable and turn the device on. If the camera has a USB mode setting, choose **PTP** or **MTP**.

### In ConnMTP

- The device appears under **Devices** in the sidebar. If it's the only device, the app connects to it automatically.
- With more than one device, click the one you want. The line under its name turns into a green **Connected** once it's connected.
- If the device doesn't appear, click the **Rescan** button (circular arrow) in the sidebar's toolbar.

> **Note:** only one program can use the MTP connection at a time. Quit Android File Transfer, OpenMTP, Image Capture and Preview before using ConnMTP.

A connected device has two buttons next to it:

- **ⓘ** (Device information): shows the manufacturer, model, firmware, serial number and the capacity of each storage.
- **⏏** (Disconnect): disconnects the device. Disconnect before unplugging the cable.

## 3. The main window

```
┌──────────────┬──────────────────────────────────────────────────────┐
│ Devices      │ ‹ ›   [List|Icons]   📁+  ⬆  ⬇  🗑  ⟳   🔍 Filter     │
│  📱 Pixel 8  ├──────────────────────────────────────────────────────┤
│              │ Internal shared storage › DCIM › Camera              │
│ Storage      │                                                      │
│  Internal    │   Files and folders                                  │
│  ▓▓▓▓▓░░░    │                                                      │
│  SD card     │                                                      │
│              ├──────────────────────────────────────────────────────┤
│              │ 120 items       [running transfer]     24 GB avail.  │
└──────────────┴──────────────────────────────────────────────────────┘
```

- **Sidebar (left):**
  - **Devices**: the devices that are plugged in.
  - **Storage**: the device's storages (internal storage, SD card…), each with a usage bar and a *“… free of …”* line. The bar turns red when more than 90% is used. A lock icon means the storage is read-only.
  - **Nintendo Switch**: only appears when a Switch running DBI is connected (see [section 9](#9-nintendo-switch-dbi)).
- **Toolbar (top):** back/forward, view mode, new folder, upload, download, delete, refresh and the filter field.
- **Path bar:** shows which folder you're in. Click a level to go back to it.
- **Status bar (bottom):** the number of items, how many are selected and their total size, the running transfer (click it for details), and the free space.
- **ⓘ button (About ConnMTP)** in the sidebar: shows the app version.

## 4. Browsing files

- **Open a folder:** double-click it.
- **Open a file:** double-click it. The app downloads the file to a temporary folder and opens it with its default app on the Mac (for example, photos open in Preview). Changes you make to that copy are **not** saved back to the device.
- **Go back:** the **‹** button or ⌘[; go to the enclosing folder with ⌘↑. Go forward with the **›** button or ⌘].
- **Refresh:** the **⟳** button or ⌘R, for when files on the device have just changed.

### Two views

| View | How to switch | What you get |
|---|---|---|
| **List** | ⌘1 or the List button | A table with name, date modified, size and kind columns. Click a column header to sort. |
| **Icons** | ⌘2 or the Icons button | A grid of icons, with thumbnails for photos and videos. The **Sort & Size** button sorts by Name / Date Modified / Size and sets the icon size. |

The app remembers the view you chose for next time.

### Filtering and hidden files

- Type in the **Filter this folder** field at the top right to show only items whose name contains that text (in the open folder only).
- ⌘⇧. (Command-Shift-period) or **Go ▸ Show Hidden Files** shows or hides hidden files (names that start with a period).

### Selecting several items

- Hold ⌘ and click to select items one by one; hold ⇧ to select a range.
- ⌘⌥A (**Edit ▸ Select All Items**) selects everything.

## 5. Copying files from the Mac to the device (Upload)

First open the destination folder on the device, then use one of these:

- **Drag and drop:** drag files or folders from Finder into the ConnMTP window. The file area is tinted slightly when you can drop.
- **The Upload button** (⬆) or ⌘U, then choose the files or folders.
- **Copy and paste:** select files in Finder, press ⌘C, switch to ConnMTP and press ⌘V.
- Right-click empty space and choose **Upload Files…**.

Folders are copied with everything inside them.

## 6. Copying files from the device to the Mac (Download)

Select files or folders in ConnMTP, then:

- **Drag and drop:** drag the items to Finder or the Desktop. Files are downloaded only when you drop them.
- **The Download button** (⬇) or ⌘⇧D, then choose a folder and click **Download Here**.
- Right-click and choose **Download…** (pick where to save) or **Download to Downloads Folder** (save straight into Downloads).

Tip: to get photos off a phone, open **DCIM ▸ Camera**, switch to the **Icons** view to see thumbnails, select the photos and drag them to the Desktop.

### Name clashes

If an item with the same name already exists at the destination, the app asks:

- **Replace**: overwrite the existing file.
- **Skip**: leave the existing file as it is.
- **Cancel**: cancel the whole transfer.

Folders with the same name are always merged; the question only applies to the files inside them.

## 7. Managing files on the device

Right-click a file or folder (or empty space) to open the menu.

| To | Do this |
|---|---|
| Create a folder | Click **New Folder** (📁+) or right-click empty space ▸ **New Folder…**, type a name and click **Create**. |
| Rename | Right-click ▸ **Rename…**, type the new name and click **Rename**. Names can't contain “/” or be “.” / “..”. |
| Delete | Select the items, press ⌫ or click **Delete** (🗑), then confirm with **Delete**. |
| Copy on the device | Select the items, press ⌘C (or right-click ▸ **Copy**), open the destination folder and press ⌘V. |
| Move on the device | Select the items, press ⌘X (or right-click ▸ **Cut**), open the destination folder and press ⌘V. |
| Get the path | Right-click ▸ **Copy Path**. The path is copied to the clipboard. |

> **Careful when deleting:** items are deleted **permanently** from the device; they don't go to the Trash. Deleting a folder deletes everything inside it.

Notes:

- When you paste into the same folder as the original, the copy is named “… copy”.
- If the device can't copy by itself, the app downloads the items to the Mac and uploads them again, so large files take longer.
- You can't copy and paste between two different devices. Download to the Mac first, then upload to the other device.

## 8. Following transfers

### The progress sheet

While a transfer runs, a sheet over the main window shows the current file, the percentage, the file count, the speed and the time left. Its buttons:

- **Cancel**: stops the running transfer. The device stays usable.
- **Cancel All**: also cancels the transfers that are waiting (only shown when some are waiting).
- **Hide** (or Esc): hides the sheet while the transfer keeps running in the background, so you can keep browsing. The sheet comes back with the next transfer.
- **Show Details**: opens the Transfers window.

### The Transfers window

Open it with **Window ▸ Transfers**, ⌘⌥T, or by clicking the transfer in the status bar.

- It lists every transfer: waiting, running, finished, failed or cancelled. Each one lists its files and their status.
- Transfers run **one at a time**. Later ones show *Waiting — another transfer is in progress*.
- The ✕ button cancels a transfer; the magnifying glass (**Show in Finder**) shows downloaded files in Finder.
- **Clear Finished** removes finished transfers from the list; **Cancel All** cancels everything.

## 9. Nintendo Switch (DBI)

This section is for a Nintendo Switch running the [DBI](https://github.com/rashevskyv/dbi) homebrew app.

**Connecting:** open DBI on the Switch, choose **Run MTP responder**, then connect the cable to the Mac. The ConnMTP sidebar gains a **Nintendo Switch** section with three parts. You can also switch between them with the control at the top of the window.

### Installed Games: view and back up installed games

- Lists the games with their size. Type in **Filter games** to search.
- Select a game to see its files: the base game, the update and any DLC.
- **Dump to Mac…**: select games, click this button, choose a folder and click **Dump Here**. The games are copied to the Mac as NSP files (base game, update and DLC as separate files).
- Double-click a game (or right-click ▸ **Show in Files**) to see its folder as ordinary files.

### Install: install games

1. Under **Install to**, choose **SD card** or **Internal memory (NAND)**. The free space is shown next to each.
2. Drop **NSP, NSZ, XCI or XCZ** files (or folders containing them) onto the dashed area, or click **Choose Files…** (⌘O).
3. Follow the install on the Switch screen. DBI installs each file as soon as it has been copied.

Messages you may see:

- **Names with accents or special characters:** DBI reports *Nothing to install* for names with accented, Chinese/Japanese/Korean or Cyrillic letters. The app offers to send the files under a plain name; choose **Use Plain Names**. Your files on the Mac are not renamed.
- **Not enough free space?:** there may not be enough room. NSZ and XCZ files are decompressed while installing, so they need more space than their file size.
- **DBI shows a CRC or “Extra buffers exceeded” error:** start DBI by holding R while launching a game, not from the Album.

**Newly installed game not in Installed Games?** DBI reads the game list only once per connection. Click **Reconnect** in the toolbar. If it still doesn't appear, leave MTP mode in DBI and start it again.

### Saves: back up and restore game saves

- **Back Up…**: select one or more games, click the button, choose a folder and click **Back Up Here**.
- **Restore…**: select **one** game, click the button, choose that game's backup folder, then confirm with **Restore**.

> **Note:** restoring **overwrites** the existing saves on the Switch. Back up the current saves first if you may need them.

To delete a save, right-click the game ▸ **Show in Files** and delete it like an ordinary file.

### When a part is turned off

If a part shows *“… is turned off in DBI”*, that item is disabled in the `dbi.config` file on the Switch's SD card. Open the `[MTP Storages]` section of that file, turn the matching item back on (for example *Installed games*, *SD Card install*, *NAND install*, *Saves*), then reconnect.

DBI's raw storages can still be browsed as ordinary files under **Storage** in the sidebar.

## 10. Keyboard shortcuts

| Keys | Action |
|---|---|
| ⌘1 / ⌘2 | View as List / Icons |
| ⌘↑ | Enclosing folder |
| ⌘[ / ⌘] | Back / Forward |
| ⌘R | Refresh |
| ⌘⇧. | Show / hide hidden files |
| ⌘⌥A | Select all |
| ⌘U | Upload files from the Mac |
| ⌘⇧D | Download the selection to the Mac |
| ⌘C / ⌘X / ⌘V | Copy / Cut / Paste |
| ⌫ | Delete the selection |
| ⌘⌥T | Open the Transfers window |
| Esc | Hide the progress sheet (the transfer keeps running) |
| ⌘O | Choose game files to install (in the Switch's Install part) |

## 11. Troubleshooting

| Symptom | Fix |
|---|---|
| The sidebar says **No devices** | Check that the cable carries data (try another cable). Unlock the phone and choose **File transfer**. Click **Rescan**. |
| *The MTP interface is in use by another program* | Quit Android File Transfer, OpenMTP, Image Capture and Preview. If it still fails, open Terminal, run `killall ptpcamerad` and try again. |
| *The device is connected but its MTP service is not answering* | Unlock the phone. In the USB notification, choose **File transfer** again (if it's already selected, switch to another mode and back). |
| *Timed out waiting for device* | Unlock the phone and check that it's in **File transfer** mode. Unplug the cable and plug it back in. |
| Connected but no files (Android) | Unlock the phone and tap **Allow** in the prompt asking for access to phone data. Then click the device in the sidebar again, or click **Rescan**. |
| *The device was disconnected* | The cable came loose or the phone disconnected. Reconnect the cable and unlock the phone. |
| *This storage is read-only* | This storage only allows reading (it has a lock icon). You can download from it, but not upload, rename or delete. |
| File dates are off by a few hours | Some devices don't report their time zone. This is a device limitation; the file contents are not affected. |
| macOS says the app can't be opened | See [Installing](#1-installing). |

If you still have a problem, note the exact error message and the device's name and model (shown by the **ⓘ** button next to the device) when you report it to the developer.
