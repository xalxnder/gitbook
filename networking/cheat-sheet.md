# Cheat Sheet

* `ip addr`
* `ip route`
* `ip link`&#x20;
* `/etc/sysconfig/network-scripts`  - Config file for the network
* `` /etc/resolv.conf` `` - File used for DNS name server resolving



#### How To Find Available IPs

Need to find availabe IPs in 192.168.235.X?

`nmap -sn 192.168.235.0/24`

```bash
nmap -sn 192.168.235.0/24 | grep "Nmap scan report for" | awk '{print $5}' > used.txt
comm -23 <(seq 1 254 | sed 's/^/192.168.1./' | sort) <(sort used.txt)

```

```bash
# See IPs being used
nmap -sn 192.168.235.0/24 -oG - | awk '/Up$/{print $2}'

```
