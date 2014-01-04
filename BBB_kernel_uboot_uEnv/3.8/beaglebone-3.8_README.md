http://circuitco.com/support/index.php?title=BeagleBoneBlack#Angstrom

https://github.com/beagleboard/kernel/tree/3.8

kernel
======

Kernel for the beagleboard.org boards

usage
======

1. git clone https://github.com/beagleboard/kernel.git

#beaglebone-3.8 patchset:

2. git checkout origin/3.8 -b 3.8
3. ./patch.sh
4. Get am335x-pm-firmware.bin from http://arago-project.org/git/projects/?p=am33x-cm3.git;a=tree;f=bin and copy it to kernel/firmware

5. cd kernel
6. cp ../configs/beaglebone .config

# toolchain setup
Note:
    This kernel can not be built with toolchain from TI
    must use the toolchain from:
    wget -c https://launchpad.net/linaro-toolchain-binaries/trunk/2013.07/+download/gcc-linaro-arm-linux-gnueabihf-4.8-2013.07-1_linux.tar.xz
    tar xJf gcc-linaro-arm-linux-gnueabihf-4.8-2013.07-1_linux.tar.xz
    export CC=`pwd`/gcc-linaro-arm-linux-gnueabihf-4.8-2013.07-1_linux/bin/arm-linux-gnueabihf-
    
    path_arm-linux-gnueabihf-.sh:

    #!/bin/sh

    export PATH=/home/peiqzhen/Projects/beaglebone_linux_distribution/Toolchain/gcc-linaro-arm-linux-gnueabihf-4.8-2013.07-1_linux/bin:${PATH}
7. source path_arm-linux-gnueabihf-.sh
# build kernel
8. make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- uImage dtbs

copy over uImage and am335x-bone.dtb to /boot

uEnv.txt for the angstrom u-boot 2012.10:

devtree=/boot/am335x-bone.dtb
dtboot=run mmcargs; ext2load mmc ${mmcdev}:2 ${kloadaddr} ${bootfile} ; ext2load mmc ${mmcdev}:2 ${fdtaddr} ${devtree} ; bootm ${kloadaddr} - ${fdtaddr}
uenvcmd=run dtboot
optargs=consoleblank=0
uEnv.txt for vanilla u-boot 2012.10:

devtree=/boot/am335x-bone.dtb
dtboot=run mmcargs; ext2load mmc ${mmcdev}:2 ${loadaddr} ${bootfile} ; ext2load mmc ${mmcdev}:2 ${fdtaddr} ${devtree} ; bootm ${loadaddr} - ${fdtaddr}
uenvcmd=run dtboot
optargs=consoleblank=0


