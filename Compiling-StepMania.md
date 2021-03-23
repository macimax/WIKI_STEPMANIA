# Compiling StepMania 

For those that are either adventurous or wish to have the latest bug-fixes, compiling the source code is an option.

Operating System-specific instructions:
* [Windows](Compiling-StepMania-Windows)
* [Linux](Compiling-StepMania-Linux)
* [macOS](Compiling-StepMania-macOS)

## Common Items

No matter what, both the source code and a way to build the source code are required.

* Use [git](https://git-scm.com/) or a third party program such as [Sourcetree](http://www.sourcetreeapp.com) to clone the StepMania repository. For the terminal users, running `git clone --depth=1 https://github.com/stepmania/stepmania.git` is sufficient.
* Init submodules.  For terminal users, `git submodule update --init` should be sufficient.
* Use [CMake](http://www.cmake.org/) to generate project files for your specific system.
* Ensure you have all of the needed dependencies. This is dependent on your operating system.

## Submodules

<!-- is this still accurate? -quietly, 23 March 2021 -->
The master branch uses submodules for some external dependencies like ffmpeg,
so they are not bundled. As a side effect, if you click the "Download ZIP"
button on github to get a source zip, you will not be able to build that zip.
