# iOS 26 Control Centre — Systemless Module

> **A flashable systemless wrapper that mounts the iOS 26-style Control Centre SystemUI plugin on HyperOS 3 — so it actually works, instead of failing to sideload.**

[![Platform](https://img.shields.io/badge/platform-Magisk%20%7C%20KernelSU%20%7C%20APatch-blue)](#-requirements)
[![HyperOS](https://img.shields.io/badge/HyperOS-3-orange)](#-requirements)
[![Status](https://img.shields.io/badge/status-unofficial-red)](#-credits--licensing)

> ⚠️ **HIGH RISK — READ BEFORE FLASHING**
> This module modifies **SystemUI**. On an incompatible device or HyperOS build it can cause **SystemUI crashes, bootloops, or a non-booting device**. You are responsible for your own device. **Read [Recovery](#-recovery) first.**

---

## 📖 Table of Contents

- [What this is](#-what-this-is)
- [Why this exists](#-why-this-exists)
- [Requirements](#-requirements)
- [Installation](#-installation)
- [Recovery](#-recovery)
- [Compatibility](#-compatibility)
- [Uninstalling](#-uninstalling)
- [Credits & licensing](#-credits--licensing)
- [Disclaimer](#-disclaimer)
- [Reporting issues](#-reporting-issues)

---

## 🧩 What this is

A **systemless module** that places the iOS 26-style Control Centre SystemUI plugin where HyperOS 3 expects it — without permanently modifying `/system`.

- ✅ Nothing in `/system` is touched permanently
- ✅ Fully removable by disabling or uninstalling the module
- ✅ Works with Magisk / KernelSU / APatch
- ❌ Not a rewrite, port, or modified build — the APK is bundled **as-is**

**Inside the zip:**

| Component | Description |
|---|---|
| `module.prop` | Module metadata |
| `customize.sh` / install logic | Systemless install script |
| Bundled APK | Original SystemUI plugin, **unmodified** |

---

## 💡 Why this exists

The original plugin was shared on Telegram, but it **cannot be installed normally** — it has to live as a system component for SystemUI to pick it up. Sideloading it simply doesn't work.

This module solves exactly that problem: it **mounts the APK systemlessly** in the right place, so the plugin loads without you having to touch `/system` or risk a permanent modification.

The value here is the **installation method**, not the APK itself.

---

## 📋 Requirements

- **HyperOS 3** — this targets the HyperOS 3 SystemUI Plugin. Other versions are **untested and likely incompatible**.
- **Magisk**, **KernelSU**, or **APatch**
- A **custom recovery** or working **`adb`** — strongly recommended for recovery
- A **backup** of your current setup

---

## 🚀 Installation

1. Download the latest `.zip` from [**Releases**](../../releases).
2. Flash it in **Magisk / KernelSU / APatch**.
3. **Reboot once** to let the systemless overlay mount.
4. **Reboot a second time** — the Control Centre may not appear until after this second reboot. This is expected and not a bug.
5. If SystemUI crashes or the device bootloops → go to [**Recovery**](#-recovery).

> 💡 **Tip:** If the module appears installed but nothing has changed after two reboots, try clearing SystemUI's cache or re-flashing the module, then reboot again.

---

## 🛟 Recovery

**If your device bootloops or SystemUI keeps crashing, do this:**

### Magisk

- Boot into **safe mode** — hold **Volume Down** during boot until it vibrates. Modules are disabled automatically.
- Or remove the module folder via `adb`:

```sh
adb shell su -c "rm -rf /data/adb/modules/ios_26_cc"
```

### KernelSU / APatch

- Boot to recovery and delete the module folder:

```sh
adb shell su -c "rm -rf /data/adb/modules/ios_26_cc"
```

- Or use the manager's **"Disable module"** option if you can still reach it.

### Last resort

- Dirty-flash your current ROM, or restore your **boot backup**.

> 💡 **Tip:** Always keep a working `adb` connection or a recovery image available *before* flashing a SystemUI mod.

---

## 📱 Compatibility

| Device | HyperOS version | Status | Notes |
|---|---|---|---|
| Redmi Note 14 4G | HyperOS 3 | ✅ Works | |
| | | | |

> **Help build this table** — open an issue with your **device model**, **HyperOS version**, and **result** (works / crashes / bootloop). Every report makes this safer for the next person.

---

## 🗑 Uninstalling

- **Magisk:** Modules → find `iOS 26 Control Centre` → Remove → Reboot.
- **KernelSU / APatch:** Manager → Modules → disable or uninstall → Reboot.
- **Manual:** delete `/data/adb/modules/ios_26_cc` and reboot.

Because the module is **systemless**, removal leaves no trace in `/system`.

---

## 🙏 Credits & licensing

- **SystemUI plugin APK** — original author, shared via Telegram: <https://t.me/EGLife2023/221590>. All rights to the APK belong to its original author. It is bundled here **unmodified** and **without a license grant** from its author.
- **Systemless wrapper, module scripts, and packaging** — **Dextrecs**.

**No license is applied to this repository.** The wrapper code is provided **as-is for personal use**. The bundled APK remains the property of its original author.

**Takedown:** If you are the author of the bundled APK and want it removed from this repository or its releases, please open an issue or contact me — I will remove it promptly.

---

## ⚠️ Disclaimer

This module is provided **as-is, with no warranty of any kind**, express or implied. Flashing it may cause **SystemUI crashes, bootloops, data loss, or a non-booting device**. **You are solely responsible for your own device.** Only flash this if you know how to recover from a soft brick.

---

## 🐞 Reporting issues

Open an issue and include:

- **Device model**
- **HyperOS version**
- **What happened** (description)
- **Logcat** if possible:

```sh
adb logcat -d > logcat.txt
```

- **Whether you can recover** (safe mode / recovery / adb)

> Please search existing issues before opening a new one — someone may have already reported your device.
