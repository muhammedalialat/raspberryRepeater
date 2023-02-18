
nmcli connection add con-name BridgeCon ifname br0 type bridge ipv4.method auto ipv6.method disabled connection.autoconnect yes stp no
nmcli connection add con-name EthernetCon ifname eth0 type bridge-slave master BridgeCon connection.autoconnect yes
nmcli connection add con-name Hotspot ifname wlan0 type wifi slave-type bridge master BridgeCon wifi.band bg wifi.mode ap wifi.ssid my-hotspot-ssid

nmcli con modify Hotspot 802-11-wireless-security.key-mgmt wpa-psk
nmcli con modify Hotspot 802-11-wireless-security.proto rsn
nmcli con modify Hotspot 802-11-wireless-security.group ccmp
nmcli con modify Hotspot 802-11-wireless-security.pairwise ccmp
nmcli con modify Hotspot 802-11-wireless-security.psk 12345678
nmcli con modify Hotspot ipv4.method shared
nmcli con up Hotspot

