Windows does not natively support mounting drives by port. However, the paid software USBDLM can add support. Coincidentally this will also work for any other arcade games that still use USB drives for saving.

# Step 1. Download USBDLM
[Download](https://www.uwe-sieber.de/usbdlm_e.html#download). Then extract. Then place somewhere where it won't be moved so you can register the service later on. (Don't put it in Program Files, it causes problems)

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

# Step 5. Assign letters in preferences.ini

Refer to the preferences.ini wiki for this, but MAKE SURE the backslash to your drive letter has been replaced with a forward slash.