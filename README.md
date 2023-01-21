# matebook-x-pro-2020-hackintosh
matebook x pro 2020 hackintosh

Original link: https://github.com/RepoWeaver/MateBook-X-Pro-2020-OpenCore The author has deleted this warehouse, unfortunately

You Must **Change SMBIOS** to use **iCloud Services**,Select MacBookPro16,2 for smbios model

It is not recommended to use opencore to boot win, it is recommended to set efi/refind/refind_x64.efi as the first boot, then you can use refind to start win and Mac normally

config.plist is applicable to unlocked cfg and dvmt, config-lockCFG.plist is used without unlocking cfg and dvmt, see below for unlocking tutorial

Simplify and compile bluetooth, wifi and sound card according to the source code, only support local use, thanks to the author and everyone

Currently working on my Personal Machine, so only **stable versions** will be released

#### Compatible macOS Versions:
big sur   Monterey    Ventura

<strong>macOS Ventura Support Completed, Will keep maintaining</strong></summary>

- Follow Dortania's steps for [making the installer in macOS](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html#setting-up-the-installer)

If you find my work useful:
* please consider **giving** it **a star** to make it more visible.


### DISCLAIMER

- For best results, read the entire README before you start and follow the install instruction throughly.
- I am not responsible for any damages you may cause.
- **This is not a support forum**.
- Should you find an error or improve anything — whether in the config or in the documentation — please consider opening an issue or pull request.
	
	
**This repository is for personal purposes only.**


## Introduction

This repo contains the files needed for getting macOS working on a **Huawei MateBook X Pro (2020 Edition)** laptop with OpenCore.
* This is intended to create a "fully" functional (as far as possible) hackintosh for the Huawei Matebook X Pro.
* The project can be considered **stable**.
* With each new release of macOS we need to resolve each new "minor issue" we run into. 
* If you would like to get started with creating a hackintosh on your MBXP but have non experience, I would highly recommend following [**Dortania's OpenCore Install guide**](https://dortania.github.io/OpenCore-Install-Guide/) and then returning here for troubleshooting or last improvements.


### Summary

- The **compatibility** is **very good** for the most part, most of the stuff works like it would on a real MacBook, including camera, audio, touchpad, iCloud services.
- The **experience** is **pleasant**, as the laptop is smooth and responsive under macOS Big Sur/Catalina/Ventura.
- **Battery life** is **quite great** (from personal experience it **lasts from 4-6 hours** for light works depending on its age with a behaviour very similar to Windows 11.

(With the use of turbo boost disabled)
http://tbswitcher.rugarciap.com/

- The **Intel WiFi** card is soldered onto the motherboard, which means it can't be replaced with a Broadcom one, but the Intel card is now **functional albeit not operating at full speeds** (however it is fine for most use cases).
    * With the latest `AirportItlwm.kext` even **Handoff** and **Continuity** features are working, but with a very limited support for AirDrop and Apple Watch unlocking (see [Changelog for OpenIntelWireless release](https://github.com/OpenIntelWireless/itlwm/releases)).
    * For any issues about `AirportItlwm.kext` please refer first to [**OpenIntelWireless Troubleshooting page**](https://openintelwireless.github.io/itlwm/Troubleshooting.html#kernel-extension-loading-status) and then to [**OpenIntelWireless Gitter Page**](https://gitter.im/OpenIntelWireless/itlwm?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)


### Generate your own SMBIOS Information

For privacy reasons, all SMBIOS information has been wiped out in the configuration file `EFI/OC/config.plist`. You need to generate your unique `SMBIOS` info by yourself (recommend to use [**CorpNewt's GenSMBIOS**](https://github.com/corpnewt/GenSMBIOS)), and inject them into your `config.plist`.
- With every **EFI update** you retrieve from here, please, remember to transfer **your Device details** under `PlatformInfo -> Generic` in your `config.plist`.

<p align="center">

<img src="https://user-images.githubusercontent.com/91159194/148256043-38860f4b-71ba-4f32-9178-013eb2b1a7a1.jpg" width="70%" alt="About this Mac Monterey Working on" />

<p align="center">
- Big Sur/Monterey/Ventura is running well (Config in Releases)
</p>

## Configuration

<div align="left">

| Specifications      | Details                                          |
| :--- | :--- |
| Computer model      | Huawei Matebook X Pro 2020                       |
| Processor           | Intel Core i5-10210U / i7-10510                  |
| Memory              | 16 GB LPDDR3 2133 MHz                            |
| Hard Disk           | WDC PC SN73(NO support Samsung pm981/a)          |
| Integrated Graphics | NVIDIA GeForce MX250 / Intel(R) UHD Graphics 620 |
| Screen              | 3K Display @ 3000 x 2000 (13.9 inch)             |
| Sound Card          | Realtek ALC256                                   |
| Wireless Card       | Intel AC9560                                     |
| Bluetooth Card      | Intel Bluetooth                                  |

</div>




## Status

- [x] **Intel(R) UHD 620** Graphics card  
- [x] **Intel(R) Wireless-AC** & **Intel(R) Bluetooth**
- [x] **Power Management** with support for HWP (Intel Speed Shift & Intel SpeedStep) - Battery Life improvements
- [x] **Sleep** and **Wake** (support for native macOS `hibernatemode3`)
- [x] **Hibernation** (support for native macOS `hibernatemode25` with `HibernationFixup.kext`)
- [x] **Battery support** with better memory access and integration of [Battery Information Supplement]
- [x] **Backlight control** 
- [x] **Fixed Black Screen on boot** (Won't have to close and open lid anymore 🎉)
- [x] **Proper Power Management after wake from sleep**
- [x] I've noticed that when plugging in a display through a hub you may need to plug in twice (This has always happened, just pointing out something)
- [x] Backlight shortcuts (F1 [brightness level down] - F2 [brightness level up])
- [x] Volume shortcuts (F4 [mute] - F5 [audio level down] - F6 [audio level up])
- [x] **Audio** for **Realtek ALC256** card (via `AppleALC.kext` and `layout-id 76`)
- [x] **Speakers** (4 Channels) & Internal Mic
- [x] **Headphone** jack [2 in 1]  (via `ALCPlugFix`)
- [x] **HDMI 2.0** up to two 4K @60 Hz monitors (via LSPCON)
- [x] **Native Color Profile** for Display 3K
- [x] **TouchPad** and **native macOS gestures**
- [x] Touchscreen (Disabled) 
- [x] PCI Devices latency support and complete description for System Information app
- [x] **USB Ports Mapping** (Type-A:1 & Type-C:2) with proper power levels
- [x] **Thunderbolt Port** (limited support,Plug in when booting)
- [x] HD Camera
- [x] NVRAM native support

#### BIOS Settings

- [x] Disable Secure Boot

<summary><strong>Notes</strong></summary>

1. **Intel Bluetooth** could not support some Bluetooth devices
2. **Touchscreen support is disabled by default** (Battery improvement,To enable, please disable SSDT-TPLT.aml)


## Note From espitgn:

There is the possibility of disabling CFG Lock and enabling dvmt 64. There is a power management improvement disabling CFG Lock which is quite good. The procedure (Customising BIOS) is quite easy to follow. 

(look at [this link](https://github.com/ske1996/Matebook-x-pro-2019-Hackintosh-newest/blob/main/readme-en.md#after-installation): "How to disable CFG Lock" and "Change dvmt to 64 mb" in "After installation" section).

I recommend using “InsydeH2OUVE” to modify dvmt and unlock cfg

These guides work without issue on the MateBook X Pro 2020 (tested with BIOS 1.21 versions). 

Each guide shows the changes to do in config.plist as well.
	
### Fixing Sleep (taken from Profzei):

Open up terminal and make the following changes:

```
sudo pmset -a hibernatemode 0
sudo rm -rf /private/var/vm/sleepimage
sudo touch /private/var/vm/sleepimage
sudo chflags uchg /private/var/vm/sleepimage
sudo pmset -a standby 0
sudo pmset -a autopoweroff 0
sudo pmset -a powernap 0
sudo pmset -a proximitywake 0
```
### Headphone Hot Plug:
Install [ALCPlugFix](https://github.com/profzei/Matebook-X-Pro-2018/tree/master/ALCPlugFix)

## Credits
Many great people.
- [ALL]



