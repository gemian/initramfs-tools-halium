# initramfs-tools-halium

Hooks and configuration to build a Halium initramfs

## Build an initramfs image

Install this package then create a new ramdisk.
```
sudo apt install initramfs-tools-halium

mkdir out
update-initramfs -tc -kgemini-arm64 -v -d ./out
```