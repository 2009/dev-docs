# Macbook Specific Installation

Specific instructions on installing arch on a Macbook.

[MacBook - Arch Wiki][2]  
[MacBookPro11,x - Arch Wiki][3]  

## Prepartion

### Update macbook firmware

Updating the firmware for a Macbook can only be done 
through installing any system updates using the App Store.

### Partion the drive

If using a single drive, you will have to shrink the main 
partition and create a separate partition for arch.
This should be done with the mac disk utility, as it can
handle working with HFS volumes.

## Booting installation USB

Macbooks support booting using *UEFI*.
To boot a UEFI bootable USB, hold down the `Alt/Option`
key while the mac is booting. This display the bootable
USB, as well as any other bootable partitions (including
the Mac partition).

## Setting up the bootloader

Any bootloader that supports UEFI (e.g. Grub) can be installed to the
EFI system partion using the standar isntallation instruction.

This will replace the default mac bootloader, but the Mac partion will
still be bootable by holding the `Alt/Option` key during boot.

An alternative is to create a HFS+ boot partions as described by
[Using the native Apple bootloader with Grub][1].

[1]: https://wiki.archlinux.org/index.php/MacBook#Using_the_native_Apple_bootloader_with_GRUB
[2]: https://wiki.archlinux.org/index.php/MacBook
[3]: https://wiki.archlinux.org/index.php/MacBookPro11,x
