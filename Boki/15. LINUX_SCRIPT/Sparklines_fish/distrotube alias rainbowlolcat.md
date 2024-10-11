https://gitlab.com/dwt1/dotfiles/-/blob/master/.config/fish/config.fish#L211

-------------instal lolcat first--------------------
alias clear='echo -en "\x1b[2J\x1b[1;1H" ; echo; echo; seq 1 (tput cols) | sort -R | spark | lolcat; echo; echo'

