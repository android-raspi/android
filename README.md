## Submitting Patches to Raspberry Pi ##
------------------
You can send patches by using Pull Requests for now.

## Getting Started ##
---------------
To get started with Android for Raspberry Pi 3, you'll need to get
familiar with [Git and Repo](https://source.android.com/source/using-repo.html).

To initialize your local repository using the Android/Raspberry trees, use a command like this:

    $ repo init -u git://github.com/android-raspi/android.git -b aosp-7.1

Establishing a Build Environment

    https://source.android.com/source/initializing.html

Also install python mako module and schedtool

    $ sudo apt-get install python-mako schedtool

Then to sync up:

    $ repo sync

Then to build:

    $ cd <source-dir>
    $ source build/envsetup.sh
    $ brunch rpi3

Building only kernel:

    $ cd <source-dir>
    $ source build/envsetup.sh
    $ bib rpi3
    $ mka bootimage

## Prepare SD Card ##
---------------
Partitions of the card should be set-up as following:

    * p1 64MB   for /BOOT   : Do fdisk : W95 FAT32(LBA) & Bootable, mkfs.vfat
    * p2 1GB    for /system : Do fdisk, new primary partition
    * p3 512MB  for /cache  : Do fdisk, mkfs.ext4
    * p4 remain for /data   : Do fdisk, mkfs.ex4

    Set volume label for each partition - system, cache, userdata
    use -L option of mkfs.ext4, e2label command, or -n option of mkfs.vfat

## Flash AOSP image to your device ##
---------------

    $ cd <source-dir>
    $ cd out/target/product/rpi3
    $ sudo dd if=system.img of=/dev/<p2> bs=1M
  
## Boot partition, kernel & ramdisk ##
---------------
Copy files:

    - First find the mount point for P1 (BOOT)

    $ cd <source-dir>
    $ cp -Rf out/target/product/rpi3/rpi-boot/* [P1 mount point]

## HDMI_MODE ##
---------------
If DVI monitor does not work, try to change config.txt (in device/broadcom/rpi[N]):

    * hdmi_group=2
    * hdmi_mode=85

## Put LeanbackLauncher ##
---------------

    https://github.com/peyo-hd/device_brcm_rpi3/wiki#how-to-apply-android-tv-leanback-launcher

## Community ##
---------------
Forum

    * https://groups.google.com/forum/#!forum/android-rpi

## Graphics HAL ##
---------------
Graphics HAL of this build is Android port of Mesa with VC4 GPU

    * https://dri.freedesktop.org/wiki/VC4
