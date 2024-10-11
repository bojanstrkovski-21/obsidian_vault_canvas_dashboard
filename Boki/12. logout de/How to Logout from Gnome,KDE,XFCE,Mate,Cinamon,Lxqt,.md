
# How to Log Out from Command Line in GNOME, KDE, XFCE & Other Linux Desktops

![[17cbbfc4de65d8007b22fba4b0d38b93.jpeg]](https://fostips.com/author/merilyn/)

This simple tutorial shows how to run single command to log out Linux desktop sessions, including **Gnome**, **Pantheon**, **Xfce4**, **KDE Plasma**, **Cinnamon**, **MATE**, **LXQt** and **LXDE**.

Log out using a Linux command may be useful for system administrator or using in a bash script. Each desktop has its own command to do the trick. And here I’m going to list them below one by one.

## 1\. Log out GNOME / Pantheon via single command:

For **Ubuntu**, **Fedora workstation**, and other Linux with GNOME, as well as **Elementary OS** Pantheon desktop. Simply run command below will bring up the ‘Log Out’ dialog, just like you click the system menu option:

```
gnome-session-quit
```

![[gnome-quit.webp]]

In case you don’t want to see the confirm dialog, but log out directly after running the command, use:

```
gnome-session-quit --no-prompt
```

Sometimes an unfinished process may break the command, so you can force log out via the command below. And, it also functions without pop-up the confirm dialog.

```
gnome-session-quit --force
```

## 2\. Command to Log out KDE Plasma:

For KDE 5, the command is a little bit different to other desktops. The log out command is:

```
qdbus org.kde.ksmserver /KSMServer logout <argument1> <argument2> <argument3>
```

The 3 arguments are numbers:

- &lt;argument1&gt; can be: **0** no confirm, or **1** to pop-up confirm dialog.
- &lt;argument2&gt; can be: **0** to log out, **1** to reboot, or **2** to hald.
- And &lt;argument3&gt; can be: **0** to activate after all session have ended, **1** to activate if no active session, **2** to force log-out, or **3** to ask what to do if sessions are still active.

And the 3 arguments can be all ‘-1’ to use default user config if any.

For example, log out KDE 5 with confirm window, just like you click the start menu option use command:

```
qdbus org.kde.ksmserver /KSMServer logout 1 0 3
```

Or, force log-out without confirm even when there are unfinished jobs:

```
qdbus org.kde.ksmserver /KSMServer logout 0 0 2
```

![[kde5-logoutcommand.webp]]

## 3\. Log out XFCE4 from command line:

For XUbuntu, Debian, and other Linux with XFCE4 Desktop environment, use the command below will do the same as you click log out option from system tray:

```
xfce4-session-logout
```

And you may use `--logout` flag, so it runs without popping up the confirm dialog:

```
xfce4-session-logout --logout
```

Like `--force` flag in GNOME, XFCE4 has `--fast` to activate quickly without saving current works.

```
xfce4-session-logout --fast
```

And, the command supports to specify which display session to log-out (get current display value via `echo $DISPLAY`):

```
xfce4-session-logout --display=DISPLAY
```

## 4\. Command to log out MATE Desktop:

For the MATE desktop in Ubuntu MATE, Linux Mint, etc, you may run this command to log-out with confirm dialog:

```
mate-session-save --logout-dialog
```

![[mate-logout.webp]]

To log out directly without user confirmation, use command:

```
mate-session-save --logout
```

Like GNOME and/or XFCE, there are also `--force` flag to log-out quickly without saving unfinished jobs, and `--display` to specify the display value.

## 5\. Command to log out Cinnamon:

For Linux Mint Cinnamon and other Linux with this desktop environment, use command:

```
cinnamon-session-quit
```

![[cinnamon-quit.webp]]

To get rid of the confirm dialog, using command:

```
cinnamon-session-quit --no-prompt
```

As well, there are `--force` and `--display` options for choice.

## 6\. Log out LXQt via command:

For the LXQt desktop, I can only find the **`lxqt-leave`** command which brings up the confirm window that contains ‘Log out’, ‘Shutdown’, ‘Reboot’, etc.

Also, there’s **`lxqt-leave --logout`** command to show the log-out dialog only.

![[lxqt-logout.webp]]

However,the command does not seem to have an option to skip confirm dialog …

## 7\. Command to log out LXDE:

LXDE has the **lxde-logout** command to bring up the system shutdown menu including log out option.

There’s another command **obsession-logout** that can do similar job by specifying text to display:

```
obsession-logout --prompt="Text to display"
```

Like LXQt, it seems that no option to skip the user confirmation window.
