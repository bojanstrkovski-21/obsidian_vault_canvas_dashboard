
1. Create the script and make it executable (open terminal in the folder where
the script is  and type **cmod +x autostart.sh** and hit enter)
use any text editor and create for example autostart.sh text file
open it with the text editor and at the begining add the shebang (**#!/usr/bin/env bash**)
than after this type youre stuf.
2. Create **.desktop** file in **~/.config ($HOME/.config)**
Folder might not exist by default. If not, create it.
The file can be named any as long as the extension is .desktop.

Its content should look like this:

[Desktop Entry]  
Version=1.0  
Encoding=UTF-8  
Name=Script  
Type=Application  
**Exec=/usr/local/share/scripts/autostart.sh**  
Terminal=false  
StartupNotify=false  
Hidden=false  


startxfce4

The startxfce4 is a convenient script to start an Xfce 4 session from the console. It will give you a session with a taskbar and a panel and with the desktop manager and window manager running.

All programs, or symbolic links to programs, in ~/Desktop/Autostart/ will be run by startxfce4 on startup.

To customize the behaviour of startxfce4, copy the file ${sysconfdir}/xfce4/xinitrc to your personal ~/.config/xfce4/ directory and edit that file. If you install from source, ${sysconfdir} defaults to /usr/local/etc; for binary packages it is often set to /etc.

With the inclusion of a session manager in Xfce 4.2, the preferred way to change startup behaviour is by using the "Save session" option in the logout dialog.

Or you can use the `xfce4-autostart-editor` program.