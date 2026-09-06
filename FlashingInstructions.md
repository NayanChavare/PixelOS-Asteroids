# Install Instructions

This assumes you've already unlocked your bootloader.

> **Upgrading from a previous build or coming from another custom ROM?**
> Skip straight to [Step 8](#8-enter-recovery).

## 1. Install Android SDK Platform Tools

Install Platform Tools if you haven't already.

> ⚠️ **Do NOT use Minimal ADB and Fastboot** or other outdated installers.

If you're on Windows 11 or the latest version of Windows 10, `winget` is preinstalled and is the fastest, more reliable way to get adb/fastboot working globally:

```powershell
winget install -e --id Google.PlatformTools
```

## 2. Enable Developer Options and USB Debugging

## 3. Reboot to Fastboot Mode

Reboot your device to **fastboot mode** (**not** bootloader mode):

```bash
adb reboot fastboot
```

> If your device is not detected by fastboot on Windows, install the correct drivers for **Android Bootloader Interface**.

## 4. Flash Recovery and Required Images

```bash
fastboot flash boot boot.img
fastboot flash dtbo dtbo.img
fastboot flash vendor_boot vendor_boot.img
fastboot flash init_boot init_boot.img
fastboot flash recovery recovery.img
```

## 5. Reboot to Bootloader Mode

```bash
fastboot reboot bootloader
```

## 6. Reboot to the New Recovery's Fastboot Mode (fastbootd mode)

```bash
fastboot reboot fastboot
```

## 6a. Wipe Super

```bash
fastboot wipe-super super_empty.img
```

> You can find `super_empty.img` in the notes!

## 7. Reboot to Bootloader

Reboot to bootloader once.

```bash
fastboot reboot bootloader
```

---

### If You Have an OTA Zip

## 8. Enter Recovery

```bash
fastboot reboot recovery
```

## 9. Apply Update via ADB

From the recovery menu: **Apply Update → Apply from ADB**

## 10. Sideload the OTA

```bash
adb sideload /path/to/ota.zip
```

## 11. Skip Additional Files

Once the sideload completes, you'll be asked if you have any additional files to install. If you don't, choose **No**.

## 12. Factory Reset

Factory reset from the main menu.

> If you are updating from another version, **don't wipe** unless otherwise specified.

---

> **Note:** Always check the phone screen for completion status (exit status `0`) or errors.
> Reaching only 47% during sideload, and `/metadata/ota` printing an error after formatting, are both **normal**.

## Reboot to System

Reboot to system from the main menu.

> **Rooting after an update:** If you're updating from an older version and want to root your device, let it boot **unrooted at least once** before flashing any patched images.
