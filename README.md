# HP 15-fc0389AU Hackintosh – macOS Sequoia

My OpenCore EFI and installation notes for the HP 15-fc0389AU (Ryzen 5 7530U).

This EFI is made specifically for macOS Sequoia. It is not intended for Tahoe.

## Hardware

- Laptop: HP 15-fc0389AU
- CPU: AMD Ryzen 5 7530U
- GPU: AMD Radeon Integrated Graphics
- RAM: 16 GB DDR4
- macOS: Sequoia 15

## Working

- ✅ Wi-Fi (after installation)
- ✅ Bluetooth
- ✅ Internal microphone
- ✅ Speakers / audio output
- ✅ Built-in camera
- ✅ Keyboard
- ✅ Trackpad

## Not working

- ❌ 3.5 mm headphone jack

## Installation

### 1. Generate your SMBIOS

Before booting, generate your own SMBIOS using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS).
- Open GenSMBIOS.bat
- Select any of the two plist file in EFI/OC folder
- Select `MacBookPro16,3` as the model.
- It will generate unique serial number, MLB and SystemUUID and will add to plist
- Open proper tree and copy serial number, MLB and SystemUUID from plist you just modified with GenSMBIOS then past in the other plist 


### 3. Prepare the installation USB

**For installation:**

- Use [Acidanthera – OpenCorePkg](https://github.com/acidanthera/OpenCorePkg) to download recovery for Sequoia,it will download the recovery in 'com.apple.recovery' folder
- Copy that folder and past in the root of your intallation pendrive
- copy the EFI folder to root of pendrive
- Rename `config_installation.plist` to `config.plist` in the D:/EFI/OC folder(D is your pendrive drive letter)
- Disable secure boot of your laptop and boot the pendrive
- This  `config_installation.plist` configuration includes a workaround for the installation freezing issue related to NootedRed. Use it when booting the installer.
### 4. Internet during installation

- Wi-Fi does not work in the macOS recovery/installation environment with this EFI.

- You will need to connect your phone to the laptop using USB tethering to get internet access during installation.

- Wi-Fi should work after installation when using the final configuration.

### 5. After getting on mac os desktop – IMPORTANT
Mac os is currently running without graphics acceleration(very sluggish) and many feature compromised,to fix it:
1. Open macOS and mount the EFI partition of your internal SSD using an EFI mounting utility.
2. Also mount the EFI partition of your USB pendrive.
3. Open the USB EFI partition and copy its `EFI` folder.
4. Paste that entire `EFI` folder into the EFI partition of your SSD where mac is installed.
5. Now in the pasted EFI ,go to OC delete config.plist , rename  `config_final.plist` to `config.plist`
6. Eject the USB and restart the laptop.
7. Enjoy!

You should now be able to boot macOS directly from your SSD without the USB pendrive.

Keep the USB EFI as backup
###Warning⚠️
- Never use restart in mac os,as it breaks ACPI and EC states,casing boot loop,only use shutdown,sleep

## Credits

- [Acidanthera – OpenCorePkg](https://github.com/acidanthera/OpenCorePkg)
- [CorpNewt – GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)
- NootedRed and other AMD Hackintosh developers.

If something doesn't work on your machine, feel free to open an Issue with your hardware details and a description of the problem. Suggestions and testing reports are welcome.
