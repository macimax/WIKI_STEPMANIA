If you run StepMania on Linux, you may want to create static mount points for USB-based profiles.  Doing so will allow you associate a USB port on your PC with a specific player's memorycard slot, as is common on arcade cabinets.

The process is **moderately technical** and assumes you are comfortable editing system files in Linux via the command line.  If you are not comfortable with this, do not proceed.

---

### Step 1 - Finding the USB port _by-path_

Since disk names `sda`, `sdb`, and so on are not deterministic, depending on the order in which devices are plugged, we can't use them to reliably identify players.  Fortunately, Linux allows us to select a disk "by path," which amounts to defining a specific USB _port_ as a given drive, which is typically what we want for USB profiles.

To find the correct device path, plug a single USB drive into the port you with to associate with PLAYER_1, then run the following command:
```bash
ls -l /dev/disk/by-path
```

This should give you output that looks something like:
```bash
/dev/disk/by-path/:
total 0
lrwxrwxrwx 1 root root  9 Jun  2 00:05 pci-0000:00:14.0-usb-0:10:1.0-scsi-0:0:0:0 -> ../../sdb
lrwxrwxrwx 1 root root 10 Jun  2 00:05 pci-0000:00:14.0-usb-0:10:1.0-scsi-0:0:0:0-part1 -> ../../sdb1
```

Copy this output to a text editor and repeat command with the USB stick plugged into the USB port you wish to associate with PLAYER_2.  Copy that output as well.

### Step 2 - Create _fstab_ Entries

You will use part of the output from the previous step to create entries in `/etc/fstab`, the file which associates specific devices (in this case a USB port _by-path_) with named mount points that can be passed to StepMania. 

The resulting _fstab_ entries will look like:

```
/dev/disk/by-path/pci-0000:00:14.0-usb-0:10:1.0-scsi-0:0:0:0-part1 	/mnt/player1 auto rw,user,noauto,sync,exec 0 0
/dev/disk/by-path/pci-0000:00:14.0-usb-0:10:1.0-scsi-0:0:0:0 		/mnt/player1 auto rw,user,noauto,sync,exec 0 0
/dev/disk/by-path/pci-0000:00:14.0-usb-0:4:1.0-scsi-0:0:0:0-part1 	/mnt/player2 auto rw,user,noauto,sync,exec 0 0
/dev/disk/by-path/pci-0000:00:14.0-usb-0:4:1.0-scsi-0:0:0:0 		/mnt/player2 auto rw,user,noauto,sync,exec 0 0
```

Note that depending on your Linux distribution, you may want/need to create your named mount points elsewhere than in `/mnt/`; some distros use `/media/` for this purpose.  You can also create an empty directory anywhere in the filesystem to use as a custom mount point.

<!-- no need to reboot or re-mount, since the drive isn't currently mounted anyway and the mount command re-reads fstab on execution -->

### Step 3 - StepMania Preferences

Finally, update your Preferences.ini file to include the following values:

```ini
MemoryCardOsMountPointP1=/mnt/player1
MemoryCardOsMountPointP2=/mnt/player2
MemoryCardProfiles=1
MemoryCardUsbBusP1=-1
MemoryCardUsbBusP2=-1
MemoryCardUsbLevelP1=-1
MemoryCardUsbLevelP2=-1
MemoryCardUsbPortP1=-1
MemoryCardUsbPortP2=-1
MemoryCards=1
```