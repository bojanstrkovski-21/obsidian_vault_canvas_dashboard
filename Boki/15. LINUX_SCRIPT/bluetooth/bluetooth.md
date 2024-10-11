sudo systemctl enable bluetooth
sudo systemctl start bluetooth

#!/usr/bin/env bash

"$CONNECTED" = $(bluetoothctl -- info 0A:83:B4:AB:A3:1B | grep Connected)
if ["$CONNECTED" = " Connected: no"]; then
pactl load-module module-bluetooth-discover
bluetoothctl -- connect 0A:83:B4:AB:A3:1B
else
bluetoothctl -- disconnect 0A:83:B4:AB:A3:1B
fi

sudo systemctl enable --now smb
sudo systemctl enable --now nmb
