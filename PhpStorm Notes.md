# Ipad/External pc won't connet using port 63342 #

In Settings/Build/Debugger 

You need to change port number to something else as 63342 is used by all IDE devices as per [article](https://intellij-support.jetbrains.com/hc/en-us/community/posts/207042105-Getting-connection-refused-on-built-in-web-server?page=1#community_comment_115000109110).  No external computers will connect using port 63342 

**Also change debug port number in chrome jetbrains plugin**

Enable allow unsigned requests and allow external connections 



## Cmder Open Here ##
**Install** `.\cmder.exe /REGISTER ALL` **Remove** `.\cmder.exe /REGISTER ALL`

## Heap memory sizes ##

1024 MB (1 GB), 2048 MB (2 GB), 4096 MB (4 GB), 8192 MB (8 GB).

## Set Phpstorm Terminal to use cmder ##
[See](https://github.com/cmderdev/cmder/issues/282#issuecomment-219684282) 

**Add environmental variable** name: `CMDER_ROOT value:F:\bin\cmder`


**Set Shell Path to** `"cmd.exe" /k "%CMDER_ROOT%\vendor\init.bat"`

![](http://i.imgur.com/lOMtWhv.png)

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

## File Types ##

Markdown
goto  Settings > File Types > Find Markdown in the Registered Patterns window delete .md

Then got an md file in your Project Window, right click and choose Fil Association and the Default Program