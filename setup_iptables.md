# Setup Iptables

### First, you will need to install iptable

    $ pacman -S iptables

### before start it, don't forget stop and disable firewelld(if you use it)

    $ systemctl disable --now firewelld

### start it using systemctl

    $ systemctl enable --now iptables

### and then modify this script down below

```bash
#!/bin/bash

# step 1: clean rule
iptables -F
iptables -X
iptables -Z

# step 2: policy
iptables -P INPUT DROP
iptables -P OUTPUT ACCEPT
iptables -P FORWARD ACCEPT

# step 3: add input
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT
iptables -A INPUT -p tcp --dport "the port you want to open" -j ACCEPT  # allow other computer access this port
iptables -A INPUT -p icmp -s "souce subnet e.g. 192.168.1.0/24" -j ACCEPT # allow other computer ping this computer

# step 4: add nat
iptables -t nat -F
iptables -t nat -X
iptables -t nat -Z
#if you want to do something like router, uncommand and modify script down below
#iptables -t nat -A POSTROUTING -s "source ip range" -o "output nic" -j MASQUERADE
#iptables -t nat -A PREROUTING -i "input nic" -p tcp -d 192.168.1.0/27 --dport 20 -j DNAT --to-destination 192.168.2.2:20 # i keep this for example
#iptables -t nat -A PREROUTING -i "input nic" -p tcp -d "destination subnet" --dport "range of port e.g. 30000:31000" -j DNAT --to-destination "destination ip:ip range"

# step 5: save to system file
iptables-save > /etc/iptables/iptables.rules

```

### run this script

    $ bash path/of/where/the/script/is.sh

### restart iptable then run

    $ iptables-save

### you will see all rule still there, if you don't just check step 5

### Done.

---

Click here back to [home](./README.md) page.