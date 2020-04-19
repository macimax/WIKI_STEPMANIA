# Windows
Install **IO2Key**, available from Nirvash. Refer to the instructions in [the video](https://www.youtube.com/watch?v=xo5m9dlNFfY).

# Linux
Install the **PIUIO input driver for Linux** available from djpohly.  Refer to the [readme provided with the project](https://github.com/djpohly/piuio).

With the driver installed, Linux will see the PIUIO as a generic joystick.  You'll need to map its buttons using StepMania's **Config Key/Joy Mappings**.

To enable support for cabinet lights, [edit your Preferences.ini](https://github.com/stepmania/stepmania/wiki/Manually-Changing-Preferences) to set

```ini
LightsDriver=Linux_PIUIO_Leds
```

*Historical Note:*
Old versions of this driver (prior to v0.2 in August 2014) required you to manually specify "PIUIO" as an InputDriver in Preferences.ini.  Many guides commonly found on the Internet still include an instruction for this but **it is no longer necessary and doing so will prevent StepMania from handling any input.**