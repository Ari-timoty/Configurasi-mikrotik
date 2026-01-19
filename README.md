# Configurasi-mikrotik
# Konfigurasi Dasar MikroTik (Sekali 


## Konfigurasi Lengkap
```bash
/system identity set name=MikroTik-TKJ

/ip address add address=192.168.10.1/24 interface=ether2

/ip dns set servers=8.8.8.8,1.1.1.1 allow-remote-requests=yes

/ip dhcp-client add interface=ether1 disabled=no

/ip firewall nat add chain=srcnat out-interface=ether1 action=masquerade

/ip pool add name=pool-lan ranges=192.168.10.10-192.168.10.100

/ip dhcp-server add name=dhcp-lan interface=ether2 address-pool=pool-lan disabled=no

/ip dhcp-server network add address=192.168.10.0/24 gateway=192.168.10.1 dns-server=8.8.8.8,1.1.1.1

/ip firewall filter add chain=input connection-state=established,related action=accept
/ip firewall filter add chain=input connection-state=invalid action=drop
/ip firewall filter add chain=input in-interface=ether1 action=drop
