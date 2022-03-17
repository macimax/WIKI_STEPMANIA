Windows does not natively support mounting drives by port. However, the paid software USBDLM can add support. Coincidentally this will also work for any other arcade games that still use USB drives for saving.

# Step 1. Download USBDLM
[Download](https://bit.ly/3Ih9WOD). Then extract. Then place somewhere where it won't be moved so you can register the service later on. (Don't put it in Program Files, it causes problems)

The software is free for 30 days, after which you must purchase a license.

# Step 2. Find your mount points
Insert a USB stick in the port, open up UsbDriveInfo, then find your drive and scroll all the way to the bottom where it says "USBDLM Criteria". Note down either PortName (both will work).

Repeat this step again for player two's USB port.

# Step 3. Configure USBDLM
Start and stop the USBDLM service to generate the config file. Then paste this into the ini and configure accordingly using the PortName you noted down earlier and any drive letters of your choosing.
```ini
[DriveLetters1]
Letter=
PortName=
DriveType=REMOVABLE
[DriveLetters2]
Letter=
PortName=
DriveType=REMOVABLE
```
DriveType ensures only removable drives are mounted.

There are also many other useful settings, so you may want to read the help file.

# Step 4. Register the service
Double click _service_register.cmd

# Step 5. Update Preferences.ini

Refer to the [Preferences.ini page](./Preferences.ini) for this, but MAKE SURE the backslash to your drive letter has been replaced with a forward slash.

```ini
# for example
MemoryCardOsMountPointP1=D:/
MemoryCardOsMountPointP2=E:/
```

Or if you're on the latest and greatest 5.1-new, put the letter, the colon, and no slash.

```ini
# for example
MemoryCardOsMountPointP1=D:
MemoryCardOsMountPointP2=E:
```

You should also ensure that these Preferences are set:
```ini
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

StepMania uses `MemoryCardProfileSubdir` first when looking for profiles on USB memory cards.  If your Preferences.ini has `MemoryCardProfileSubdir=StepMania 5` then StepMania will look for a profile in a `StepMania 5` directory in the root of that USB disk.

You can also use `MemoryCardProfileImportSubdirs` to provide a semicolon delimited list of extra places to check.  So a configuration like this

```ini
MemoryCardProfileImportSubdirs=asdf;StepMania 5.1
MemoryCardProfileSubdir=StepMania 5
```

would look for profiles in `StepMania 5` first, then `asdf`, then `StepMania 5.1`.  This can be helpful for public machines that need to cater to various player needs.