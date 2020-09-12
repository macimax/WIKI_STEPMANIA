Most preferences can (and should) be set with StepMania's UI, but there are times when you may want to manually edit *Preferences.ini* where your settings are stored.

Before attempting to edit your *Preferences.ini* file, it is important to understand

+ StepMania expects specific values for each preference
+ many of these are not documented anywhere yet (we're working on it!)
+ providing an invalid value may cause StepMania to not work as expected (or at all)

With that established, if you wish to proceed, you'll need to quit StepMania first if it is actively running.  This will ensure that any changes you make manually will stick when you start StepMania next time.

# Finding *Preferences.ini*
The location of your *Preferences.ini* file depends on your operating system and your version of SM5.


If you're using **SM5.0.12**:

<table>
<tbody>
  <tr>
    <td>Windows 10, 8, 7</td>
    <td>C:\Users\<code>USERNAME</code>\AppData\Roaming\StepMania 5\Save\Preferences.ini</td>
  </tr>
  <tr>
    <td>macOS</td>
    <td>/Users/<code>USERNAME</code>/Library/Preferences/StepMania 5/Preferences.ini</td>
  </tr>
  <tr>
    <td>Linux</td>
    <td>/home/<code>USERNAME</code>/.stepmania-5.0/Save/Preferences.ini</td>
  </tr>
</tbody>
</table>

If you're using **SM5.1-beta**:

<table>
<tbody>
  <tr>
    <td>Windows 10, 8, 7</td>
    <td>C:\Users\<code>USERNAME</code>\AppData\Roaming\StepMania 5.1\Save\Preferences.ini</td>
  </tr>
  <tr>
    <td>macOS</td>
    <td>/Users/<code>USERNAME</code>/Library/Preferences/StepMania 5.1/Preferences.ini</td>
  </tr>
  <tr>
    <td>Linux</td>
    <td>/home/<code>USERNAME</code>/.stepmania-5.1/Save/Preferences.ini</td>
  </tr>
</tbody>
</table>

In each of these paths, <code>USERNAME</code> will be your OS username.

🔷 Tip: If you find yourself manually changing Preferences frequently, you may wish to create a shortcut there. The user content folder can be cumbersome to navigate to.


## macOS

Apple hides the *Library* folder by default but there are a few ways to get there.

Finder's *Go* menu has a *Go To Folder...* item which brings up a dialog box.  Copy and paste the path provided above and click *Go*.

![Go To Folder... + Preferences.ini path](http://i.imgur.com/xrUN4gHh.png)

Alternatively, it is possible to [un-hide the Library folder from Finder](https://apple.stackexchange.com/a/378378), allowing you to navigate to it like any other folder.