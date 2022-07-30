1.
 ```

ip a                                                                                                             
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: wlp1s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 28:cd:c4:9e:8f:a5 brd ff:ff:ff:ff:ff:ff
    inet 192.168.137.18/24 brd 192.168.137.255 scope global dynamic noprefixroute wlp1s0
       valid_lft 83645sec preferred_lft 83645sec
    inet6 fe80::d0ea:db4d:d553:834b/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
3: outline-tun0: <NO-CARRIER,POINTOPOINT,MULTICAST,NOARP,UP> mtu 1500 qdisc fq_codel state DOWN group default qlen 500
    link/none 
    inet 10.0.85.1/24 scope global outline-tun0
       valid_lft forever preferred_lft forever
12: enx2c16dbab8bcc: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc fq_codel state DOWN group default qlen 1000
    link/ether 2c:16:db:ab:8b:cc brd ff:ff:ff:ff:ff:ff
    ```
    
```
2. CDP - приоприетарный протокол Cisco
   
   LLDP - открытый протокол 

   lldpd - apt-get install lldpd - поддерживает не только LLDP, но также и CDP, EDP, SONMP и AgentX SNMP.
   
   Еще нашел 'ladvd' - sudo apt install ladvd


3. VLAN - Технология VLAN (Virtual Local Area Network) позволяет создавать и гибко конфигурировать виртуальные сети поверх физической. Это позволяет реализовывать достаточно сложные сетевые конфигурации без покупки дополнительного оборудования и прокладки дополнительных кабелей.
```
auto vlan1400
iface vlan1400 inet static
        address 192.168.1.1
        netmask 255.255.255.0
        vlan_raw_device eth0
```
4. Bonding – это объединение сетевых интерфейсов по определенному типу агрегации, Служит для увеличения пропускной способности и/или отказоустойчивость сети.
![Хорошо все расписано](http://www.adminia.ru/linux-bonding-obiedinenie-setevyih-interfeysov-v-linux/)

Пример настройки интерфейсов eth0 и eth1 в режиме active-backup в файле «/etc/network/interfaces»:
```
auto bond0
iface bond0 inet dhcp
   bond-slaves eth0 eth1
   bond-mode active-backup
   bond-miimon 100
   bond-primary eth0 eth1
```

5. /29 - это 6 адресов IP + 1 для броадкаста + 1 - адрес сети
```
ipcalc 10.10.10.0/29                                                                                         
Address:   10.10.10.0           00001010.00001010.00001010.00000 000
Netmask:   255.255.255.248 = 29 11111111.11111111.11111111.11111 000
Wildcard:  0.0.0.7              00000000.00000000.00000000.00000 111
=>
Network:   10.10.10.0/29        00001010.00001010.00001010.00000 000
HostMin:   10.10.10.1           00001010.00001010.00001010.00000 001
HostMax:   10.10.10.6           00001010.00001010.00001010.00000 110
Broadcast: 10.10.10.7           00001010.00001010.00001010.00000 111
Hosts/Net: 6                     Class A, Private Internet
```
```
>>> 256//8
32
``` 
32 сети получится c с маской /29 подсетей из сети /24
10.10.10.0/29 
10.10.10.8/29
10.10.10.16/29 и т.д. до...
10.10.10.248/29

6. Например 100.64.0.0/10
```
ipcalc 100.64.0.0/10 -s 45                                                                                       
Address:   100.64.0.0           01100100.01 000000.00000000.00000000
Netmask:   255.192.0.0 = 10     11111111.11 000000.00000000.00000000
Wildcard:  0.63.255.255         00000000.00 111111.11111111.11111111
=>
Network:   100.64.0.0/10        01100100.01 000000.00000000.00000000
HostMin:   100.64.0.1           01100100.01 000000.00000000.00000001
HostMax:   100.127.255.254      01100100.01 111111.11111111.11111110
Broadcast: 100.127.255.255      01100100.01 111111.11111111.11111111
Hosts/Net: 4194302               Class A

1. Requested size: 45 hosts
Netmask:   255.255.255.192 = 26 11111111.11111111.11111111.11 000000
Network:   100.64.0.0/26        01100100.01000000.00000000.00 000000
HostMin:   100.64.0.1           01100100.01000000.00000000.00 000001
HostMax:   100.64.0.62          01100100.01000000.00000000.00 111110
Broadcast: 100.64.0.63          01100100.01000000.00000000.00 111111
Hosts/Net: 62                    Class A

Needed size:  64 addresses.
Used network: 100.64.0.0/26
Unused:
100.64.0.64/26
100.64.0.128/25
100.64.1.0/24
100.64.2.0/23
100.64.4.0/22
100.64.8.0/21
100.64.16.0/20
100.64.32.0/19
100.64.64.0/18
100.64.128.0/17
100.65.0.0/16
100.66.0.0/15
100.68.0.0/14
100.72.0.0/13
100.80.0.0/12
100.96.0.0/11
```

7 . 
Windows\Linux: arp

Все хосты Windows arp -a

Удалить 1 хост: arp -d 192.168.1.1

ip neigh flush all   
