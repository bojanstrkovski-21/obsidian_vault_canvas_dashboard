[Unit]
Description=/etc/net-start_default Compatibility
ConditionPathExists=/etc/net-start_default

[Service]
Type=forking
ExecStart=/etc/net-start_default start
TimeoutSec=0
StandardOutput=tty
RemainAfterExit=yes
SysVStartPriority=99

[Install]
WantedBy=graphical.target
