---
created: 2024-03-06T11:15:21 (UTC +01:00)
tags: []
source: https://faun.pub/the-easiest-way-to-install-dwm-43bbf668ea83
author: Prinux
---

# The easiest way to install DWM!! | FAUN — Developer Community 🐾

## **Why I use DWM?**

It leaves nearly 100% of the screen real estate for me to **use**. It starts almost instantly on my underpowered desktop. It perfectly mirrors my own personal usage patterns: I do not ever want to manually resize or move a window if I don’t have to. I usually have least two windows open side-by-side.Very low system requirements and usage.Below are few customized DWM setups from Reddit:-

## What is DWM ?

The suckless developers created DWM, which stands for dynamic window manager. It’s a tiling window manager with a minimalist design. It takes less than 500MB of RAM and only a few processes when it first starts up. First and foremost, there is only one correct way to install dwm and other Suckless tools: from source (either straight from suckless.org , or from your own build, or from someone else’s build, though I wouldn’t recommend that unless you really trust the person) and compile it yourself.

## Dependencies for DWM

-   **On Arch Linux:**  
    `sudo pacman -S base-devel libx11 libxft libxinerama freetype2 fontconfig`
-   **On Debian:**  
    `sudo apt install build-essential libx11-dev libxft-dev libxinerama-dev libfreetype6-dev libfontconfig1-dev`
-   **On OpenBSD:**  
    if Xenocara is installed, dependencies are already met.
-   **On Void Linux (case sensitive):**  
    `sudo xbps-install base-devel libX11-devel libXft-devel libXinerama-devel freetype-devel fontconfig-devel`

## How to install DWM

Here i have already installed Arch and gnome in it, hence i also have a Display manager and will be explaining , on how to start dwm using startx.

**step1: Clone**

As a result, the first step in installing DWM is to clone the github source from suckless or anyone else. Let’s now create a directory for all of the repositories(You may call your directory whatever you wish)

```
<span id="6ab9" data-selectable-paragraph="">mkdir .suckless<br>cd .suckless</span>
```

Now lets clone the repository required for our build , here for simplicity we will be using st as the default terminal. You can change your preferred terminal in config.h file in the dwm directory.

```
<span id="6414" data-selectable-paragraph="">git clone https://git.suckless.org/dwm</span><span id="80f3" data-selectable-paragraph="">git clone https://git.suckless.org/st</span><span id="beca" data-selectable-paragraph="">git clone https://git.suckless.org/dmenu</span>
```

**step 2 : Compiling the code**

Now to need to go the dwm , st and dmenu directory to `make` and then run `sudo make insatall`. For making it easier for you , you can copy the code below and run it in your terminal.

```
<span id="1c44" data-selectable-paragraph="">cd .suckless<br>cd dwm<br>make<br>sudo make clean install<br>cd..</span><span id="d6f4" data-selectable-paragraph="">cd st<br>make<br>sudo make clean install</span><span id="a807" data-selectable-paragraph="">cd ..<br>cd dmenu<br>make<br>sudo make clean install`</span><span id="31cc" data-selectable-paragraph="">cd</span>
```

**step 3 :Starting dwm**

If you’re using startx, simply add exec /usr/local/bin/dwm at the end of your .xinitrc file on Linux, or at the end of your .xsession file on OpenBSD.

## How to use DWM in a display manager ?

But if your using a display manager , you don’t need to do this. Instead you’ll need to create a .desktop file for dwm, with this content:

```
<span id="8ac7" data-selectable-paragraph="">[Desktop Entry]<br>Encoding=UTF-8<br>Name=Dwm<br>Comment=Dynamic window manager<br>Exec=/usr/local/bin/dwm<br>Icon=dwm<br>Type=XSession</span>
```

Put that file in /usr/share/xsessions. If dwm refuses to start, change the full path (/usr/local/bin/dwm) to simply dwm.  
And you’re all set.

## A few to tips to my younger self.

I’ve made a few mistakes that caused me to reinstall dwm from scratch, so make a backup of all your dwm files before you start tweaking and applying any patches.

## Use git

Git is a great tool for version control, but don’t forget to add and commit files as you make changes, and don’t be lazy because it can save you a lot of time and effort when things go wrong.

## In case if you don’t know , how to use git

For initializing git use `git init` and then use the command `git add .` for adding all the files in a current repository and then use the git commit command along -m flag with a message for committing the staged files . Example `git commit -m "DWM version 1"`.
