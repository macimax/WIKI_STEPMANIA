#Compiling StepMania

For those that are either adventurous or wish to have the latest bug-fixes, compiling the source code is an option.

##Common Items

No matter what, both the source code and a way to build the source code are required.

* Use [git](https://git-scm.com/) or a third party program such as [Sourcetree](http://www.sourcetreeapp.com) to clone the StepMania repository. For the terminal users, running `git clone --depth=1 https://github.com/stepmania/stepmania.git` is sufficient.
* Init submodules.  For terminal users, `git submodule update --init` should be sufficient.
* Use [CMake](http://www.cmake.org/) to generate project files for your specific system.
* Ensure you have all of the needed dependencies. This is dependent on your operating system.

### Submodules
The master branch uses submodules for some external dependencies like ffmpeg,
so they are not bundled. As a side effect, if you click the "Download ZIP"
button on github to get a source zip, you will not be able to build that zip.

##Operating System Specific

There may be some specific things to watch out for. This section covers that.

###Windows

Ensure you have the [Direct X Summer 2010 SDK](https://www.microsoft.com/en-us/download/details.aspx?id=6812) installed.

Currently we only support using generated [Visual Studio](https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx) solution files from CMake. Please use either Visual Studio Community 2013 or 2015. If you already have a paid version of either of those year based releases, that is also sufficient.

###Linux

####1-a: Prepare dependencies(Debian Based systems)

Open a terminal and:
```
sudo apt-get install build-essential
sudo apt-get install mesa-common-dev libglu1-mesa-dev libglew1.5-dev libxtst-dev libxrandr-dev libpng12-dev libjpeg8-dev zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev binutils-dev libgtk2.0-dev libmad0-dev libudev-dev libva-dev
```
####1-b: Prepare dependencies(Fedora Based systems)

Open a terminal and:
```
dnf install http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
dnf install libXrandr-devel libXtst-devel libpng-devel libjpeg-devel zlib-devel libogg-devel libvorbis-devel yasm alsa-lib-devel pulseaudio-libs-devel libmad-devel bzip2-devel jack-audio-connection-kit-devel libva-devel pcre-devel gtk2-devel glew-devel libudev-devel
```

####2: Clone the stepmania git and compile stepmania

Open a terminal and:
```
git clone --depth=1 https://github.com/stepmania/stepmania.git
git submodule update --init
cd stepmania/Build/
cmake -G 'Unix Makefiles' -DCMAKE_BUILD_TYPE=Release .. && cmake ..
make -j8
```
The job count passed to make should not be more than double the number of cores you have.

####3: Making a Launcher

If you want to run stepmania from a launch button like some desktop environments have, make a shell script like this and set the launch button to run the shell script. This assumes that the stepmania folder is ~/stepmania. If you don't know already, "~/" is shorthand for the home folder of the current user on Linux.

Make a new emtpy text document and add the following:
```
#!/bin/bash
cd ~/stepmania
./stepmania
```
Save it as stepmanialauncher.sh or something similar

right click it and make it executable in properties>permissions

####4: Configuration

Install songs in ~/.stepmania-5.0/Songs/ 

Install themes in ~/.stepmania-5.0/Themes/ 

Install noteskins in ~/.stepmania-5.0/NoteSkins/ 

(noteskins for Stepmania 5.1 also go in ~/.stepmania-5.0/NoteSkins/)

Preferences are in ~/.stepmania-5.0/Save/Preferences.ini 

Profiles are in ~/.stepmania-5.0/Save/LocalProfiles/ 

###5: Updating

When you want to update your copy of SM5: 

cd into the stepmania folder you cloned, and run a git pull in terminal:

```
git pull origin master
cd Build/
cmake -G 'Unix Makefiles' -DCMAKE_BUILD_TYPE=Release .. && cmake ..
make -j8
```
####6: Controllers and Joysticks

As far as getting your controller to work, as long as its an xinput detected device that should be as trivial as entering stepmania settings and pressing the appropriate buttons in the key config setup.

If not you might wanna have it emulate a keyboard using Antimicro

simply add ppa:ryochan7/antimicro to your ppa's in software sources
```
sudo apt-get update
sudo apt-get install antimicro 
```

#### Fetching the 5.1 branch
5.1 was merged into master.  Fetching master will fetch the 5.1 branch.

#### Fetching the 5.0 branch
Use the branch name `5_0` instead of `master`.

###Mac OS X

At this time, only generated [Xcode](https://developer.apple.com/xcode/) projects are supported.
