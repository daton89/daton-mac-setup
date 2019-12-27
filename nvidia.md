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

