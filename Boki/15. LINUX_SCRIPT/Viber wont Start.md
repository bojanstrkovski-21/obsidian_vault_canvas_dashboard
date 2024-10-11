 
Terminal:
install viber from pacman (sudo pacman -S viber)  or aur (yay -S viber / paru -S viber)
Run in Terminal: QT_STYLE_OVERRIDE="" viber (or create Alias in your bashrc/fishrc...)
alias viber='QT_STYLE_OVERRIDE="" viber'

Flatpak:
install flatseal from flathub.org (flatpak install flathub com.github.tchx84.Flatseal)
install viber from flathub.org (flatpak install flathub com.viber.Viber)
Add  the line - QT_STYLE_OVERRIDE=Fusion - in Flatseal => Enironment => Variables