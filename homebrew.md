# Homebrew

[Homebrew](https://brew.sh/) calls itself _The missing package manager for macOS_ and is an essential tool for any developer.

### Installation {#installation}

An important dependency before Homebrew can run is the **Command Line Tools** for **Xcode**. These include compilers that will allow you to build things from source, if you are missing this it's available through the App Store &gt; Updates.

To install Homebrew paste the following command in your terminal, hit **Enter**, and follow the steps on the screen:

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

One thing we need to do is tell the system to use programs installed by Hombrew \(in `/usr/local/bin`\) rather than the OS default if it exists. We do this by adding `/usr/local/bin` to your `$PATH`environment variable \(if you're using oh my zsh you should use `.zshrc` instead of `.bash_profile`\):

```bash
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile
```

Alternatively, we can also insert `/usr/local/bin` to the first line of `/private/etc/paths` and reboot the Mac to change global paths loading order. Admin password may be required if you modify the file.

To be able to use `brew` you need to start a new terminal session. Do this by opening a new terminal tab with **Cmd+T** \(you should also close the old one\), then run the following command to make sure everything is working:

```bash
brew doctor
```



## Using Homebrew {#using-homebrew}

To install a package \(or **Formula** in Homebrew vocabulary\) simply type:

```bash
brew install <formula>
```

To update Homebrew's directory of formulae, run:

```bash
brew update
```

**Note**: I've seen that command fail sometimes because of a bug. If that ever happens, run the following \(when you have Git installed\):

```bash
cd /usr/local/Homebrew/
git fetch origin
git reset --hard origin/master
```

To see if any of your packages need to be updated:

```bash
brew outdated
```

To update a package:

```bash
brew upgrade <formula>
```

Homebrew keeps older versions of packages installed, in case you want to roll back. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

```bash
brew cleanup
```

To see what you have installed \(with their version numbers\):

```bash
brew list --versions
```



## Homebrew Cask {#homebrew-cask}

[Homebrew-Cask](https://caskroom.github.io/) extends Homebrew and allows you to install large binary files via a command-line tool. Examples of these files is Google Chrome, Dropbox, VLC and Spectacle.

### Installation {#installation}

As of December 2015, Cask comes installed with Homebrew, if you have not installed Homebrew see the [Homebrew section](http://sourabhbajaj.com/mac-setup/mac-setup/Homebrew/README.html).

### Search {#search}

To see if an app is available on Cask you can search on the [official Cask website](https://caskroom.github.io/). You can also search using the following command:

```bash
brew cask search <package>
```

### Quick Look plugins {#quick-look-plugins}

These plugins adds support for the corresponding file type to Mac Quick Look \(In Finder, mark a file and press Space to start Quick Look\). The plugins includes features like syntax highlighting, markdown rendering, preview of JSON, patch files, csv, zip files and more.

```bash
brew cask install \
    qlcolorcode \
    qlstephen \
    qlmarkdown \
    quicklook-json \
    qlprettypatch \
    quicklook-csv \
    betterzipql \
    webpquicklook \
    suspicious-package
```

### App Suggestions {#app-suggestions}

Here are some useful apps that are available on Cask.

```bash
brew cask install \
    alfred \
    android-file-transfer \
    asepsis \
    appcleaner \
    caffeine \
    cheatsheet \
    docker \
    dropbox \
    google-chrome \
    google-drive \
    google-hangouts \
    flux \
    pdftk \
    spectacle \
    superduper \
    totalfinder \
    transmission \
    visual-studio-code \
    vlc
```

