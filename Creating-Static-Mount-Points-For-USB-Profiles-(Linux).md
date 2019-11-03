If you run StepMania on Linux, you may want to create static mount points for USB-based profiles.  Doing so will allow you associate a USB port on your PC with a specific player's memorycard slot, as is common on arcade cabinets.

The process is **moderately technical** and assumes you are comfortable editing system files in Linux via the command line.  If you are not comfortable with this, do not proceed.

---

### Step 1 - Finding the USB port _by-path_

Since disk names `sda`, `sdb`, and so on are not deterministic, depending on the order in which devices are plugged, we can't use them to reliably identify players.  Fortunately, Linux allows us to select a disk "by path," which amounts to associating a physical USB _port_ as a specific device, which is typically what we want for USB profiles.

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

Copy this output to a text editor and repeat the command with the USB stick plugged into the USB port you wish to associate with PLAYER_2.  Copy that output as well.

### Step 2 - Create _fstab_ Entries

You will use part of the output from the previous step to create new entries in `/etc/fstab`, the file which associates specific devices (in this case a USB port _by-path_) with named mount points that can be passed to StepMania. 

The resulting _fstab_ entries will look like:

```
/dev/disk/by-path/pci-0000:00:14.0-usb-0:10:1.0-scsi-0:0:0:0-part1 	/mnt/player1 auto rw,user,noauto,noatime 0 0
/dev/disk/by-path/pci-0000:00:14.0-usb-0:10:1.0-scsi-0:0:0:0 		/mnt/player1 auto rw,user,noauto,noatime 0 0
/dev/disk/by-path/pci-0000:00:14.0-usb-0:4:1.0-scsi-0:0:0:0-part1 	/mnt/player2 auto rw,user,noauto,noatime 0 0
/dev/disk/by-path/pci-0000:00:14.0-usb-0:4:1.0-scsi-0:0:0:0 		/mnt/player2 auto rw,user,noauto,noatime 0 0
```

**Note:** There will be other entries already defined in _fstab_ when you edit it (for example, the entry to mount your Linux filesystem to `/`).  You should leave those alone and just append the new entries for StepMania to the end of the file.

<!-- no need to reboot or re-mount, since the drive isn't currently mounted anyway and the mount command re-reads fstab on execution -->


### Step 3 - Create the Mount Points for StepMania

Next, you'll need to create the directories you specified in the previous step.  If you had wanted to use `/mnt/player1` and `/mnt/player2`, then you could create the directories using

```
mkdir /mnt/player1/
mkdir /mnt/player2/
```

Depending on the permissions of the location you chose, you may need to create the directories using `sudo`.

If you are seeing output in your logs like `mount: /mnt/player1/: mount point does not exist.` then you should ensure that you have completed this step.

### Step 4 - StepMania Preferences

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

You may also want to modify `MemoryCardProfileSubdir` and `MemoryCardProfileImportSubdirs` to suit your needs.  

StepMania uses `MemoryCardProfileSubdir` first when looking for profiles on USB memory cards.  If your Preferences.ini has `MemoryCardProfileSubdir=StepMania 5` then StepMania will look for a profile in a `StepMania 5` directory in the root of that USB disk.  It would not find any profiles if they were in a `StepMania 5.1` directory in the root of the same USB disk.

Fortunately, you can use `MemoryCardProfileImportSubdirs` to provide a semicolon delimited list of extra places to check.  So a configuration like this

```ini
MemoryCardProfileImportSubdirs=asdf;StepMania 5.1
MemoryCardProfileSubdir=StepMania 5
```

would look for profiles in `StepMania 5` first, then `asdf`, then `StepMania 5.1`.  This can be helpful for public machines that need to cater to various player needs.

### Step 5 - Disable automount

Some distros like Ubuntu (and [Ubuntu derivatives](https://wiki.ubuntu.com/DerivativeTeam/Derivatives) such as Mint), come preconfigured to automount USB devices as soon as they are inserted.  This conflicts with the way StepMania mounts drives and breaks USB memorycard support.

If you are unable to get USB memorycards working and and you see log output like

```
WARNING: failed to execute 'mount /dev/disk/by-path/pci-0000:00:1d.7-usb-0:4:1.0-scsi-0:0:0:0' with error 8192
```

your distro is likely automounting USB disks and you'll need to disable this.

If you are using **xfce** as your desktop environment you can 

 1. Thunar -> File Manager Preferences -> Advanced -> untick Enable Volume Management
 2. search "Removable Drives and Media" in the settings and untick every single automount option
 
If you are using **Cinnamon** as your desktop environment you can

 1. Open a file browser window -> Edit menu -> Preferences -> Behavior -> untick all automount options under "Media Handling"
 
 
### Troubleshooting Suggestions

Ubuntu seems to have a lot of autoconfig "magic" surrounding `/media`, so you may have an easier time using `/mnt` for USB profiles instead.

If you are going through the trouble of configuring USB memory cards, you're probably setting up a dedicated arcade machine.  The best practice for such setups is to run StepMania 5 in its own xsession without a desktop environment or graphical file manager.  This should improve StepMania's performance (at the cost of being more confusing to use if you are less comfortable with Linux).

On machines with a USB3 controller, a physical port may be mapped to different paths depending on if a USB2 or USB3 device is inserted. You should use USB2 and USB3 devices in the port to check for any path variations that may be used for that port.