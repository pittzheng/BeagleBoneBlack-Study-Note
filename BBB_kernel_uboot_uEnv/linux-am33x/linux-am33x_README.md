http://arago-project.org/git/projects/?p=linux-am33x.git;a=summary
git clone git://arago-project.org/git/projects/linux-am33x.git

source toolchaing path
cd linux-am33x


Enable "CONFIG_EXT4_FS=y" in arch/arm/configs/am335x_evm_defconfig
Enable "CONFIG_DEVTMPFS=y" in arch/arm/configs/am335x_evm_defconfig

make ARCH=arm CROSS_COMPILE=arm-arago-linux-gnueabi- am335x_evm_defconfig
make ARCH=arm CROSS_COMPILE=arm-arago-linux-gnueabi- menuconfig
"Enable Device Drivers->Generic Driver Options->Automount devtmpfs at /dev, after the kernel mounted the rootfs,
then CONFIG_DEVTMPFS_MOUNT=y will be enabled in .config"

make ARCH=arm CROSS_COMPILE=arm-arago-linux-gnueabi- uImage
make ARCH=arm CROSS_COMPILE=arm-arago-linux-gnueabi- distclean
