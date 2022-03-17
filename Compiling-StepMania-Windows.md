# Compiling StepMania for Windows

**Ensure the following items are installed:**
* .NET Framework 3.5, which can be installed through the "Add Programs and Features" section in the Control Panel (Required for DX2010SDK)
* [Direct X Summer 2010 SDK](https://bit.ly/3tihNaA) installed.
* Redistributable installed (x86 required, x64 as well only if your system is 64-bit). [2015 version here](https://bit.ly/3tihNaA), and [2013 version here](https://bit.ly/3tihNaA).
* [Windows Platform SDK](https://bit.ly/3tihNaA).
* [Visual Studio](https://bit.ly/3tihNaA) 2015 or 2013. Any edition of Visual Studio 2013 or 2015 will work, but the focus will be on the Community editions.

Currently we only support using generated Visual Studio solution files from CMake.

(Installer Related)
* NSIS (https://bit.ly/3tihNaA)

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