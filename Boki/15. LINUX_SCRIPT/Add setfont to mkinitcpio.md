#!/usr/bin/bash

#########################################################################
"#"

tput setaf 2
echo  "####################################################################"
echo  "######  Adding setfont to the binaries to avoid error message "
echo  "######  in /etc/mkinitcpio.conf"
echo  "######  and rebuilding /boot files"
echo  "####################################################################"
tput sgr20
echo

FIND='BINARIES=()'
REPLACE='BINARIES=(setfont)'

FIND='BINARIES=""'
REPLACE='BINARIES=(setfont)'
sudo sed -i "s/$FIND/REPLACE/G" /etc/mkinitcpio.conf

echo
tput setaf 2
echo  "####################################################################"
echo  "######  Mkinitcpio and update-grub"
echo  "####################################################################"
tput sgr0

sudo mkinitcpio -P

sudo grub-nkconfig -o /boot/grub/grub.cfg

echo

