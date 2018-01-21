# Tune the ev3dev installation

### WLAN config

/etc/network/interfaces.d/wlan0: 
```
allow-hotplug wlan0
auto wlan0
iface wlan0 inet static
  wpa-ssid REPLACED
  wpa-psk REPLACED
  address 192.168.178.80
  netmask 255.255.255.0
  gateway 192.168.178.1
  dns-nameservers 192.168.178.1
  dns-domain fritz.box
  wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
```

/etc/wpa_supplicant/wpa_supplicant.conf:
```
ctrl_interface=/var/run/wpa_supplicant
network={
    ssid="REPLACED"
    scan_ssid=1
    proto=WPA RSN
    key_mgmt=WPA-PSK
    pairwise=CCMP TKIP
    group=CCMP TKIP
    psk=REPLACED
}
```

### Add ssh key for user robot
```
mkdir -p /home/robot/.ssh && \
	echo "YOURPUBLICKEY" >> /home/robot/.ssh/authorized_keys && \
	chown -R robot.robot /home/robot/.ssh && \
	chmod 700 /home/robot/.ssh && \
	chmod 600 /home/robot/.ssh/authorized_keys
```

### Add ssh key for user root
```
mkdir -p /root/.ssh && \
	echo "YOURPUBLICKEY" >> /root/.ssh/authorized_keys && \
	chown -R root.root /root/.ssh && \
	chmod 700 /root/.ssh && \
	chmod 600 /root/.ssh/authorized_keys
```

### I am connecting via WLAN - disable avahi and bluetooth
```
sudo systemctl stop bluetooth && \
	sudo systemctl disable bluetooth
```

```
sudo systemctl stop avahi-daemon && \
	sudo systemctl disable avahi-daemon
```

### I use ssh - remove samba
```
sudo apt-get purge samba && \
	sudo apt-get autoremove
```

### sudo without password
Edit /etc/sudoers
```
# %sudo	ALL=(ALL:ALL) ALL
%sudo	ALL=(ALL) NOPASSWD:ALL
```

