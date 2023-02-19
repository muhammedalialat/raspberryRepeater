# Rasperry Pi as a WiFi Repeater
Configure your Reaspberry Pi as a wifi repeater. The Raspberry Pi will get a internet connection from the ethernet cable. The onbard WiFi Module will act as an access point which is bridged to the ethernet connection. All WiFi connected devices will reach your network behind the ethernet connection.

Execute `raspi-config` command and go to Advanced Settings and then go to AA Network Config. Select the second option 2. NetworkManager. Confirm and quit raspi-config.

Execute following command as root:

First create a bridge to combin the wifi connection with your ethernet connection. Then create the ethernet and wifi connection seperately.
* `nmcli connection add con-name BridgeCon ifname br0 type bridge ipv4.method auto ipv6.method disabled connection.autoconnect yes stp no`
* `nmcli connection add con-name EthernetCon ifname eth0 type bridge-slave master BridgeCon connection.autoconnect yes`
* `nmcli connection add con-name Hotspot ifname wlan0 type wifi slave-type bridge master BridgeCon wifi.band bg wifi.mode ap wifi.ssid my-hotspot-ssid`

Configure the WiFi Connection to use WPA2 Authentication:
* `nmcli con modify Hotspot 802-11-wireless-security.key-mgmt wpa-psk`
* `nmcli con modify Hotspot 802-11-wireless-security.proto rsn`
* `nmcli con modify Hotspot 802-11-wireless-security.group ccmp`
* `nmcli con modify Hotspot 802-11-wireless-security.pairwise ccmp`
* `nmcli con modify Hotspot 802-11-wireless-security.psk 12345678`
* `nmcli con modify Hotspot ipv4.method shared`
* `nmcli con up Hotspot`

