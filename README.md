# Axon U-Boot User Guide

This document provides instructions for:

* Flashing OS images to supported storage devices
* Accessing the U-Boot via HDMI and keyboard
* Using the interactive boot menu
* Installing U-Boot using APT

---

## Supported Boot Devices

The Axon U-Boot supports booting from the following storage devices:

* USB Drive
* NVMe SSD
* SD Card
* eMMC

---

## Flashing Images to Storage Devices

**Caution**: Be sure to use the correct device path (e.g., `/dev/sdX`, `/dev/nvme0n1`) to avoid overwriting important data.

[Download eMMC Image](https://drive.google.com/file/d/1BYcnlJjHHNbGBsgnQMTn5ydN8Gc7QB-e/view?usp=drive_link)

[Download Raw Image](https://drive.google.com/file/d/1Zz_FKpvpcDQBfyncV0C8VQCTakyDlAzD/view?usp=drive_link)

Note : Raw image can be used in SD Card, NVMe and USB Storage Media device.

### Flashing to eMMC

Refer to the detailed guide:
**[eMMC Flashing Guide (Vicharak Docs)](https://vicharak.docs/emmc)**

### Flashing to NVMe SSD

```bash
sudo dd if=<image-name> of=/dev/nvme0n1 status=progress; sync
```

### Flashing to SD Card

```bash
sudo dd if=<image-name> of=/dev/sdX status=progress; sync
```

### Flashing to USB Drive

```bash
sudo dd if=<image-name> of=/dev/sdX status=progress; sync
```

### Verifying the Flash

After flashing, verify the image:

```bash
sudo fdisk -l /dev/<device>
```

Example output:

```
Device          Start     End     Sectors   Size Type
/dev/<device>1   16384    24575     8192     4M  Linux filesystem
/dev/<device>2   24576    32767     8192     4M  Linux filesystem
/dev/<device>3   32768  1081343  1048576   512M  Linux filesystem
/dev/<device>4 1081344  1671167   589824   288M  Linux filesystem
/dev/<device>5 1671168  2195455   524288   256M  Linux filesystem
/dev/<device>6 2195456 13420510 11225055   5.4G  Linux filesystem
```
---

## Accessing Boot Menu and U-Boot Console

### Hardware Requirements (Common to Both)

* **HDMI display** connected to **HDMI TX0**
* **USB keyboard** connected **before** powering on the device

If the keyboard is disconnected after power-on, it will not reconnect. Reboot with the keyboard connected to resolve this.

---

### Accessing the Boot Menu

1. Power on the device.
2. When the **Vicharak logo** appears, press **Ctrl + Q** repeatedly until the boot menu appears.

#### Boot Menu Navigation

* **Arrow keys**: Select the desired boot device (USB, NVMe, SD Card, eMMC)
* **Enter**: Boot from the selected device
* **Shift + D**: Set the selected device as the default boot source for future boots

(Only one USB storage device is supported for booting via the boot menu.)

---

### Accessing the U-Boot Console

1. Power on the device.
2. When the **Vicharak logo** appears, press **Ctrl + C** repeatedly until the U-Boot console appears.

#### U-Boot Console Features

* Load and boot custom kernel or initrd images
* Configure boot parameters
* Set environment variables using `setenv`
* Manually boot from any supported storage device

---

## Installing U-Boot via APT

This U-Boot build includes HDMI console and boot menu functionality specific to Vicharak RK3588-based boards.

### Installation Steps

```bash
sudo apt update
sudo apt install u-boot-rk3588-axon
```

This version includes features not found in upstream or vendor U-Boot builds.

---

## Troubleshooting

### Boot Console or Boot Menu Not Appearing

* Ensure that **Ctrl + Q** (boot menu) or **Ctrl + C** (console) is pressed **immediately** when the Vicharak logo appears.

### Keyboard Not Working

* If the keyboard is unplugged during boot, it will not reconnect.
* Solution: Reboot the board with the keyboard plugged in.

---

## Summary of Features

| Feature                       | Description                                        |
| ----------------------------- | -------------------------------------------------- |
| HDMI Console Support          | U-Boot interaction using HDMI and USB keyboard     |
| Multiple Boot Device Support  | Boot from USB, NVMe, SD Card, or eMMC              |
| Flash Custom OS Images        | Use `dd` to write OS images to storage media       |
| Interactive Boot Menu         | Choose boot source during startup                  |
| Default Boot Source Selection | Configure persistent boot priority using Shift + D |

---

