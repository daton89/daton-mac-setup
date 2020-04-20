# NVIDIA

Check the NVIDIA Graphic Card: 

```text
lspci -k | grep -A 2 -E "(VGA|3D)"

00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 630 (Mobile)
	DeviceName:  Onboard IGD
	Subsystem: Dell Device 087c
--
01:00.0 3D controller: NVIDIA Corporation GP107M [GeForce GTX 1050 Ti Mobile] (rev a1)
	Subsystem: Dell Device 087c
	Kernel driver in use: nouveau
```

If we are using a recent NVIDIA Graphic Card we can install the most recent driver: 

```text
sudo dnf install akmod-nvidia
```

Then check for any updates:

```text
sudo dnf update -y
```

Now when we restart the laptop check:

```text
lspci -k | grep -A 2 -E "(VGA|3D)"

00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 630 (Mobile)
	DeviceName:  Onboard IGD
	Subsystem: Dell Device 087c
--
01:00.0 3D controller: NVIDIA Corporation GP107M [GeForce GTX 1050 Ti Mobile] (rev a1)
	Subsystem: Dell Device 087c
	Kernel driver in use: nvidia
```

This method was the most clean, and I found it on the [official rpmfusion docs](https://rpmfusion.org/Howto/NVIDIA#Current_GeForce.2FQuadro.2FTesla).

If you have problems with sleep and hybernations I check if you have this configuration in the `/etc/default/grub` file:

```text
GRUB_TIMEOUT=5
GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX="nouveau.blacklist=1 systemd.unified_cgroup_hierarchy=0 rd.driver.blacklist=nouveau modprobe.blacklist=nouveau nvidia-drm.modeset=1 resume=/dev/mapper/fedora-swap rd.lvm.lv=fedora/root rd.lvm.lv=fedora/swap rhgb quiet"
GRUB_DISABLE_RECOVERY="true"
GRUB_ENABLE_BLSCFG=true

```

Adding the option `nouveau.blacklist=1` solved my problem.

Then finally run this command to update the grub: 

```text
sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg
```

