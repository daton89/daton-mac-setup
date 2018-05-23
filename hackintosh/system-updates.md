# System Updates

First step should be to update to the latest repository.

To do so:

```bash
cd ~/Projects/envy.git
git stash
git pull 
make
make install
./download.sh
./install_downloads.sh
```

Also update Clover to the latest using the Clover installer. Be sure to fix `EFI/Clover/kexts`, so that only `EFI/Clover/kexts/Other` is existing. All version specific directories under `EFI/Clover/kexts` should be removed.  
  
Also update `config.plist` at `EFI/Clover/config.plist` to the latest content from the repo. Be sure to retain your own `SMBIOS` data at `config.plist/SMBIOS`.  
  
Now you can update via the App Store. Just boot the `installer/updater` upon restart.  
  
After updating, run `./install_downloads.sh` again:

```bash
cd ~/Projects/envy.git
./install_downloads.sh
```

