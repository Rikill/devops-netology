1.
```
route-views>show ip route 79.139.215.17   
Routing entry for 79.139.128.0/17
  Known via "bgp 6447", distance 20, metric 0
  Tag 2497, type external
  Last update from 202.232.0.2 7w0d ago
  Routing Descriptor Blocks:
  * 202.232.0.2, from 202.232.0.2, 7w0d ago
      Route metric is 0, traffic share count is 1
      AS Hops 3
      Route tag 2497
      MPLS label: none



route-views>show bgp 79.139.215.17     
BGP routing table entry for 79.139.128.0/17, version 307607026
Paths: (24 available, best #22, table default)
  Not advertised to any peer
  Refresh Epoch 1
  701 3356 8359 25513
    137.39.3.55 from 137.39.3.55 (137.39.3.55)
      Origin IGP, localpref 100, valid, external
      path 7FE0313B4B90 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3356 8359 25513
    4.68.4.46 from 4.68.4.46 (4.69.184.201)
      Origin IGP, metric 0, localpref 100, valid, external
      Community: 0:151 3356:2 3356:22 3356:100 3356:123 3356:519 3356:903 3356:2094 8359:100 8359:5500 8359:55277
      path 7FE1764B0188 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3267 1299 8359 25513
    194.85.40.15 from 194.85.40.15 (185.141.126.1)
      Origin IGP, metric 0, localpref 100, valid, external
      path 7FE0BFD9FB30 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  57866 3356 8359 25513
    37.139.139.17 from 37.139.139.17 (37.139.139.17)
      Origin IGP, metric 0, localpref 100, valid, external
      Community: 0:151 3356:2 3356:22 3356:100 3356:123 3356:519 3356:903 3356:2094 8359:100 8359:5500 8359:55277
      path 7FE129161A88 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  53767 174 174 3356 8359 25513
    162.251.163.2 from 162.251.163.2 (162.251.162.3)
      Origin IGP, localpref 100, valid, external
      Community: 174:21000 174:22013 53767:5000
      path 7FE15E6B8C48 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  20912 3257 3356 8359 25513
    212.66.96.126 from 212.66.96.126 (212.66.96.126)
      Origin IGP, localpref 100, valid, external
      Community: 3257:8070 3257:30515 3257:50001 3257:53900 3257:53902 20912:65004
      path 7FE1650E18C8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  19214 3257 3356 8359 25513
    208.74.64.40 from 208.74.64.40 (208.74.64.40)
      Origin IGP, localpref 100, valid, external
      Community: 3257:8108 3257:30048 3257:50002 3257:51200 3257:51203
      path 7FE0829B23C8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  6939 8359 25513
    64.71.137.241 from 64.71.137.241 (216.218.252.164)
      Origin IGP, localpref 100, valid, external
      path 7FE1877E2DB8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  1351 8359 8359 25513
    132.198.255.253 from 132.198.255.253 (132.198.255.253)
      Origin IGP, localpref 100, valid, external
      path 7FE1777048A8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  20130 6939 8359 25513
    140.192.8.16 from 140.192.8.16 (140.192.8.16)
      Origin IGP, localpref 100, valid, external
      path 7FE0AEEA0428 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3333 8359 25513
    193.0.0.56 from 193.0.0.56 (193.0.0.56)
      Origin IGP, localpref 100, valid, external
      Community: 0:151 8359:100 8359:5500 8359:55277
      path 7FE11E3217C0 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  4901 6079 8359 25513
    162.250.137.254 from 162.250.137.254 (162.250.137.254)
      Origin IGP, localpref 100, valid, external
      Community: 65000:10100 65000:10300 65000:10400
      path 7FE14DF061C0 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  7018 3356 8359 25513
    12.0.1.63 from 12.0.1.63 (12.0.1.63)
      Origin IGP, localpref 100, valid, external
      Community: 7018:5000 7018:37232
      path 7FE14F624838 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  101 3356 8359 25513
    209.124.176.223 from 209.124.176.223 (209.124.176.223)
      Origin IGP, localpref 100, valid, external
      Community: 0:151 101:20100 101:20110 101:22100 3356:2 3356:22 3356:100 3356:123 3356:519 3356:903 3356:2094 8359:100 8359:5500 8359:55277
      Extended Community: RT:101:22100
      path 7FE09C5B3250 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  49788 12552 8359 25513
    91.218.184.60 from 91.218.184.60 (91.218.184.60)
      Origin IGP, localpref 100, valid, external
      Community: 12552:12000 12552:12100 12552:12101 12552:22000
      Extended Community: 0x43:100:1
      path 7FE0EAC7BA60 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  852 3356 8359 25513
    154.11.12.212 from 154.11.12.212 (96.1.209.43)
      Origin IGP, metric 0, localpref 100, valid, external
      path 7FE10192D330 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  8283 8359 25513
    94.142.247.3 from 94.142.247.3 (94.142.247.3)
      Origin IGP, metric 0, localpref 100, valid, external
      Community: 0:151 8283:1 8283:101 8359:100 8359:5500 8359:55277
      unknown transitive attribute: flag 0xE0 type 0x20 length 0x18
        value 0000 205B 0000 0000 0000 0001 0000 205B
              0000 0005 0000 0001 
      path 7FE109678968 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3549 3356 8359 25513
    208.51.134.254 from 208.51.134.254 (67.16.168.191)
      Origin IGP, metric 0, localpref 100, valid, external
      Community: 0:151 3356:2 3356:22 3356:100 3356:123 3356:519 3356:903 3356:2094 3549:2581 3549:30840 8359:100 8359:5500 8359:55277
      path 7FE094F095A8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  7660 2516 1299 8359 25513
    203.181.248.168 from 203.181.248.168 (203.181.248.168)
      Origin IGP, localpref 100, valid, external
      Community: 2516:1030 7660:9003
      path 7FE162414E90 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3561 3910 3356 8359 25513
    206.24.210.80 from 206.24.210.80 (206.24.210.80)
      Origin IGP, localpref 100, valid, external
      path 7FE0FC206F90 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3303 8359 25513
    217.192.89.50 from 217.192.89.50 (138.187.128.158)
      Origin IGP, localpref 100, valid, external
      Community: 0:151 3303:1004 3303:1006 3303:1030 3303:3054 8359:100 8359:5500 8359:55277
      path 7FE1263C7CA8 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 3
  2497 8359 25513
    202.232.0.2 from 202.232.0.2 (58.138.96.254)
      Origin IGP, localpref 100, valid, external, best
      path 7FE0EF49BD80 RPKI State not found
      rx pathid: 0, tx pathid: 0x0
  Refresh Epoch 1
  1221 4637 8359 25513
    203.62.252.83 from 203.62.252.83 (203.62.252.83)
      Origin IGP, localpref 100, valid, external
      path 7FE164D82208 RPKI State not found
      rx pathid: 0, tx pathid: 0
  Refresh Epoch 1
  3257 3356 8359 25513
    89.149.178.10 from 89.149.178.10 (213.200.83.26)
      Origin IGP, metric 10, localpref 100, valid, external
      Community: 3257:8794 3257:30043 3257:50001 3257:54900 3257:54901
      path 7FE02C697AB0 RPKI State not found
      rx pathid: 0, tx pathid: 0
```
2.
```
??? modprobe -v dummy numdummies=2
insmod /lib/modules/5.4.0-122-generic/kernel/drivers/net/dummy.ko numdummies=0 numdummies=2

???   lsmod | grep dummy
dummy                  16384  0

???  ip a | grep dummy
13: dummy0: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN group default qlen 1000
14: dummy1: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN group default qlen 1000

??? ip addr add 192.168.1.1/24 dev dummy0

??? ip a | grep dummy                    
13: dummy0: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN group default qlen 1000
    inet 192.168.1.1/24 scope global dummy0
14: dummy1: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN group default qlen 1000

???  ifconfig dummy0
dummy0: flags=195<UP,BROADCAST,RUNNING,NOARP>  mtu 1500
        inet 192.168.1.1  netmask 255.255.255.0  broadcast 0.0.0.0
        inet6 fe80::68c9:89ff:fee6:7fc  prefixlen 64  scopeid 0x20<link>
        ether 6a:c9:89:e6:07:fc  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 4  bytes 280 (280.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
???????????? ?????? ???????????????? Dummy ???????????????????? ?????? ???????????????? ???????????????? ??????????:
```
auto dummy0
iface dummy0 inet static
address 192.168.1.1
netmask 255.255.255.0
```
3.
```
ss -at | grep 25                                                                                              
ESTAB     0      0        192.168.137.18:51716     198.252.206.25:https         
ESTAB     0      0        192.168.137.18:51254      52.98.207.194:imaps         
```

4
```
 ss -au                                                                                                           
State                  Recv-Q                 Send-Q                                                      Local Address:Port                                          Peer Address:Port                   Process                 
UNCONN                 0                      0                                                           127.0.0.53%lo:domain                                         0.0.0.0:*                                              
ESTAB                  0                      0                                                   192.168.137.18%wlp1s0:bootpc                                    192.168.137.1:bootps                                         
UNCONN                 0                      0                                                                 0.0.0.0:sunrpc                                              0.0.0.0:*                                              
UNCONN                 0                      0                                                                 0.0.0.0:49608                                               0.0.0.0:*                                              
UNCONN                 0                      0                                                                 0.0.0.0:631                                                 0.0.0.0:*                                              
UNCONN                 0                      0                                                                 0.0.0.0:mdns                                                0.0.0.0:*                                              
UNCONN                 0                      0                                                                    [::]:40875                                                  [::]:*                                              
UNCONN                 0                      0                                                                    [::]:sunrpc                                                 [::]:*                                              
UNCONN                 0                      0                                      [fe80::d0ea:db4d:d553:834b]%wlp1s0:dhcpv6-client                                          [::]:*                                              
UNCONN                 0                      0                                                                    [::]:mdns                                                   [::]:* 
```

5.
![?????? ???????????????? ???????? ???? ??????????????](https://i.imgur.com/8YZpmEJ.png)

