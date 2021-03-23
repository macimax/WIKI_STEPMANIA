# Compiling from Source on macOS

## setup

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

## clone StepMania from GitHub

Use git's command-line interface to clone StepMania from GitHub.
```bash
git clone --depth=1 https://github.com/stepmania/stepmania.git
```


When that has completed, `cd` into your local copy of the repository and initialize your local project's submodules.
```bash
cd stepmania
git submodule update --init
```

## use cmake to generate build files

Next, `cd` into your *Build* folder and use cmake to generate a makefile.
```bash
cd Build
cmake -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Release .. && cmake  ..
```

If you have been designated as the macOS developer to build a formal, major release for distribution purposes, you can use the `WITH_FULL_RELEASE` flag.  This will remove any git hash from the StepMania version number in the resulting executable.

```bash
cmake -G "Unix Makefiles" -DWITH_FULL_RELEASE=ON -DCMAKE_BUILD_TYPE=Release .. && cmake  ..
```

## build

Finally, build StepMania.

You can use the `-j` flag to compile more quickly by using multiple simultaneous build jobs. The number of build jobs should not exceed 2x your CPU cores.
So if you have 4 cores, you can use `-j8`.  If you have 2 cores, you can use `-j4`.

```
make -j8
```

## allow Input Monitoring

**⚠️ Note:** For macOS 10.15 ("Catalina") and newer, you'll need to explicitly grant StepMania *Input Monitoring* permissions in System Preferences for input to be recognized. 

![grant StepMania Input Monitoring permissions for macOS](https://i.imgur.com/cWpnT9Jl.png)

Add StepMania to the list of permitted applications in: System Preferences → Security & Privacy → Input Monitoring

You'll need to remove StepMania from this list and re-add it every time you rebuild from source.