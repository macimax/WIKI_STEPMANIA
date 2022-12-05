# Windows
Install **IO2Key**, available from Nirvash. Refer to the instructions in [the video](https://www.youtube.com/watch?v=xo5m9dlNFfY).

# Linux
Install the **PIUIO input driver for Linux** originally authored by djpohly, currently hosted by DinsFire64.  Refer to that project's [readme](https://github.com/DinsFire64/piuio) for instructions.

With the driver installed, Linux will see the PIUIO as a generic joystick.  You'll need to map its buttons using StepMania's **Config Key/Joy Mappings** screen.

To enable support for cabinet lights, [edit your Preferences.ini](https://github.com/stepmania/stepmania/wiki/Manually-Changing-Preferences) to set

```ini
LightsDriver=Linux_PIUIO_Leds
```

If your arcade cabinet includes an auxiliary PIUIO "button" card, used for menu buttons on Pump it Up FX, CX, and TX cabinet models (not included with/used in ITG2 dedicabs), edit your Preferences.ini to set
```ini
LightsDriver=PIUIO_Leds,PIUIOBTN_Leds
```

*Historical Note:*
Old versions of this driver (prior to v0.2 in August 2014) required you to manually specify "PIUIO" as an InputDriver in Preferences.ini.  Many guides commonly found on the Internet still include an instruction for this but **it is no longer necessary and doing so will prevent StepMania from handling any input.**