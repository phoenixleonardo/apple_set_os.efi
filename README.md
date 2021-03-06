# apple_set_os.efi
Tiny EFI program for unlocking the Intel IGD on the Macbook Pro 11,3 for Linux and Windows.  
It has been made to be easily chainloaded by unmodified EFI bootloader like Grub, rEFInd etc.

The Macbook Pro 11,3 model's EFI is switching off the Intel GPU if you boot anything but Mac OS X.  
So a little trick by faking the OS identifiction is required to make all hardware accessible.

All credits belong to [Andreas Heider](https://github.com/ah-) who originally discovered this hack:  
https://lists.gnu.org/archive/html/grub-devel/2013-12/msg00442.html

## Usage:
Copy the apple_set_os.efi binary (download it from [releases](https://github.com/0xbb/apple_set_os.efi/releases)) to EFI System Partition (ESP) :
```
mkdir /boot/efi/EFI/custom
cp apple_set_os.efi /boot/efi/EFI/custom
```
[rEFInd](http://www.rodsbooks.com/refind/) should automatically show a new icon for apple_set_os.efi.

Grub can be configured to start apple_set_os.efi automatically by adding the following lines to  ``/etc/grub.d/40_custom``:
```
search --no-floppy --set=root --label EFI
chainloader (${root})/EFI/custom/apple_set_os.efi
boot
```

## Build:
Tested on Debian Jessie 8.0:
```
apt-get install gnu-efi
git clone https://github.com/0xbb/apple_set_os.efi
cd apple_set_os.efi
make
```
## Build via docker
```bash
docker build -t apple_set_os . && docker run --rm -it -v $(pwd):/build apple_set_os
```


