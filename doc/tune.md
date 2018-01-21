# Tune the ev3dev installation

### WLAN config

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
´´´
sudo systemctl stop bluetooth && \
	sudo systemctl disable bluetooth
´´´

´´´
sudo systemctl stop avahi-daemon && \
	sudo systemctl disable avahi-daemon
´´´

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

