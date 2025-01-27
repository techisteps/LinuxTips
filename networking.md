

`ifconfig` command is deprecated thus now start using `ip` command.


### Setup manually
```bash

# Bring up interface if its down
sudo ip link set eth0 up

# Give manual IP
sudo ip addr add 192.168.1.110/24 dev eth0

# Add default route
sudo ip route add default via 192.168.1.1 dev eth0
```

### Get IP using DHCP (Temporary)
```bash
dhclient
```

>>> Make sure your nameserver entries are present else DNS will now work.

```
cat /etc/resolv.conf
echo 'nameserver 8.8.8.8' >> /etc/resolv.conf
```

### Get IP using DHCP (Permanent)

```bash
# Add below lines to "/etc/network/interfaces"
## - eth0 is interface name
## - alpinehost is hostname of the system
auto eth0
iface eth0 inet dhcp
  hostname alpinehost

# Restart networking service to acquire the IP
rc-service networking restart

### TO-DO: Check if without restarting network service, IP can be acquire.
```

### Few commands

```bash
ip --help
ip link show
ip addr show
#sudo ip route delete 10.0.0.0/24 via 192.168.1.1 dev eth0
sudo ip link set eth0 mtu 1500
watch -n 1 "ip -s link show eth0 | grep 'RX bytes'"
ip -s link show eth0 | grep -E 'errors|dropped'
```


### Install Commands
```bash
# For Alpine
sudo apk add networkmanager-cli
sudo apk add dhclient
sudo apk add networkmanager-tui
```

