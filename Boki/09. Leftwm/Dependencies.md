- xorg (runtime, build): specifically libx11, xrandr, xorg-server, libxinerama
- sh (runtime): any posix-compliant shell for starting up and down files
- rust (build): >= 1.65.0
- bash (optional): Most of the themes available use bash, though the scripts maybe converted to any posix-compliant shell
- feh
List of common dependencies for themes:

|Dependency  <br>(git)|Ubuntu 20.4.1  <br>_sudo apt install {}_|Arch  <br>_sudo pacman -S {}_|Fedora 33  <br>_sudo dnf install {}_|PKGS|
|---|---|---|---|---|
|[feh](https://github.com/derf/feh)|feh|feh|feh|[feh](https://pkgs.org/search/?q=feh&on=provides)|
|[compton](https://github.com/chjj/compton)|compton|picom|compton|[compton](https://pkgs.org/download/compton)|
|[picom](https://github.com/yshui/picom)|manual **|picom|picom|[picom](https://pkgs.org/download/picom)|
|[polybar](https://github.com/polybar/polybar)|manual **|polybar|polybar|[polybar](https://pkgs.org/download/polybar)|
|[xmobar](https://github.com/jaor/xmobar)|xmobar|xmobar|xmobar|[xmobar](https://pkgs.org/download/xmobar)|
|[lemonbar](https://github.com/LemonBoy/bar)|lemonbar|paru -S lemonbar*|manual **|[lemonbar](https://pkgs.org/download/lemonbar)|
|[conky](https://github.com/brndnmtthws/conky)|conky|conky|conky|[conky](https://pkgs.org/download/conky)|
|[dmenu](https://git.suckless.org/dmenu)|dmenu|dmenu|dmenu|[dmenu](https://pkgs.org/download/dmenu)|

> * You can use whichever AUR wrapper you like. See [paru](https://github.com/Morganamilo/paru) and [yay](https://github.com/Jguer/yay).  
> ** See the git page (link in first column) for how to install these manually