Buildroot for Olimex Olinuxino

Steps for making an SDCard

1. Use fdisk or similar tool to create two partitions. The first
   should be type 53 (OnTrack DM6 Aux3) and be 16MB. The second
   partition should be type 83 (Linux) and large enough for the
   rootfs.

2. Create the raw image for the first partition. Per the i.MX23
   EVK Linux User's Guide, this is 2048 bytes of 0s and then 
   the bootstream.

dd if=/dev/zero of=sd_mmc_bootstream.raw bs=512 count=4
dd if=output/images/imx23_olinuxino_dev_linux.sb of=sd_mmc_bootstream.raw ibs=512 seek=4 conv=sync,notrunc

3. Write the raw bootstream image to the SDCard.

sudo dd if=sd_mmc_bootstream.raw of=/dev/sdX1

4. Write the rootfs image to the SDCard

sudo dd if=output/images/rootfs.ext2 of=/dev/sdX2

