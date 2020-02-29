Turtoial from https://lala.im/3684.html
### Some scripts

Parastor;123


```
ifconfig
```
to get the current machine router name. Usually is en0.
```
vi /etc/ocserv/ocserv.conf
echo -e "net.ipv4.ip_forward=1" >> /etc/sysctl.conf && sysctl -p
vi /etc/sysctl.conf
```
view the ip forward command is applied into the machine
```
iptables -I FORWARD -p tcp --tcp-flags SYN,RST SYN -j TCPMSS --clamp-mss-to-pmtu
iptables -t nat -I POSTROUTING -s 192.168.1.0/24 -o eno1 -j MASQUERADE
iptables -t nat -A POSTROUTING -j MASQUERADE
```
Some rules to proxy the Openvpn to the local machine ip.
```
iptables -I INPUT -p tcp --dport 10089 -j ACCEPT
iptables -I OUTPUT -p udp --dport 10089 -j ACCEPT

```
Regular machine INPUT OUTPUT iptables rules.
```
iptables -I IN_public_allow -p udp --dport 10089 -j ACCEPT
iptables -I IN_public_allow -p tcp --dport 10089 -j ACCEPT

#to remove 

iptables -D IN_public_allow -p udp --dport 10089 -j ACCEPT
iptables -D IN_public_allow -p tcp --dport 10089 -j ACCEPT
```
Suitable for paratrix server iptables rules.

```
sysctl -w net.ipv4.ip_forward=1
```
Enable the system way for ipv4 forward.
```
ocserv -f -d 1
```
Testing and debug

```
systemctl start ocserv
```
To toally start the service.

```
vi /etc/dnsmasq.conf
service dnsmasq restart
```
This command usually restart the dns router inside the machine
