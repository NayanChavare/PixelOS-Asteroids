# How to Install / Update This ROM (Nothing Phone 3a / asteroids)

A beginner-friendly step-by-step guide to flashing this ROM.

> ⚠️ **Before You Begin:**
> 1. Your phone's **bootloader must already be unlocked**.
> 2. **Backup your data!** A clean flash (required when coming from Stock or another ROM) will wipe all files and apps from your phone.
> 3. Keep your phone charged to at least **50%**.

---

## 🧰 Tools & Files You Need

1. **Official Google Platform-Tools (ADB & Fastboot):**
   * **Windows 10/11:** Open PowerShell and run:
     ```powershell
     winget install -e --id Google.PlatformTools
     ```
   * **Mac / Linux:** Download the official package directly from [Google's Platform-Tools](https://developer.android.com/tools/releases/platform-tools).
   > ⛔ **Important:** Avoid third-party installers like "Minimal ADB and Fastboot"; they are outdated and will fail on modern dynamic partition devices.

2. **Files to Download:**
   * **ROM Installation Zip** (e.g., `PixelOS_asteroids-....zip`)
   * **`recovery.img`** *(Only needed if coming from Stock Nothing OS)*
   * **`super_empty.img`** *(Only needed if coming from Stock or another Custom ROM)*

> ℹ️ *Note: Separate partition images like `boot.img`, `dtbo.img`, `vendor_boot.img`, and `init_boot.img` are **not required**.*

---

## 🧭 Choose Your Scenario

* **[1. Coming from Stock Nothing OS](#1-coming-from-stock-nothing-os-clean-flash)** (First time installing a custom ROM)
* **[2. Coming from Another Custom ROM](#2-coming-from-another-custom-rom-clean-flash)** (e.g., LineageOS, AOSPA, etc.)
* **[3. Updating / Dirty Flashing](#3-updating--dirty-flashing-from-a-previous-build)** (Already running a previous build of this ROM)

---

## 1. Coming from Stock Nothing OS (Clean Flash)

Follow these steps if you are currently running official Nothing OS.

### Step 1: Reboot into Bootloader Mode
Connect your phone to your computer with a USB cable. Open your terminal or PowerShell and run:
```bash
adb reboot bootloader
```
*(Alternatively, power off the phone and hold **Volume Down + Power** until the bootloader screen appears).*

### Step 2: Flash the Recovery Image
In the folder where your downloaded files are located, run:
```bash
fastboot flash recovery recovery.img
```

### Step 3: Reboot to Fastbootd Mode
```bash
fastboot reboot fastboot
```
*(Your phone will reboot into a screen that says **fastbootd** at the top).*

### Step 4: Wipe the Super Partition
While in `fastbootd` mode, run:
```bash
fastboot wipe-super super_empty.img
```

### Step 5: Enter Recovery Mode
```bash
fastboot reboot recovery
```

### Step 6: Sideload the ROM
1. On your phone screen, use the Volume buttons to navigate and the Power button to select:
   **Apply Update** ➔ **Apply from ADB**
2. On your computer, run:
   ```bash
   adb sideload <path_to_rom>.zip
   ```
   *(Wait for the transfer to finish. It is completely normal for it to pause at 47% or 94% — see notes below).*

### Step 7: Factory Reset (Required)
1. Once installation finishes, return to the main recovery menu.
2. Select **Factory Reset** ➔ **Format data / factory reset** and confirm.

### Step 8: Reboot to System
Select **Reboot system now**. Welcome to your new ROM!

---

## 2. Coming from Another Custom ROM (Clean Flash)

Follow these steps if you are switching over from a different custom ROM (e.g., LineageOS, AOSPA, etc.).

### Step 1: Reboot into Fastbootd
With your phone connected to your computer, run:
```bash
adb reboot fastboot
```
*(Or from your current custom recovery, select **Advanced** ➔ **Enter fastboot**).*

### Step 2: Wipe the Super Partition
While in `fastbootd` mode, run:
```bash
fastboot wipe-super super_empty.img
```

### Step 3: Reboot to Recovery
```bash
fastboot reboot recovery
```

### Step 4: Sideload the ROM
1. On your phone screen, select:
   **Apply Update** ➔ **Apply from ADB**
2. On your computer, run:
   ```bash
   adb sideload <path_to_rom>.zip
   ```
   *(Wait for the transfer to finish. It may pause around 47% or 94%).*

### Step 5: Factory Reset (Required)
1. Return to the main recovery menu.
2. Select **Factory Reset** ➔ **Format data / factory reset** and confirm.

### Step 6: Reboot to System
Select **Reboot system now**.

---

## 3. Updating / Dirty Flashing (From a Previous Build)

Follow these steps if you are already on this ROM and just upgrading to a newer release. **Your apps, files, and personal data will remain untouched.**

### Step 1: Reboot into Recovery
With your phone connected to your computer, run:
```bash
adb reboot recovery
```
*(Or power off the phone and hold **Volume Up + Power** until recovery appears).*

### Step 2: Sideload the ROM
1. On your phone screen, select:
   **Apply Update** ➔ **Apply from ADB**
2. On your computer, run:
   ```bash
   adb sideload <path_to_rom>.zip
   ```

### Step 3: Skip Additional Packages Prompt
When installation finishes, if the recovery asks: *"Install additional packages?"*, select **No**.

### Step 4: Keep Your Data
* **DO NOT format data / factory reset!** Doing so will wipe your phone.
* *(Only factory reset if the release notes for a specific build explicitly mandate a clean flash).*

### Step 5: Reboot to System
Select **Reboot system now**.

---

## 💡 Things That Look Scary But Are Completely Normal ✅

* **Sideload Pauses at 47% or 94%:**
  During `adb sideload`, the progress bar frequently pauses or stops at **47%** (verifying payload) or **94%** (finishing partition unmounts). This is normal behavior on modern Android recoveries! As long as your phone displays **"Install completed with status 0"** or your PC terminal shows `Total xfer: 1.00x` / `step 2/2`, the installation was 100% successful.
* **Error Message About `/metadata/ota`:**
  Seeing a notice or warning about `/metadata/ota` after formatting or updating is harmless and expected.
* **Planning to Root (Magisk / KernelSU / APatch)?**
  Always boot into the system normally **at least once** before flashing any root modules or patched boot images. This ensures your internal data encryption keys finalize properly first.
