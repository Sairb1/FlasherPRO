# ⚡ Flasher Pro

A modern Android flashing and repair toolkit for Realme, OnePlus, and OPPO dynamic-partition devices — rebuilt from the ground up with a fast, polished desktop UI.

![Flasher Pro] (<img width="48" height="48" alt="3" src="https://github.com/user-attachments/assets/bf5c9e82-7946-45a1-b305-b696d3f69eab" />)

---

## ⚡ Overview

Flasher Pro simplifies low-level Android operations into a clean, powerful desktop app:

- Flash ROMs (Port / Stock / GSI)
- Extract payloads & partitions — including directly from a live OTA link
- Run ADB / Fastboot commands in a real interactive terminal
- Query official ColorOS/OPlus OTA servers for real, signed download links
- Back up and restore IMEI/NVRAM partitions
- Remove FRP, check battery health, install USB drivers
- Auto-update itself from GitHub Releases

Everything in one place — no tool switching, no command-line juggling.

---

## 🖥️ Requirements

- **OS:** Windows 10 / 11 (64-bit)
- **Device:** USB Debugging enabled
- **Bootloader:** Unlocked (required for flashing features)
- ADB / Fastboot are bundled — no separate driver tool download needed for basic detection, though device-specific USB drivers may still be required (see USB Drivers page in-app)

---

## 📦 Installation

### Download

Grab the latest installer from the [Releases page](https://github.com/Sairb1/FlasherPRO/releases).

- Windows → `Flasher-Pro-Setup-x.x.x.exe`

### Setup

Run the installer, follow the setup wizard, and launch Flasher Pro from the Start Menu or desktop shortcut. The app will check for updates automatically and let you know when a new version is available — updating is one click from the Dashboard.

---

## 🚀 What's New in v7.0

A complete rebuild from the original PySide6 desktop app:

- **All-new interface** — modern glass-panel design system, full light/dark theme support, smooth animations
- **Real-time interactive CMD Studio** — type any ADB/Fastboot command and see live streamed output, drag-and-drop file paths straight into the command line, quick-action shortcuts and a one-click reboot menu
- **Live OTA Downloader** — queries the real official OnePlus / Realme / OPPO update servers directly, returns real signed download links, changelogs, and lets you extract partitions straight from the link without downloading the whole package first when possible
- **Fully automated Stock ROM pipeline** — select a ZIP or payload.bin, it extracts, verifies, sorts, and flashes in the correct order automatically
- **Persistent local usage stats** — the Dashboard tracks how many devices you've detected, flashes completed, OTAs downloaded, and more, right on your machine
- **Auto-update** — Flasher Pro checks GitHub for new releases and can download and install updates itself

---

## 🌟 Features

### 📱 Device Check

- Real-time ADB / Fastboot detection, auto-scans on open
- Device info: brand, model, codename, Android version, build ID, kernel version, battery level
- Bootloader lock status

---

### 🔥 Flash ROM

#### Port ROM
- Flash a folder of `.img` files directly
- Rebuilds OPlus/ColorOS dynamic partitions before flashing (delete → recreate → flash), so ported ROMs fit correctly
- Only flashes whichever images are actually present in your folder — no forced file list
- Optional wipe (userdata / metadata / FRP) and post-flash ADB setup bypass

#### Stock ROM
- Fully automated: point it at an official OTA ZIP or payload.bin
- Extracts `payload.bin`, sorts every image into BOOTLOADER / CRITICAL / SYSTEM / EXTRA / MODEM categories, verifies everything landed correctly, then flashes in the safe order — dual-slot aware
- EXTRA and MODEM are optional — not every firmware ships them, and Flasher Pro won't block a flash over a missing modem image that was never part of the package
- Optional userdata wipe

#### Boot Flasher
- Flash boot, recovery, vendor_boot, init_boot, or dtbo individually

---

### 💿 GSI Flasher

- Verifies your selected folder actually contains `vbmeta.img`, `vbmeta_system.img`, and `system.img` before letting you flash — real filesystem checks, not a guess
- Disables verity/verification, rebuilds the relevant dynamic partitions, flashes the GSI as primary system
- ⚠️ High-risk, permanent operation — wipes user data, requires an unlocked bootloader

---

### 🖥️ CMD Studio

- Live ADB/Fastboot terminal with real streamed output
- Drag and drop a file straight into the command line to insert its full path
- Quick actions: ADB Devices, Fastboot Devices, Dump Logcat, Get Properties
- One-click reboot menu (Bootloader / Recovery / Fastbootd / System)
- Live device connection badge

---

### 📡 OTA Downloader

- Browse real device catalogs for OnePlus, Realme, and OPPO, or run a fully manual query for any model/region/firmware combination
- Queries the actual official OPlus/ColorOS OTA servers — not a static mirror — and returns a real signed download link, file size, MD5, security patch info, and changelog
- Extract partitions directly from the returned link
- Paste your own OTA link if you already have one

---

### 📦 Payload Dumper

- Load a `payload.bin` or OTA ZIP
- Real partition scan — every file shows its actual name and size, straight from the payload header
- Select exactly which partitions to extract
- Clear/reset button to start over with a new file

---

### 🔑 IMEI

Root-required backup and restore of:
- `nvram` · `nvdata` · `persist` · `nvcfg` · `protect1` · `protect2`

Every step verifies a real device is connected and checks real command results before reporting success — no silent false-positives.

---

### 🔓 Remove FRP

- Fastboot-only flow (no unreliable ADB-reboot dependency)
- Two-step confirmation before anything irreversible happens
- Erases FRP, userdata, and metadata, then reboots

---

### 🔋 Battery Health

- **Non-Rooted:** reads live stats via `dumpsys battery` — level, status, health, temperature, voltage, cycle count. Auto-scans on open.
- **Rooted:** reads real kernel power-supply nodes for design capacity and wear percentage

---

### 🔌 USB Drivers

One-click, UAC-elevated installers for:
- Universal Android driver
- MediaTek (MTK) driver
- OPPO MediaTek/Qualcomm HS-USB driver

---

### 📊 Dashboard

- Live usage stats: ADB/Fastboot commands run, flashes completed by type, OTAs downloaded, IMEI backups/restores, FRP removals, devices detected — all saved locally and persisted across restarts
- Update checker with one-click download and install

---

## 🔄 Flashing Flow

**Port ROM:**
`.img folder → fastbootd → delete/recreate dynamic partitions → flash → optional wipe → reboot`

**Stock ROM:**
`ZIP/payload.bin → extract payload → sort into FIRMWARE categories → verify → fastbootd → flash in order → optional wipe → reboot`

**OTA Link:**
`Query official server → real signed link → download or extract directly → flash via Stock ROM pipeline`

**GSI:**
`fastbootd → disable verity → delete partitions → recreate → flash system → optional wipe → reboot`

---

## ⚠️ Disclaimer

This tool performs low-level operations on your device's partitions.

You can:
- Brick your device
- Lose all data
- Break your partition table

Always:
- Back up everything first
- Verify you have the correct firmware for your exact model and region
- Make sure your battery is charged above 60% before flashing
- Understand what an operation does before you click confirm

The developer is not responsible for any damage caused by using this tool.

---

## 🙏 Credits

- **Developer:** Ayan ([@imnotaino](https://github.com/sairb1))
- **OTA query reference:** Abhinav Verma — [github.com/RemuruSama](https://github.com/RemuruSama)
- **UI/UX design system reference:** [Kudu](https://github.com/adventdevinc/kudu) (MIT License)
- Google Platform Tools (ADB/Fastboot)
- lucide-react, Tailwind CSS, Electron & React

---

## 👤 Developer

**Ayan** ([@imnotaino](https://github.com/sairb1))
