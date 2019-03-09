# initramfs-tools-halium

Hooks and configuration to build a Halium initramfs

## Build an initramfs image

Install this package to create a new ramdisk.
```
sudo apt install initramfs-tools-halium
```
The post install script does this for you:
```
sudo update-initramfs -tc -kgemini.cpio.gz -v -b /usr/share/kernel

```

## Build the boot image with the kernel

```
mkbootimg --kernel /usr/share/kernel/Image.gz-dtb --ramdisk /usr/share/kernel/initrd.img-gemini.cpio.gz --base 0x40080000 --second_offset 0x00e80000 --cmdline "bootopt=64S3,32N2,64N2 log_buf_len=4M" --kernel_offset 0x00000000 --ramdisk_offset 0x04f80000 --tags_offset 0x03f80000 --pagesize 2048 -o linux-boot.img
```
or
```
mkbootimg --kernel /usr/share/kernel/Image.gz-dtb --ramdisk /usr/share/kernel/initrd.img-gemini.cpio.gz --base 0x40080000 --second_offset 0x00e80000 --cmdline "bootopt=64S3,32N2,64N2 log_buf_len=4M stowaways_os=stretch" --kernel_offset 0x00000000 --ramdisk_offset 0x04f80000 --tags_offset 0x03f80000 --pagesize 2048 -o linux-boot-stretch.img
```
or
```
mkbootimg --kernel /usr/share/kernel/Image.gz-dtb --ramdisk /usr/share/kernel/initrd.img-gemini.cpio.gz --base 0x40080000 --second_offset 0x00e80000 --cmdline "bootopt=64S3,32N2,64N2 log_buf_len=4M root_lv=stretch" --kernel_offset 0x00000000 --ramdisk_offset 0x04f80000 --tags_offset 0x03f80000 --pagesize 2048 -o linux-boot-lvm-stretch.img
```

## Flash the kernel to one of your boot partitions
```
sudo dd if=linux-boot.img of=/dev/disk/by-partlabel/boot3
```
or
```
sudo dd if=linux-boot-stretch.img of=/dev/disk/by-partlabel/boot3
```
or
```
sudo dd if=linux-boot-lvm-stretch.img of=/dev/disk/by-partlabel/boot3
```