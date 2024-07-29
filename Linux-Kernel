# Linux Kernel


### Reference
- [docs.kernel.org](https://docs.kernel.org/index.html)  
- [kernel.org](https://www.kernel.org/)  


### Download Source

Clone linux kernel code 
```bash

git clone --depth 1 https://github.com/torvalds/linux.git

```
OR

Download source code archive from `https://www.kernel.org/`
```bash

wget https://cdn.kernel.org/pub/linux/kernel/v6.x/linux-6.10.2.tar.xz

```

### Build From Source

Before building Linux kernel from source, one should ask few questions.

1. What is the architecture of the host system where kernel is being compiled?
2. What is the architecture of the target system where kernel will run?
3. Are you cross-compiling? From one architecture to another?
4. Have you installed all build dependencies on host system? (Most of them are mentioned at [current-minimal-requirements](https://docs.kernel.org/process/changes.html#current-minimal-requirements) )

Answer to these questions are important as if you are compiling for arm64 from x86_64 then you have to select options and define parameter to highlight that.

Go to Linux source directory and run below command to understand all options for build.

```bash
# To check option for make
make --help

# To check Kernel build options
make help | less

```

> Kernel build default uses `gcc` if you want to use LLVM please refer [LLVM](https://docs.kernel.org/kbuild/llvm.html)

Always try to use `O=` (capital O) option in `make` command. This option will keep your source directory clean and will generate files in the given location. Another benefit of using this option is that you can generate/configure multiple configuration to compile kernel in parallel. This option is same as `KBUILD_OUTPUT` environment variable mentioned at [environment-variables](https://docs.kernel.org/kbuild/kbuild.html#kbuild-output).

```bash
# https://www.kernel.org/doc/html/latest/kbuild/kconfig.html#menuconfig

make O=/home/name/build/tmp_kernel menuconfig

```

It's always a good idea to start configuration with default config. In below case if you are building on **32bit** system then `i386_defconfig` and `defconfig` will generate same configuration. Similarly if you are building on **64bit** system then `x86_64_defconfig` and `defconfig` will generate same configuration. Please refer "Architecture-specific targets" segment in `make help` output.

```bash 

make O=/root/build/tmp_kernel i386_defconfig              # Build for i386
make O=/root/build/tmp_kernel x86_64_defconfig            # Build for x86_64

# OR

make O=/root/build/tmp_kernel defconfig

```

`make` provides multiple editors to select config parameters `nconfig`, `menuconfig` etc.
Please refer the link provided in code segment.

```bash 
# https://www.kernel.org/doc/html/latest/kbuild/kconfig.html#nconfig
make O=/root/build/tmp_kernel NCONFIG_MODE=single_menu nconfig

# https://www.kernel.org/doc/html/latest/kbuild/kconfig.html#menuconfig
make O=/root/build/tmp_kernel MENUCONFIG_COLOR=classic menuconfig

```

```bash 
# https://www.kernel.org/doc/html/latest/kbuild/kbuild.html#environment-variables

### If you are cross compiling for "arm64" as target use below environment-variables
make O=/root/build/tmp_kernel_arm ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- menuconfig

### If you are cross compiling for "x86_64" as target use below environment-variables
make O=/root/build/tmp_kernel_x86 ARCH=x86_64 CROSS_COMPILE=x86_64-linux-gnu- menuconfig

```

```bash
### Run build in parallel using SMP
make -j16

# OR

### Use "nproc" to define available processor on your host system.
make -j$(nproc)

# OR

### Use below syntax to capture make command output to log file.
( make -j8 O=/root/build/tmp_kernel 2>&1 | tee /root/build/kernel_allmod/my_make_log.log && exit $PIPESTATUS )

```


```bash
### At below location kernel image will be placed after build.
ls -lrt arch/x86/boot/bzImage
```

If you are installing kernel and modules to non-default location then use below environment variable. in below example:
1. `/mnt/usb` is where target system `/` is mounted thus modules will be installed under this path in `lib` directory.
2. `/mnt/usb/boot` is absolute path of boot folder where kernel will be installed.

```bash

INSTALL_MOD_PATH=/mnt/usb \
INSTALL_PATH=/mnt/usb/boot \
make O=/root/build/kernel modules_install install

```