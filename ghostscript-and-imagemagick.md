# Ghostscript and Imagemagick

## Installation

We can use Homebrew: 

```bash
brew install ghostscript
brew install pkgconfig
brew install imagemagick
```

If you need an older version of Imagemagick like the 6: 

```bash
brew install imagemagick@6
```

We'll see an output like this: 

```bash
==> Downloading https://homebrew.bintray.com/bottles/imagemagick@6-6.9.9-51.high_sierra.bottle.tar.gz
Already downloaded: /Users/tony/Library/Caches/Homebrew/imagemagick@6-6.9.9-51.high_sierra.bottle.tar.gz

This formula is keg-only, which means it was not symlinked into /usr/local,
because this is an alternate version of another formula.

If you need to have this software first in your PATH run:
    echo 'export PATH="/usr/local/opt/imagemagick@6/bin:$PATH"' >> ~/.zshrc
```

So running `echo 'export PATH="/usr/local/opt/imagemagick@6/bin:$PATH"' >> ~/.zshrc` you will find convert in teh pahtt

