---
Title: Create a Bootable USB Device from an ISO in Mac OS X
---

# Create a Bootable USB Device from an ISO in Mac OS X

## Convert from ISO to UDFI

```
$ hdiutil convert -format UDRW -o output.dmg input.iso
```

## Find Your USB Device

```
$ diskutil list

/dev/disk5 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *62.7 GB    disk5
   1:                        EFI EFI                     209.7 MB   disk5s1
   2:                 Apple_APFS Container disk6         62.5 GB    disk5s2

/dev/disk6 (synthesized):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      APFS Container Scheme -                      +62.5 GB    disk6
                                 Physical Store disk5s2
   1:                APFS Volume Flashy                  913.4 KB   disk6s1
```

## Delete the APFS Container

```
$ diskutil apfs deleteContainer disk5s2

Started APFS operation on disk5s2
Deleting APFS Container with all of its APFS Volumes
Assuming that the APFS Container is damaged; any additional Physical Store disks which define the Container might not be found for reformatting and might need to be handled separately
Deleting Container
Switching content types
Reformatting former APFS disk
Initialized /dev/rdisk5s2 as a 58 GB case-insensitive HFS Plus volume with a 8192k journal
Mounting disk
Finished APFS operation on disk5s2
```
Your APFS container will be deleted, and a HFS+ partition created on our USB device.

```
$ diskutil list

/dev/disk5 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *62.7 GB    disk5
   1:                        EFI EFI                     209.7 MB   disk5s1
   2:                  Apple_HFS Untitled                62.4 GB    disk5s2
```

## Wipe the USB device

```
$ diskutil partitionDisk /dev/disk5 "Free Space" "unused" "100%"

Started partitioning on disk5
Unmounting disk
Creating the partition map
Waiting for partitions to activate
Finished partitioning on disk5
/dev/disk5 (external, physical):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                        *62.7 GB    disk5
   1:                        EFI EFI                     209.7 MB   disk5s1
```

## Copy the Image to Your device

```
$ sudo dd if=centos.dmg of=/dev/disk5 bs=1m
Password:

791+1 records in
791+1 records out
829872128 bytes transferred in 25.853054 secs (32099578 bytes/sec)
```

Mac OS will attempt to mount the device afterwards but a dialog will pop
if you copied an image that uses a filesystem that Mac OS can't read. Simply
opt to eject the device and you're done!

## References
* <https://blog.tinned-software.net/create-bootable-usb-stick-from-iso-in-mac-os-x/>
* <http://endlessgeek.com/2014/02/mac-osx-how-to-burn-an-iso-image-to-a-usb-key/>
* <https://unix.stackexchange.com/questions/114984/how-to-create-a-bootable-linux-installation-usb-from-an-iso-in-os-x/114987#114987>
* <https://www.macobserver.com/tips/deep-dive/macos-sierra-delete-apfs-partition-right-way/>
