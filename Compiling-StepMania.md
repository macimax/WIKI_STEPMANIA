#Compiling StepMania

For those that are either adventurous or wish to have the latest bug-fixes, compiling the source code is an option.

##Common Items

No matter what, both the source code and a way to build the source code are required.

* Use [git](https://git-scm.com/) or a third party program such as [Sourcetree](http://www.sourcetreeapp.com) to clone the StepMania repository. For the terminal users, running `git clone https://github.com/stepmania/stepmania.git` is sufficient.
* Use [CMake](http://www.cmake.org/) to generate project files for your specific system.
* Ensure you have all of the needed dependencies. This is dependent on your operating system.

##Operating System Specific

There may be some specific things to watch out for. This section covers that.

###Windows

Ensure you have the [Direct X Summer 2010 SDK](https://www.microsoft.com/en-us/download/details.aspx?id=6812) installed.

Currently we only support using generated [Visual Studio](https://www.visualstudio.com/en-us/products/visual-studio-community-vs.aspx) solution files from CMake. Please use either Visual Studio Community 2013 or 2015. If you already have a paid version of either of those year based releases, that is also sufficient.

###Linux

First, please see [Linux Dependencies](http://www.stepmania.com/wiki/linux-dependencies/) for libraries and programs required to build StepMania on Linux.

Then, follow the instructions provided by Kyzentun in [this thread](http://www.stepmania.com/forums/stepmania-releases/show/457), which are presented here in slightly modified form. Anything that `looks like this` is a command to be run in the terminal.

1. Install git and cmake if you haven't already.
2. Figure out where you'd like to keep the source code, and clone the project (`git clone https://github.com/stepmania/stepmania.git`) to obtain the code.
3. Once the project is done cloning (it will take a while), go into the build directory with `cd Build`. It is in here where the build files will be generated.
4. Run `cmake .. && cmake ..` to set up your environment. You can view the CMakeCache.txt file that generated to see the different options and settings available.
5. Finally, we can start the build process by running `make` in the same directory. Compiling will take a while, especially if this is the first time (or a file with large-reaching changes has been changed).
6. Once the build has finished, go back to the parent directory and run `./stepmania` to begin playing.

###Mac OS X

At this time, only generated [Xcode](https://developer.apple.com/xcode/) projects are supported.
