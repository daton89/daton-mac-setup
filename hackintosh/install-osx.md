# Install OSX

## **Download macOS High Sierra**

The full operating system is a free download for anyone who has purchased Mac OS X Snow Leopard, Lion, or Mountain Lion or has a Mac preloaded with OS X Mavericks, Yosemite, El Capitan, or macOS Sierra. Download the Application from the Mac App Store using your Apple ID on any Mac or functional computer running OS X 10.7.5 or later.

1. Open **Mac App Store**
2. Log in with your Apple ID
3. Download **macOS High Sierra**

The Application **Install macOS High Sierra** will appear in /Applications.

## **Building the OS X installer**

This is the same mechanism you would use to create a USB installer for a real Mac.  
  
It is a single line, executed in Terminal:

```bash
# copy installer image
sudo "/Applications/Install macOS High Sierra.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install_osx --nointeraction
# Then change the name to be less unwieldy...
sudo diskutil rename "Install macOS High Sierra" install_osx
```



## **Booting the Installer**

After you create you USB, it is ready to go... Read post \#2 for more details on using the USB.  
  
Generally, you will need to use a special button to turn the laptop on or press some special keys to access the boot menu, where you can choose to boot the USB.

Note that you may see it listed twice \(depending on setting of legacy boot\). Choose the listing that is UEFI or legacy depending on what type of USB you opted for. Of course, if your computer doesn't have UEFI, you'll see no such listing and will boot the device in legacy mode in order to boot Clover.  
  
You can press the spacebar in Clover to select various options. It is a good idea to use this to boot verbose \(the config.plist files I provide do not have verbose turned on by default\). In verbose mode you have a better idea of the booting process and get better information in the case of a crash.

## **Install macOS High Sierra**

You're almost done! All you need to do is boot from the USB drive and install! For best results, insert the USB in a USB 2.0 port.

1. Turn on the computer
2. Press the hotkey to choose boot device \(F12 for Gigabyte motherboards, F8 for ASUS motherboards, F11 for ASrock motherboards\)
3. Choose **USB** 
4. At Clover boot screen, choose **Boot OS X Install from Install macOS High Sierra** 
5. When you arrive at the Installer, choose language.
6. For a new installation of macOS, you MUST erase and format the destination drive according to the following steps before continuing.
   1. In the top menu bar choose **Utilities**, and open **Disk Utility**
   2. Highlight your target drive for the High Sierra installation in left column.
   3. Click **Erase** button
   4. For **Name:** type **High Sierra** \(You can rename it later\)
   5. For **Format:** choose **Mac OS Extended \(Journaled\)**
   6. Click **Erase**
   7. Close **Disk Utility**
7. When the installer asks you where to install, choose **High Sierra**
8. Upon completion, the system will automatically restart.
9. Press the hotkey to choose boot device \(F12 for Gigabyte motherboards, F8 for ASUS motherboards, F11 for ASrock motherboards\)
10. Choose **USB**
11. At the Boot Screen, choose **High Sierra**
12. Complete macOS installation. The system will automatically reboot.

##  **Clover Resources**

It is a good idea to become familiar with the software you are using and read the documentation.  
  
Clover wiki: [http://clover-wiki.zetam.org/Home](http://clover-wiki.zetam.org/Home)  
  
Clover instructions thread: [http://www.insanelymac.com/forum/topic/282787-clover-v2-instructions/](http://www.insanelymac.com/forum/topic/282787-clover-v2-instructions/)  
  
Clover discussion: [http://www.insanelymac.com/forum/topic/284656-clover-general-discussion/](http://www.insanelymac.com/forum/topic/284656-clover-general-discussion/)  
  
Clover patch/bug reports: [http://www.insanelymac.com/forum/topic/306156-clover-bugissue-report-and-patch/](http://www.insanelymac.com/forum/topic/306156-clover-bugissue-report-and-patch/)  
  
Clover changes: [http://www.insanelymac.com/forum/topic/304530-clover-change-explanations/](http://www.insanelymac.com/forum/topic/304530-clover-change-explanations/)



