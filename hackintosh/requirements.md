# Requirements

#### Computer Specifics

* HP Envy 15  J104SL
* i7-4700MQ @2.4Ghz, 12GB RAM
* HM87 chipset
* HD4600 graphics \(1080p panel\)
* BCM4352 ac WiFi
* RTL8111/8168/8411



#### **BIOS settings**

To start, set BIOS to Windows 8 defaults.  
  
Then insure:

* UEFI boot is enabled
* secure boot is disabled
* enable Legacy Boot \(but UEFI first\) and you may experience less boot time glitches

  
Note: The DSDT/SSDT patching script will automatically disable the discrete Nvidia card if you have it enabled in BIOS. It is best, therefore to keep it enabled in BIOS so you can still use it on Windows, but have DSDT/SSDT patched properly for OS X.  


