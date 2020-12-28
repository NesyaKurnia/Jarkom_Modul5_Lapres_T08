## Lapres Jarkom Modul5 Kelompok T08
### Anggota Kelompok :
1. Kadek Nesya Kurniadewi (05311840000009)
2. Agung Mulyono (05311840000035)

### Topologi Jaringan
### Menggunakan Metode VLSM
### Command IP Tables
```
iptables 1
iptables -t nat -A POSTROUTING -s 192.168.0.0/16 -o eth0 -j SNAT --to-source 10.151.74.74 #surabaya

iptables 2
iptables -A FORWARD -d 10.151.83.144/29 -i eth0 -p tcp --dport 22 -j DROP #surabaya

iptables 3
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP #malang dan mojokerto

iptables 4
iptables -A INPUT -s 192.168.0.0/24 -m time --timestart 07:00 --timestop 17:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -s 192.168.0.0/24 -j REJECT #malang

iptables 5
iptables -A INPUT -s 192.168.1.0/24 -m time --timestart 06:59 --timestop 16:59 -j REJECT #malang

iptables 6
#surabaya
iptables -t nat -A PREROUTING -p tcp -d 10.151.83.146 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.168.2.11:80
iptables -t nat -A PREROUTING -p tcp -d 10.151.83.146 -j DNAT --to-destination 192.168.2.10:80

iptables 7
#surabaya
iptables -N LOGGING
iptables -A FORWARD -j LOGGING
iptables -A OUTPUT -j LOGGING
iptables -A LOGGING -j LOG --log-prefix "IPTables-Dropped: " --log-level 4
iptables -A LOGGING -j DROP

#malang
iptables -N LOGGING
iptables -A INPUT -j LOGGING
iptables -A OUTPUT -j LOGGING
iptables -A LOGGING -j LOG --log-prefix "IPTables-Dropped: " --log-level 4
iptables -A LOGGING -j DROP

#mojokerto
iptables -N LOGGING
iptables -A INPUT -j LOGGING
iptables -A OUTPUT -j LOGGING
iptables -A LOGGING -j LOG --log-prefix "IPTables-Dropped: " --log-level 4
iptables -A LOGGING -j DROP
```
