If you run StepMania on Linux, you may want to create static mount points for USB-based profiles.  Doing so will allow you associate a USB port on your PC with a specific player's memorycard slot, as is common on arcade cabinets.

The process is **moderately technical** and assumes you are comfortable editing system files in Linux via the command line.  If you are not comfortable with this, do not proceed.

---

### Step 1 - grep-ing by-path

Run the following command from your terminal with a single USB drive plugged into the the USB port you wish to associate with PLAYER_1:
```bash
ls -l /dev/disk/by-path grep by-path /etc/fstab
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

You will use part of that output to create entries in _fstab_ which will associate a specific USB port (_by-path_) with a named mount point that you can pass to StepMania. 

The resulting _fstab_ entries will look like:

```
/dev/disk/by-path/pci-0000:00:14.0-usb-0:10:1.0-scsi-0:0:0:0-part1 	/mnt/player1 auto rw,user,noauto,sync,exec 0 0
/dev/disk/by-path/pci-0000:00:14.0-usb-0:10:1.0-scsi-0:0:0:0 		/mnt/player1 auto rw,user,noauto,sync,exec 0 0
/dev/disk/by-path/pci-0000:00:14.0-usb-0:4:1.0-scsi-0:0:0:0-part1 	/mnt/player2 auto rw,user,noauto,sync,exec 0 0
/dev/disk/by-path/pci-0000:00:14.0-usb-0:4:1.0-scsi-0:0:0:0 		/mnt/player2 auto rw,user,noauto,sync,exec 0 0
```

Note that depending on your Linux distribution, you may want/need to create your named mount points elsewhere than in _/mnt/_.

After doing so, you can either reboot your PC or reload your fstab via `mount -a`

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