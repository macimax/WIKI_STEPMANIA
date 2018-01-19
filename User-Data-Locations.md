Data Locations
--------------
Modern operating systems have user profiles; by default, StepMania 5.0 and later store user data (such as score data and settings) within a folder in your operating system's home directory. The exact location varies by platform;

* **Windows**: `%APPDATA%\StepMania 5\`
* **Linux**: `~/.stepmania-5.0/`
* **Mac OS X**: `~/Library/Application Support/StepMania 5/`

#### Mac OS X
The *~/Library* directory is hidden from Finder by default, which makes adding content on OS X somewhat cumbersome.  You can follow the instructions from the Wiki page on [Manually Changing Preferences](Manually-Changing-Preferences) but use the path provided above to access your StepMania profile directory.

Songs and other add-ons can be loaded from StepMania's user data directory, using the folders provided within.

Portable Mode
--------------
In some cases, such as if you are running StepMania from a portable drive, or otherwise do not wish to store profile data in your home directory, StepMania can be configured to store user data within its installation directory instead&emdash;which was the default behaviour on older versions such as 3.9. 

To activate Portable Mode, create a blank text file named ``Portable.ini`` in the folder where StepMania was installed. User profile data is stored within a ``Save`` folder within the installation directory.

Storing content in other locations
-------------
The [Preferences file](https://github.com/stepmania/stepmania/wiki/Preferences.ini) contains settings that can be used to load content, such as songs, courses, and add-ons, from locations different from the user data directory or where StepMania is installed. 

This is useful if you are running multiple builds of StepMania and wish to keep your song library synchronized between them, or if you want to store your content on a different hard drive or partition to conserve disk space.
