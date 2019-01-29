# About

Although StepMania 5.1 is currently in beta, it offers many great new features and should already be stable enough to replace older versions of SM5.  You can read more about SM5.1's new features in the release notes for [beta1](https://github.com/stepmania/stepmania/releases/tag/v5.1.0-b1) and [beta2](https://github.com/stepmania/stepmania/releases/tag/v5.1.0-b2).

Unfortunately for macOS users, StepMania's macOS code hasn't kept up with the times, and installing any version of SM5 on a modern version of macOS is currently tricky.  This page will describe the steps necessary to install and run SM5.1 on macOS.



## 1. Download SM5.1 from GitHub.

Start by downloading the macOS version of StepMania 5.1 beta from its GitHub page.

  * [SM5.1-beta2](https://github.com/stepmania/stepmania/releases/tag/v5.1.0-b2)

After this step, you should have the **.dmg** file in your *Downloads* folder.



## 2. Mount the *.dmg* and drag the folder to your Desktop

Double-click the dmg you downloaded to mount it in your filesystem.  The window that automatically opens should show a single folder titled `StepMania-5.1.0`.  Drag this folder to your Desktop.



## 3. Attempt to run SM5.1 beta from your Desktop

Open the new folder on your Desktop, and double-click on the StepMania application to start it.  You will likely be notified that `"StepMania" can't be opened because it is from an unidentified developer.`  Click OK.

![Gatekeeper](https://imgur.com/c2Uar5Pl.png)



## 4. Allow SM5.1 to open

From the Apple Menu, go to `System Preferences...` and choose *Security & Privacy* from the first row.  Click *Open Anyway* to grant SM5.1 permission to open.

![Open Anyway](https://imgur.com/tTXSRvLl.png)



## 5.  Attempt to run SM5.1 again

Double-click the StepMania application on your Desktop to attempt to start it again.  If it starts to load songs, you can stop reading now and enjoy SM5.1 beta.

If you are given an error message like `Metric "Common::ScreenWidth" is missing.` or `No NoteSkins found.` click **Abort**.

![Quarantine](https://i.imgur.com/EeWAgc4l.png)

You've encountered a [known bug](https://github.com/stepmania/stepmania/issues/1299#issuecomment-275114142) that can be resolved by running a command from your Terminal.

## 6. Remove Quarantine Extended Attribute from SM5.1

For this step, you'll need to use your macOS Terminal.  You can find it by pressing <kbd>⌘</kbd> + <kbd>Spacebar</kbd> to bring up Spotlight Search, typing `Terminal`, and pressing <kbd>Return</kbd>.

Assuming your `StepMania-5.1.0` folder is on your Desktop, copy and paste this command into your terminal, and press <kbd>Return</kbd> to run it.  This command will **not work** as-is if the folder is not on your Desktop.

```bash
xattr -dr com.apple.quarantine ~/Desktop/StepMania-5.1.0/
```

Assuming it worked, the Terminal will not give any error messages or really do anything.  No news is good news in Terminal-land.

You should now be able to close the Terminal window and successfully start SM5.1 beta.