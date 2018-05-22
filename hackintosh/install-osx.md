# Install OSX

**STEP 1: Download macOS High Sierra**  
The full operating system is a free download for anyone who has purchased Mac OS X Snow Leopard, Lion, or Mountain Lion or has a Mac preloaded with OS X Mavericks, Yosemite, El Capitan, or macOS Sierra. Download the Application from the Mac App Store using your Apple ID on any Mac or functional computer running OS X 10.7.5 or later.  
  
1. Open **Mac App Store**  
2. Log in with your Apple ID  
3. Download **macOS High Sierra**  
  
The Application **Install macOS High Sierra** will appear in /Applications.

  
**Building the OS X installer**  
  
There are two ways to copy the OS X installer to USB:  
- 'createinstallmedia' method \(recommended\)  
- BaseBinaries clone method \(use when 'createinstallmedia' is not available\)  
  
  
**createinstallmedia method**  
  
This is the same mechanism you would use to create a USB installer for a real Mac.  
  
It is a single line, executed in Terminal:  
Code \(Text\):  
\# copy installer image  
sudo "/Applications/Install macOS High Sierra.app/Contents/Resources/createinstallmedia" --volume  /Volumes/install\_osx --nointeraction  
 Then change the name to be less unwieldy...  
Code \(Text\):  
\# rename  
sudo diskutil rename "Install macOS High Sierra" install\_osx  
 

