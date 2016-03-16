You will absolutely, positively need:

* cmake (version 2.8.12 minimum, version 3.2 or higher recommended)
* Either clang++ and clang, or gcc and g++
* OpenGL libraries and headers (The libraries should come with your graphics card driver; headers are Debian: mesa-common-dev)
* GLU libraries and headers (Debian: libglu1-mesa-dev)
* GLEW 1.5 or newer (Debian: depending on your OS version, libglew1.5-dev or libglew1.6-dev or libglew1.7-dev and so on)
* X11 libraries and headers
* Especially: Xtst and Xrandr (Debian: libxtst-dev and libxrandr-dev respectively)
* libpng (Debian: libpng12-dev)
* libjpeg (Debian: libjpeg8-dev)
* zlib (Debian: zlib1g-dev)
* libBZ2 (Debian: libbz2-dev)
* libogg and libvorbis (Debian: libogg-dev and libvorbis-dev respectively)
* libpthread (Debian: part of libc6-dev)
* yasm (for building ffmpeg)
* Headers and libraries for one or more of: ALSA  (Debian: libasound-dev), OSS (kernel headers actually), PulseAudio (Debian: libpulse-dev), and/or JACK (Debian: libjack-dev)
* and of course, GNU make.

You may also want:

* For even the slightest prayer of people helping you when things go wrong: libiberty (Debian: part of binutils-dev)
* For a loading dialog: GTK+ 2 (Debian: libgtk2.0-dev)
* For MP3 support: libMAD (Debian: libmad0-dev)


### Debian or Mint
```
sudo apt-get install mesa-common-dev libglu1-mesa-dev libglew1.5-dev libxtst-dev libxrandr-dev libpng12-dev libjpeg8-dev zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev libjack-dev binutils-dev libgtk2.0-dev libmad0-dev libjack0
```

### Fedora 23
```
dnf install http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
dnf install libXrandr-devel libXtst-devel libpng-devel libjpeg-devel zlib-devel libogg-devel libvorbis-devel yasm alsa-lib-devel pulseaudio-libs-devel libmad-devel bzip2-devel jack-audio-connection-kit-devel libva-devel pcre-devel gtk2-devel
```
Dance pads are not supported on Fedora until someone else figures out what's wrong with them and posts instructions.