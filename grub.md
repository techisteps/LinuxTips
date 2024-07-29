# Grub


### Grub Install

`/mnt/usb` is the mount-point where I have mounted guest `/`, thus mentioned it in `--prefix` option

```bash
#Grub install


wget https://ftp.gnu.org/gnu/grub/grub-2.12.tar.xz

tar -xvf grub-2.12.tar.xz && cd grub-2.12

./configure --prefix=/mnt/usb/usr          \
            --sysconfdir=/etc      \
            --disable-efiemu       \
            --disable-werror

( make -j4 2>&1 | tee _my_make_j4.log && exit $PIPESTATUS )

( make install 2>&1 | tee _my_make_install.log && exit $PIPESTATUS )

mv -v /etc/bash_completion.d/grub /usr/share/bash-completion/completions

```


### Grub command line



### Grub config file



### Write grub loader