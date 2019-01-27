.redir is a text file that contains the name of the file you want this object to redirect to.

For example, ScreenSelectMusic course music.redir containing the text "_Music menu" will redirect to a file with that name.

You can chain redirects. Extension for the file you are redirecting to is not required inside the redir.

Note that putting a redir in a folder will make StepMania start again from the source folder.
For example, if you have a redir inside Graphics/ComboNumbers/ named Combo100.redir and you want it to point to a file named Combo110.png inside Graphics/ComboNumbers, you must put `Graphics/ComboNumbers/Combo100` instead of `Combo100` inside the redir.