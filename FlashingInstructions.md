# How to Install This ROM (Beginner-Friendly Guide)

This guide assumes your phone's **bootloader is already unlocked**. If it's not, you'll need to do that first (it's a separate process, different for every phone).

> **Already running a previous build of this ROM, or coming from another custom ROM?**
> You don't need to do the early steps below — just jump straight to **[Step 8: Enter Recovery](#8-enter-recovery)**.

---

## What You'll Need First

- A computer (Windows, Mac, or Linux)
- A USB cable to connect your phone to the computer
- The ROM files (boot.img, dtbo.img, recovery.img, etc. — these come with the ROM download)

---

## Step 1: Install "Platform Tools" on Your Computer

Platform Tools are a small set of programs called **ADB** and **Fastboot**. They let your computer "talk" to your phone when it's plugged in — this is required to install the ROM.

⚠️ **Important:** Don't use "Minimal ADB and Fastboot" or any other random installer you find online — some are outdated and can cause problems. Get the official tool from Google.

**If you're on Windows 10 or 11**, open PowerShell and run:
```powershell
winget install -e --id Google.PlatformTools
```
This is the easiest and safest way to get it.

*(If you're on Mac or Linux, or winget doesn't work, search for "Android Platform Tools" from Google's official site instead.)*

---

## Step 2: Turn On Developer Options and USB Debugging

This unlocks hidden settings on your phone that let a computer control it. (If you've already unlocked your bootloader, you may have already done this step.)

---

## Step 3: Put Your Phone Into "Fastboot Mode"

Fastboot mode is a special screen your phone boots into that lets your computer install system files directly. It's different from the regular bootloader screen.

Plug your phone into your computer, then run:
```bash
adb reboot fastboot
```
Your phone screen should now look different — that means it worked.

> If your computer doesn't detect the phone at this point (Windows only), you may need to install a driver called **"Android Bootloader Interface."**

---

## Step 4: Install the Core System Files

These commands copy the essential files onto your phone. Run them one at a time, in this order, while your phone is still connected and in Fastboot Mode:

```bash
fastboot flash boot boot.img
fastboot flash dtbo dtbo.img
fastboot flash vendor_boot vendor_boot.img
fastboot flash init_boot init_boot.img
fastboot flash recovery recovery.img
```

*("Flashing" just means writing/installing a file directly onto the phone's storage.)*

---

## Step 5: Restart to the Bootloader Screen

```bash
fastboot reboot bootloader
```

---

## Step 6: Restart Into the New Recovery's Fastboot Mode

```bash
fastboot reboot fastboot
```

### Step 6a: Clear Out Old Storage Partitions ("Wipe Super")

This step clears space on your phone so the new system can be installed cleanly.

```bash
fastboot wipe-super super_empty.img
```

> 📁 You'll find the `super_empty.img` file included with your ROM download — check the notes/download page for it.

---

## Step 7: Restart to the Bootloader One More Time

```bash
fastboot reboot bootloader
```

---

### 🔀 From here, the steps depend on how you're installing the ROM

The rest of this guide covers installing via an **OTA zip file** (the most common method).

---

## 8. Enter Recovery

"Recovery" is a special menu on your phone (separate from your normal home screen) used for installing updates.

```bash
fastboot reboot recovery
```

## 9. Start the Update Process

On your phone's recovery screen, use the volume/power buttons to navigate to:

**Apply Update → Apply from ADB**

## 10. Send the Update File to Your Phone

Back on your computer, run this (replace the path with wherever your ZIP file actually is):

```bash
adb sideload /path/to/ota.zip
```

This sends the ROM update file from your computer to your phone over the USB cable.

## 11. Skip Extra Files

After the file finishes sending, your phone may ask if you want to install anything else. Choose **No** unless you specifically have another file to add.

## 12. Factory Reset

From the main recovery menu, choose **Factory Reset**.

> ⚠️ If you're **updating** from a previous version of this same ROM (not installing fresh), **skip this reset step** unless you were told otherwise — it will erase your data.

---

### A Few Things That Look Scary But Are Actually Fine ✅

- While sending the update file, your phone's progress bar may **stop at 47%** — this is completely normal, just wait.
- You might see an **error message about `/metadata/ota`** after formatting — this is also normal and can be ignored.
- To check if a step actually succeeded, look at your phone's screen for an **"exit status 0"** message — that means success.

---

## Final Step: Reboot to System

From the main recovery menu, choose **Reboot to System**. Your phone will now start up on the new ROM.

---

### 🔑 Planning to Root Your Phone?

If you're updating from an older version **and** you want root access afterward:
Let your phone boot up normally **at least once, without root**, before flashing any rooted/patched files. Doing it out of order can cause issues.
