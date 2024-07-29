# Build Environment


Below is the minimum setup required of C/C++ development. The same is required for Kernel development as well.


### Alpine Linux

Install Alpine Linux and update/install packages.

```bash
apk update
apk add coreutils diffutils findutils binutils build-base util-linux
apk add bash grep bison gawk m4 sed texinfo xz shadow
apk add bc file gzip man-db ncurses procps psmisc tar zlib
apk add perl python3 wget
apk add flex git ncurses-dev elfutils-dev
apk add virtualbox-guest-additions
```



### Ubuntu Linux

Install Ubuntu Linux and update/install packages.

```bash
apt update && apt upgrade
apt install build-essential
apt install binutils coreutils diffutils findutils util-linux xz-utils util-linux
apt install bison gawk m4 python3 texinfo vim nano wget
apt install flex expect dejagnu llvm libisl23
apt install gettext bash bc file grep gzip man-db procps psmisc sed tar perl
apt install zlib1g libncurses6 libncursesw6 libdevmapper-dev
apt install libfreetype6-dev libfontconfig1-dev libfuse2
apt install libssl-dev
apt install libelf-dev
apt install liblzma-dev fuse
```