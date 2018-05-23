# Post installation

## Install Clover Boot Loader on your HDD

At this point, you are ready for "Post Installation", you first step should be to install the Clover Boot Loader to your HDD. 

Since the installation is very similar to the install you can go to the [Prepare Usb Drive ](https://daton.gitbook.io/daton-mac/~/edit/primary/hackintosh/post-install)and follow the **Installing Clover Boot Loader to USB drive** section skipping the first step of choosing a different install location.

After installing the Boot Loader, you should take an inventory of things working and not working. 

## Patching issues and devices

Since there are still many issues and devices that won't work correctly. For that, we need to patch DSDT, provide a proper config.plist, and install the kexts that are required.

Since you have RealtekRTL8111.kext already injected by Clover, you should have internet access simply by using an Ethernet cable to your router. Plug it in and make sure you have internet access before continuing.

To start, the developer tools must be installed. Run Terminal, and type:

```bash
git
```

You will be prompted to install the developer tools. Since you have internet working, you can choose to have it download and install them automatically. Do that before continuing.  
  
After the developer tools are installed, we need a copy of the [repo](https://github.com/RehabMan/HP-Envy-DSDT-Patch):

```bash
mkdir ~/Projects
cd ~/Projects
# since we are an HP Envy J Series there is this repo ready for us 
git clone https://github.com/RehabMan/HP-Envy-DSDT-Patch envy.git
cd envy.git
./download.sh
./install.sh
```

If you are using a different Hardware, go [here](https://www.tonymacx86.com/).

The `download.sh` script will automatically gather the latest version of all tools \(`patchmatic`, `iasl`, `MaciASL`\) and all the kexts \(`FakeSMC.kext`, `IntelBacklight.kext`, `ACPIBatteryManager.kext`, etc\) from bitbucket. The `install_downloads.sh` will automatically install them to the proper locations.

With the current project, no patched `DSDT/SSDTs` are used. Instead are used Clover hot-patches and a small `SSDT` called `SSDT-HACK`, `SSDT-HACK-K1` or `SSDT-HACK-K2,` depending on your laptop.

```bash
cd ~/Projects/envy.git
make
make install
```

The `make` causes the `SSDT-HACK.aml` files to be compiled \(with `iasl`\), the results placed in `./build`.  
  
Finally, `make install` mounts the EFI partition, and copies the built files where they can be loaded by Clover \(to `EFI/Clover/ACPI/patched`\).

Up to now, you've been using the same `config.plist` we were using for installation. You're ready to use the final `config.plist` from the `Envy repo`

```bash
cd ~/Projects/envy.git
./mount_efi.sh
cp config.plist /Volumes/EFI/EFI/Clover/config.plist
```

## Configure SMBIOS

After copying the `config.plist` from the repo to `EFI/Clover/config.plist`, you should customise the `SMBIOS` so you have a unique serial. You can use `Clover Configurator` to do this \(use google to find/download it\). **DO NOT use** `Clover Configurator` to edit your actual `config.plist`. Instead edit a _dummy_ `config.plist` to create the `SMBIOS` data and then use copy/paste with a plist editor \(I use Xcode\) to copy the `SMBIOS` section into my active `config.plist`. `Clover Configurator` is too buggy and cannot be trusted with edits to your real `config.plist`. This guide uses `MacBookPro11,1`. Do not use any other model identifier.

The detailed guide to correctly configure is [here](https://www.tonymacx86.com/threads/guide-how-to-configure-your-systems-smbios-correctly.198155/).

