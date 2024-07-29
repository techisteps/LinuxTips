# OpenRC

### OpenRC install

> `/mnt/usb` is the mount-point, where I have mounted guest root `/`, thus option `--destdir=/mnt/usb/` is point to the location where we want to install the package.

```bash

git clone https://github.com/OpenRC/openrc.git

cd openrc/

ROOTPREFIX=/mnt/usb meson setup --wipe builddir

cd builddir/

#ROOTPREFIX=/mnt/usb meson compile
( ROOTPREFIX=/mnt/usb meson compile 2>&1 | tee _my_meson_compile.log && exit $PIPESTATUS )

#ROOTPREFIX=/mnt/usb meson install --destdir=/mnt/usb/
( ROOTPREFIX=/mnt/usb meson install --destdir=/mnt/usb/ 2>&1 | tee _my_meson_install.log && exit $PIPESTATUS )
```


### Docs
[README](https://github.com/OpenRC/openrc/blob/master/README.md)  
[user-guide](https://github.com/OpenRC/openrc/blob/master/user-guide.md)  
Check other guides in git repository **https://github.com/OpenRC/openrc.git**


### Reference
https://wiki.gentoo.org/wiki/OpenRC  
https://wiki.gentoo.org/wiki/Handbook:AMD64/Working/Initscripts  

### Cheat Sheet
https://gist.github.com/unrooted/d70583fd4eceb3c818d65a83bf2c6acf  
https://cheatography.com/misterrabinhalder/cheat-sheets/openrc/  
