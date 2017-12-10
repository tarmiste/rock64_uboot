# rock64_uboot 

Build u-boot for the ROCK64

This repository contains scripts, notes and other files that may be 
useful in the building of u-boot for the ROCK64 board.

Scripts in this repository are based on ROCK64 system image
build scripts (linux-build 0.5.10) created by ayufan (and maybe 
others as well).   This repository is intended to aide those who
wish to experiment specifically with uboot for the ROCK64.

This script has been tested only with SD cards on the ROCK64.  It is
untested and unknown whether or not it will work for updating 
uboot on eMMC cards.



Prerequisites:

x86_64 Linux host with arm64 cross compiler.  The scripts in this
repository were developed on a Centos 7 machine with a cross compiler 
built by crosstool-ng (using aarch64-unknown-linux-gnu target).


Setup:

Modify the setenv file as needed to use the desired cross compile 
tools on your host.

If building using git repositories of rkbin and/or u-boot is 
desired, then uncomment the appropriate "git clone" lines in the
buildimgs file.

Otherwise create the rkbin and u-boot trees that are to be used
during the build.  Tarballs of working snapshots of rkbin and 
u-boot trees are provided for reference.

If manual configuration of u-boot is desired, uncomment the 
"#make menuconfig" line in the buildimgs script.   Otherise, 
u-boot will be built using the default configuration for the
rock64 board.


Building:

Run the buildimgs script:

./buildimgs


Results:

Results will be found in the directory out/u-boot.   Updating the
boot device with the uboot.img file from that directory 
will update the boards uboot image to the built version.  
The other files found in the out/u-boot directory are not 
needed to update uboot and can be ignored.

Before installing the uboot.img file, care should be taken to 
ensure that any crucial data on the ROCK64 system has been 
backed up.  Modifying the bootloader could potentially result in
a non-bootable board.  So, take whatever precautions are needed
to safeguard any important information that you have on your ROCK64
board before attempting to update uboot.

The uboot.img file should be copied to partition 4 of the sd card:

dd if=uboot.img of=/dev/mmcblk1p4
sync

At the next reboot, the new uboot image will be executed.
