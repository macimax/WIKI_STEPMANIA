# Linux

**⚠️ Warning:** Do not use autogen.sh to compile StepMania. It is not maintained and you will likely run into issues such as no sound.

## 1. Prepare dependencies

#### 1-a: Prepare dependencies (Debian-based systems)

Open a terminal and:

```
# On Ubuntu 17.04 or Debian >= 9.0. Worked on 18.04, 19.04.
sudo apt-get install build-essential cmake mesa-common-dev libglu1-mesa-dev libglew1.5-dev libxtst-dev libxrandr-dev libpng-dev libjpeg-dev zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev binutils-dev libgtk-3-dev libmad0-dev libudev-dev libva-dev nasm
# On Ubuntu 22.04
sudo apt install build-essential cmake mesa-common-dev libglu1-mesa-dev libglew-dev libxtst-dev libxrandr-dev libpng-dev libjpeg-dev zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev binutils-dev libgtk-3-dev libmad0-dev libudev-dev libva-dev nasm
```

#### 1-b: Prepare dependencies (Fedora-based systems)

Open a terminal and:
```
dnf install http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
dnf install libXrandr-devel libXtst-devel libpng-devel libjpeg-devel zlib-devel libogg-devel libvorbis-devel yasm alsa-lib-devel pulseaudio-libs-devel libmad-devel bzip2-devel jack-audio-connection-kit-devel libva-devel pcre-devel gtk3-devel glew-devel libudev-devel
```

## 2: Clone, Initialize Submodules, Build

Clone StepMania's `5_1-new` branch (the default branch) from GitHub to your local machine:
```
git clone --depth=1 https://github.com/stepmania/stepmania.git
```

Initialize your local repository's submodules:
```
cd stepmania
git submodule update --init
```

Use cmake to generate a makefile for a release build of StepMania:
```
cd Build
cmake -G 'Unix Makefiles' -DCMAKE_BUILD_TYPE=Release .. && cmake ..
```

Build StepMania.
```
make -j8
```
The job count passed to `make` should not be more than double the number of cores you have.<br>e.g. `-j8` if your CPU has 4 cores.

<hr>

#### 2-b: Fetching the 5.2 branch

Work on StepMania 5.2 was merged into the `master` branch, so fetching master (which is not the default) will allow you to build StepMania 5.2.  Development on this branch is currently paused indefinitely, and it is considered **unsupported**.

If you'd like to fetch this branch, use:
`git clone --single-branch -b master --depth=1 https://github.com/stepmania/stepmania.git`

From there, the steps of initializing submodules, generating a makefile, and building should be the same.

**Historical Note:**  This branch was previously thought of as "5.1", but was renamed to 5.2 after the release of [5.1.-3](https://github.com/stepmania/stepmania/releases/tag/v5.1.0a3).

<hr>

## 3: Making a Launcher

If you want to run StepMania from a launch button like some desktop environments have, make a shell script like this and set the launch button to run the shell script. This assumes that the stepmania folder is \~/stepmania.  "\~/" is shorthand for *the home folder of the current user on Linux*.

Make a new empty text document and add the following:
```
#!/bin/bash
cd ~/stepmania
./stepmania
```
Save it as stepmanialauncher.sh or something similar

Right click it and make it executable in properties>permissions

### Desktop File

To create an ordinary desktop launcher that you can find in the application menu (that optionally has a proper icon), you can edit the `stepmania.desktop` file. This will allow Stepmania to be treated as any other application (be searchable, have an icon, etc.). You need to give the full path to Stepmania under TryExec and Exec; if you installed Stepmania in your home folder you would use this (replacing USERNAME_HERE):

```
[Desktop Entry]
Encoding=UTF-8
Name=StepMania
GenericName=Rhythm and dance game
TryExec=/home/USERNAME_HERE/stepmania/stepmania
Exec=/home/USERNAME_HERE/stepmania/stepmania
Terminal=false
Icon=/home/USERNAME_HERE/stepmania/stepmania-ssc
Type=Application
Categories=Application;Game;ArcadeGame
Comment=A cross-platform rhythm video game.
```

If you want the icon to work, you will need to put a picture with the name `stepmania-ssc` in the directory yourself.

Move it to the proper location:

```
sudo mv ~/stepmania/stepmania.desktop /usr/share/applications/
```

You can then look at the applications menu and Stepmania will appear.

## 4: Configuration and User Content

Install songs in ~/.stepmania-5.1/Songs/

Install themes in ~/.stepmania-5.1/Themes/

Install NoteSkins in ~/.stepmania-5.1/NoteSkins/

Preferences are in ~/.stepmania-5.1/Save/Preferences.ini

Profiles are in ~/.stepmania-5.1/Save/LocalProfiles/

## 5: Updating

When you want to update your copy of SM5:
```
cd path/to/stepmania
git pull origin 5_1-new
cd Build/
cmake -G 'Unix Makefiles' -DCMAKE_BUILD_TYPE=Release .. && cmake ..
make -j8
```

## 6: Controllers and Joysticks

As far as getting your controller to work, as long as its an xinput detected device that should be as simple as entering StepMania settings and pressing the appropriate buttons in the key config setup.

If not you might wanna have it emulate a keyboard using Antimicro

simply add ppa:mdeguzis/libregeek to your ppa's in software sources
```
sudo apt-get update
sudo apt-get install antimicro
```