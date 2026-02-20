# NFC Tile

A minimalist app to add an NFC tile to Android Quick Settings.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="screenshots_dark.png">
  <source media="(prefers-color-scheme: light)" srcset="screenshots_light.png">
  <img alt="App screenshots" src="screenshots_light.png" width="100%">
</picture>

## Features

- **Minimal size** - ~12 KB for NoLauncher versions
- **System-like behavior** - blends in with other Quick Settings tiles in appearance and function
- **No background processes** - works only when needed
- **Works without Root** - just grant permission via ADB

## Overview

Designed for AOSP-based devices (e.g. Pixel) that don’t include a native NFC tile. Expected to work on most OEM skins, though the icon may look slightly different.

## Choosing a Version

| Version | Differences |
|:-------:|-------------|
| [**Regular**](../../releases/latest/download/NFC_Tile.apk)<br>Android&nbsp;7.0+ | Has launcher icon and instruction dialog for granting permission. |
| [**NoLauncher**](../../releases/latest/download/NFC_Tile_NoLauncher.apk)<br>Android&nbsp;8.0+ | No launcher icon, no instruction dialog. |
| [**NoSubtitle**](../../releases/latest/download/NFC_Tile_NoLauncher_New.apk)<br>Android&nbsp;8.0+ | Same as NoLauncher, but without subtitle. For Android 16+ with the new Quick Settings design. If your system tiles don't have "On/Off" subtitles, use this version. |

**Note:** On Android 8-11, subtitles are not displayed in any version due to Android's own limitations. Subtitles are available starting from Android 12.

## Installation and Setup

### Step 1: Download

Download the required APK version by clicking the name in the table above or from the [Releases](../../releases) section.

### Step 2: Install APK

Install the downloaded file. For initial installation, use the **Regular** version.

### Step 3: Grant WRITE_SECURE_SETTINGS Permission

> ⚠️ **Permission required for instant toggle**
> The `android.permission.WRITE_SECURE_SETTINGS` permission is needed to switch NFC directly. Without it, the tile will only open NFC system settings.

#### Option 1: Root (easiest)

1. Open the app
2. In the dialog, tap the **Root** button
3. Done!

#### Option 2: ADB (via computer)

1. Enable **Developer options** on your device
2. Enable **USB debugging**
3. On some devices (Oppo/Realme/OnePlus), you also need to enable **Disable Permissions Monitoring**
4. Download [Android Platform Tools](https://developer.android.com/tools/releases/platform-tools)
5. Connect your device to the computer and run:
```bash
adb shell pm grant com.vlrs.nfc android.permission.WRITE_SECURE_SETTINGS
```

After granting permission, you can safely turn off USB debugging, "Disable Permissions Monitoring", and Developer options.

#### Option 3: Without a computer (for advanced users)

If you can't connect to a PC:

- **[LADB](https://github.com/tytydraco/LADB)** - local ADB over Wi-Fi
- **[Shizuku](https://github.com/RikkaApps/Shizuku)** with [aShell](https://github.com/DP-Hridayan/aShellYou) or an app to grant permissions via Shizuku

After granting permission, you can safely turn off Wireless debugging, "Disable Permissions Monitoring", and Developer options.

### Step 4: (Recommended) Hide the Icon

#### For Android 7-9

1. Open the app
2. Enable the **Hide icon from Launcher** checkbox
3. Tap **Apply and Exit**

#### For Android 8-16+

After successfully granting permission, install **NoLauncher** (or **NoSubtitle** for Android 16+) over the regular version.

### Step 5: Add the Tile to Quick Settings

Open Quick Settings, tap the pencil/edit icon, find the tile named **NFC** or **NFC Tile**, and drag it to your desired position.

## Usage

- **Short tap** - toggle NFC on/off (if permission granted)
- **Long press** - open NFC system settings
- **Tap without permission** - open NFC system settings

The on/off state is shown even without the permission.

## Source Code

The source code is not published separately because the app was originally written directly in [smali](https://github.com/JesusFreke/smali/wiki) assembly. Decompiling the APK with [ApkTool](https://apktool.org) will give you essentially the original project, except for auto-generated label names and a few missing comments.

## Credits

- **Nfc Switcher** (lack006) - inspired the main window design
- **Tiles** (rascarlo) - where I found out about using WRITE_SECURE_SETTINGS permission instead of root
