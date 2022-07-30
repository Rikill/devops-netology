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
2.
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

5





