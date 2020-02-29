Turtoial from https://lala.im/3684.html
### Some scripts
Parastor;123
ifconfig

```
vi /etc/ocserv/ocserv.conf
echo -e "net.ipv4.ip_forward=1" >> /etc/sysctl.conf && sysctl -p
vi /etc/sysctl.conf
iptables -t nat -I POSTROUTING -s 192.168.1.0/24 -o eno1 -j MASQUERADE
iptables -t nat -A POSTROUTING -j MASQUERADE

iptables -D INPUT -p tcp --dport 10089 -j ACCEPT
iptables -D OUTPUT -p udp --dport 10089 -j ACCEPT
iptables -I IN_public_allow -p udp --dport 10089 -j ACCEPT
iptables -I IN_public_allow -p tcp --dport 10089 -j ACCEPT

sysctl -w net.ipv4.ip_forward=1

vi /etc/dnsmasq.conf
service dnsmasq restart

systemctl start ocserv
```
