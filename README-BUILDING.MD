TF101-GNU-kernel
================

## Preparation
1. Cross-compiler Tool
Since this is a pretty old kernel code, we can't compile using latest arm-GCC.
We need to use very specific GCC version. The easiest is to get pre-built version from here:
```
https://launchpadlibrarian.net/151487636/gcc-arm-none-eabi-4_7-2013q3-20130916-linux.tar.bz2
```

## Building
1. Use TF101 config as kernel build config
```
make tf101-linux_defconfig
```

2. Setup environment variable
```
# Tell build system we're compiling for ARM
export ARCH=arm
# Specify tools to do cross-compilation, because we're building for ARM using X86-64
export CROSS_COMPILE=/path/to/downloaded/gcc-arm-none-eabi-4_7-2013q3/bin/arm-none-eabi-

```

2. Build the Kernel
```
# Make sure toolchain for cross-compilation is already installed, as we're building
# on X86 host for ARM machine
make -j4 ```

3. Build modules
```
# Build kernel modules
make ARCH=arm modules
```

4. Install modules
```
# TODO: This is tricky because this should be part of initramfs, but we're
        using one from postmarketos, I guess for debugging purposes, easiest
        would be to compile needed modules as built-in. Then only when
        we try to upstream to postmarketos, we build them as modules
```
