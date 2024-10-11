
ln -s /usr/lib/systemd/system/NetworkManager.service airootfs/etc/systemd/system/multi-user.target.wants/NetworkManager.service

ln -s /usr/lib/systemd/system/NetworkManager-dispatcher.service airootfs/etc/systemd/system/dbus-org.freedesktop.nm-dispatcher.service


ln -s /usr/lib/systemd/system/NetworkManager-wait-online.service airootfs/etc/systemd/system/network-online.target.wants/NetworkManager-wait-online.service


ln -s /usr/lib/systemd/system/sddm.service airootfs/etc/systemd/system/display-manager.service



