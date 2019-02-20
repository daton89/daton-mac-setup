# Keyboard Mapping

## How to personalise keyboard's buttons

The mapping for Control, Option, and Command are according to the physical layout of the keys on an actual MacBook keyboard, not the labels on the keys. Control=Control, Windows=Option, and Alt=Command. If you want a more PC friendly keyboard layout, use `Karabiner` \(formerly KeyRemap4MacBook\). You can find it [here](https://pqrs.org/osx/karabiner/).

{% hint style="info" %}
You should find this software with `Homebrew`: `brew cask install karabiner`
{% endhint %}

The function of Fn+F1..F12 and F1..F12 can be changed in SysPrefs-&gt;Keyboard.

Personally i only changed the **right ctrl** to be mapped to the **right alt**.

### Troubleshooting 

If you get issues with keyboard mapping and you decide to reset it:   
  
`sudo rm /Library/Preferences/com.apple.keyboardtype.plist`  
  
and then reboot. After reboot the Assistant asks to verify the layout, bingo !



