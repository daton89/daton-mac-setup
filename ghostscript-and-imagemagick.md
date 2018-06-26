# Ghostscript and Imagemagick

## Installation

We can use Homebrew: 

```bash
brew install ghostscript
```

Now before installing `Imagemagick` we should need:

```bash
brew install pkgconfig
```

If you need an older version of `Imagemagick` like the 6: 

```bash
brew install imagemagick@6 \
--with-fftw \
--with-fontconfig \
--with-ghostscript \
--with-hdri \
--with-liblqr \
--with-librsvg \
--with-libwmf \
--with-little-cms \
--with-little-cms2 \
--with-opencl \
--with-openexr \
--with-openjpeg \
--with-openmp \
--with-pango \
--with-perl \
--with-webp \
--with-x11
```

We'll see an output like this: 

```bash
==> Downloading 
Already downloaded: /Users/tony/Library/Caches/Homebrew/imagemagick@6-6.9.9-51.high_sierra.bottle.tar.gz

This formula is keg-only, which means it was not symlinked into /usr/local,
because this is an alternate version of another formula.

If you need to have this software first in your PATH run:
    echo 'export PATH="/usr/local/opt/imagemagick@6/bin:$PATH"' >> ~/.zshrc
```

So running `echo 'export PATH="/usr/local/opt/imagemagick@6/bin:$PATH"' >> ~/.zshrc` you will find convert in the path.

```bash
export PKG_CONFIG_PATH=/usr/local/opt/imagemagick@6/lib/pkgconfig
```

