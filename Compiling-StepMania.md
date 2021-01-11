# Compiling StepMania 

For those that are either adventurous or wish to have the latest bug-fixes, compiling the source code is an option.

Operating System-specific instructions:
* [Windows](#windows)
* [Linux](#linux)
* [macOS](#macos)

## Common Items ##

No matter what, both the source code and a way to build the source code are required.

* Use [git](https://git-scm.com/) or a third party program such as [Sourcetree](http://www.sourcetreeapp.com) to clone the StepMania repository. For the terminal users, running `git clone --depth=1 https://github.com/stepmania/stepmania.git` is sufficient.
* Init submodules.  For terminal users, `git submodule update --init` should be sufficient.
* Use [CMake](http://www.cmake.org/) to generate project files for your specific system.
* Ensure you have all of the needed dependencies. This is dependent on your operating system.

### Submodules ###
The master branch uses submodules for some external dependencies like ffmpeg,
so they are not bundled. As a side effect, if you click the "Download ZIP"
button on github to get a source zip, you will not be able to build that zip.


## Windows ##

**Ensure the following items are installed:**
* .NET Framework 3.5, which can be installed through the "Add Programs and Features" section in the Control Panel (Required for DX2010SDK)
* [Direct X Summer 2010 SDK](https://www.microsoft.com/en-us/download/details.aspx?id=6812) installed.
* Redistributable installed (x86 required, x64 as well only if your system is 64-bit). [2015 version here](https://www.microsoft.com/en-us/download/details.aspx?id=48145), and [2013 version here](https://www.microsoft.com/en-us/download/details.aspx?id=40784).
* [Windows Platform SDK](https://developer.microsoft.com/en-us/windows/downloads/windows-10-sdk).
* [Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/) 2015 or 2013. Any edition of Visual Studio 2013 or 2015 will work, but the focus will be on the Community editions.

Currently we only support using generated Visual Studio solution files from CMake.

(Installer Related)
* NSIS (http://nsis.sourceforge.net/Download)

(Installer Related)

If you intend to release SM as a Windows Installer, you will need NSIS. Once installed, use cmake, config/generate the solution file, and open it, you will have to change two things before it will work. Right click the "Solution" area for the StepMania Project and click properties. With ALL_BUILD configuration selected, find INSTALL and PACKAGE, and click the check mark for for Build. By default, they are disabled. Once SM builds, it will start a new task that will build the installer. It should go in: <Directory>\Build\_CPack_Packages\win32\NSIS once complete.

**Then, to compile:**

Before you do anything:
```batch
git clone --single-branch -b 5_1-new --depth=1 https://github.com/stepmania/stepmania.git
cd stepmania
git submodule update --init
```

**To compile with a GUI:**
1. Open cmake-gui from your start menu. Click browse source, then navigate to where you cloned the stepmania dir.
2. Click browse build, then navigate to the Build folder in the cloned stepmania dir.
3. Click configure.
4. Click generate.
5. Click Open Project, or if you're feeling adventurous you can navigate to the Build folder yourself and double click on the .sln.
6. Set the build type to release, then click build. The files will get put in the "Program" directory of stepmania.

**If you would like to build StepMania on Windows without a GUI (headless server, etc):**

Launch the Visual Studio Command Prompt from the start menu, or if you don't have access to the start menu you can cd to `%ProgramFiles(x86)%\Microsoft Visual Studio 14.0\VC\bin` and run `vcvars32.bat`.
```batch
:: substitute 'cd stepmania' with the location of where you cloned stepmania.
cd stepmania
cd Build
cmake -DCMAKE_BUILD_TYPE=Release .. && cmake ..
devenv StepMania.sln /Build Release
```

If you have the visual studio installer, the C++ build tools, and the CMake tools, and vcvars32.bat and would rather compile without installing Visual Studio:
```batch
::If you are using anything other than 2015 this will be in a different location.
"%ProgramFiles(x86)%\Microsoft Visual Studio 14.0\VC\bin\vcvars32.bat"
cd stepmania
cd Build
cmake -G "Visual Studio 14 2015" -A Win32 -DCMAKE_BUILD_TYPE=Release .. && cmake ..
msbuild.exe StepMania.sln /t:Build /p:Configuration=Release;Platform=Win32
```

## Linux

**⚠️ Warning:** Do not use autogen.sh to compile StepMania. It is not maintained and you will likely run into issues such as no sound.

### 1-a: Prepare dependencies (Debian-based systems)

Open a terminal and:

```
# On Ubuntu 17.04 or Debian >= 9.0. Worked on 18.04, 19.04.
sudo apt-get install build-essential cmake mesa-common-dev libglu1-mesa-dev libglew1.5-dev libxtst-dev libxrandr-dev libpng-dev libjpeg-dev zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev binutils-dev libgtk-3-dev libmad0-dev libudev-dev libva-dev nasm
```

### 1-b: Prepare dependencies (Fedora-based systems)

Open a terminal and:
```
dnf install http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
dnf install libXrandr-devel libXtst-devel libpng-devel libjpeg-devel zlib-devel libogg-devel libvorbis-devel yasm alsa-lib-devel pulseaudio-libs-devel libmad-devel bzip2-devel jack-audio-connection-kit-devel libva-devel pcre-devel gtk3-devel glew-devel libudev-devel
```

### 2: Clone, Initialize Submodules, Build

Clone StepMania's `5_1-new` branch from GitHub to your local machine:
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


#### 2-b: Fetching the 5.2 branch
Work on StepMania 5.2 was merged into the master branch, so fetching master will allow you to build StepMania 5.2.  Development on this branch is currently paused indefinitely, and it should be considered unsupported.

If you'd like to fetch this branch, use:
`git clone --single-branch -b master --depth=1 https://github.com/stepmania/stepmania.git`

From there, the steps of initializing submodules, generating a makefile, and building should be the same.

**Historical Note:**  This branch was previously thought of as "5.1", but was renamed to 5.2 after [5.1.-3](https://github.com/stepmania/stepmania/releases/tag/v5.1.0a3).



### 3: Making a Launcher

If you want to run StepMania from a launch button like some desktop environments have, make a shell script like this and set the launch button to run the shell script. This assumes that the stepmania folder is \~/stepmania.  "\~/" is shorthand for *the home folder of the current user on Linux*.

Make a new empty text document and add the following:
```
#!/bin/bash
cd ~/stepmania
./stepmania
```
Save it as stepmanialauncher.sh or something similar

right click it and make it executable in properties>permissions

### 4: Configuration and User Content

Install songs in ~/.stepmania-5.1/Songs/

Install themes in ~/.stepmania-5.1/Themes/

Install NoteSkins in ~/.stepmania-5.1/NoteSkins/

Preferences are in ~/.stepmania-5.1/Save/Preferences.ini

Profiles are in ~/.stepmania-5.1/Save/LocalProfiles/

### 5: Updating

When you want to update your copy of SM5:
```
cd path/to/stepmania
git pull origin 5_1-new
cd Build/
cmake -G 'Unix Makefiles' -DCMAKE_BUILD_TYPE=Release .. && cmake ..
make -j8
```

### 6: Controllers and Joysticks

As far as getting your controller to work, as long as its an xinput detected device that should be as simple as entering StepMania settings and pressing the appropriate buttons in the key config setup.

If not you might wanna have it emulate a keyboard using Antimicro

simply add ppa:mdeguzis/libregeek to your ppa's in software sources
```
sudo apt-get update
sudo apt-get install antimicro
```

## macOS

### setup

First, install [Homebrew](https://brew.sh/) by following the instructions on the Homebrew homepage.

Once it's installed, use Homebrew to install cmake and yasm.
```bash
brew install cmake yasm
```

If your version of macOS is recent, you'll already have git installed.  You can check using
```bash
which git
```
which will return a path to where `git` is located on your computer if it's available, or `git not found` if not.  

If you don't have git installed, use Homebrew to do so now.
```bash
brew install git
```

### clone StepMania from GitHub

Use git's command-line interface to clone StepMania from GitHub.
```bash
git clone --depth=1 https://github.com/stepmania/stepmania.git
```


When that has completed, `cd` into your local copy of the repository and initialize your local project's submodules.
```bash
cd stepmania
git submodule update --init
```

### use cmake to generate build files

Next, `cd` into your *Build* folder and use cmake to generate a makefile.
```bash
cd Build
cmake -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Release .. && cmake  ..
```

If you have been designated as the macOS developer to build a formal, major release for distribution purposes, you can use the `WITH_FULL_RELEASE` flag.  This will remove any git hash from the StepMania version number in the resulting executable.

```bash
cmake -G "Unix Makefiles" -DWITH_FULL_RELEASE=ON -DCMAKE_BUILD_TYPE=Release .. && cmake  ..
```

### build

Finally, build StepMania.

You can use the `-j` flag to compile more quickly by using multiple simultaneous build jobs. The number of build jobs should not exceed 2x your CPU cores.
So if you have 4 cores, you can use `-j8`.  If you have 2 cores, you can use `-j4`.

```
make -j8
```

### allow Input Monitoring

**⚠️ Note:** For macOS 10.15 ("Catalina") and newer, you'll need to explicitly grant StepMania *Input Monitoring* permissions in System Preferences for input to be recognized. 

![grant StepMania Input Monitoring permissions for macOS](https://i.imgur.com/cWpnT9Jl.png)

Add StepMania to the list of permitted applications in: System Preferences → Security & Privacy → Input Monitoring

You'll need to remove StepMania from this list and re-add it every time you rebuild from source.