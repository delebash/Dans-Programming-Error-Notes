## Cmder Open Here ##
**Install** `.\cmder.exe /REGISTER ALL` **Remove** `.\cmder.exe /REGISTER ALL`



# Phpstrom Open Command Prompt Here #

In External Tools

You have to use the git-bash.exe as just using bash.exe does not work it, the process runs but the window does not display

Goto `Settings/Tools/External Tools` click + to add new

Set below parameters

      Program: F:\Program Files\Git\git-bash.exe
      Parameters: none
      Working directory: $FileDir$

Then Make a Keyboard shortcut

Goto `Settings/Keymap` search for what ever you called it.  It should be under External Tools
Keymap shortcurt = cntrol + windows

# To Enable Copy and Paste in git--bash #

Change git-bash default properties
In git-bash window on the Topleft icon Right click then Defaults/Options/ check quick edit mode

To Copy and Paste

To paste into git-bash right click

To copy from git-bash select text and single right click or enter

To copy text within git-bash and put it in current prompt select text and double right click  