1. Sparce - изучил
2. Нет, не могут т.к. HardLink - это по сути своей ссылка на тот же самый файл+тот же самы inod - права будут одинаковые.
3. Получилось
```
vagrant@vagrant:~$ lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0                       7:0    0 61.9M  1 loop /snap/core20/1328
loop1                       7:1    0 67.2M  1 loop /snap/lxd/21835
loop2                       7:2    0 43.6M  1 loop /snap/snapd/14978
sda                         8:0    0   64G  0 disk 
├─sda1                      8:1    0    1M  0 part 
├─sda2                      8:2    0  1.5G  0 part /boot
└─sda3                      8:3    0 62.5G  0 part 
  └─ubuntu--vg-ubuntu--lv 253:0    0 31.3G  0 lvm  /
sdb                         8:16   0  2.5G  0 disk 
sdc                         8:32   0  2.5G  0 disk 
```
4. 
```
fdisk /dev/sdb

Command (m for help): n
Partition type
  p   primary (0 primary, 0 extended, 4 free)
  e   extended (container for logical partitions)
Select (default p):

Using default response p.
Partition number (1-4, default 1):
First sector (2048-5242879, default 2048):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-5242879, default 5242879): +2G

Created a new partition 1 of type 'Linux' and of size 2 GiB.

Command (m for help): n
Partition type
  p   primary (1 primary, 0 extended, 3 free)
  e   extended (container for logical partitions)
Select (default p):

Using default response p.
Partition number (2-4, default 2):
First sector (4196352-5242879, default 4196352):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (4196352-5242879, default 5242879):
.............................
Created a new partition 2 of type 'Linux' and of size 511 MiB.

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```
Получили диск sdb1 - 2 ГБ + sdb2 511M
```
vagrant@vagrant:~$ lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0                       7:0    0 61.9M  1 loop /snap/core20/1328
loop1                       7:1    0 67.2M  1 loop /snap/lxd/21835
loop2                       7:2    0 43.6M  1 loop /snap/snapd/14978
loop3                       7:3    0   47M  1 loop /snap/snapd/16292
loop4                       7:4    0   62M  1 loop /snap/core20/1581
loop5                       7:5    0 67.8M  1 loop /snap/lxd/22753
sda                         8:0    0   64G  0 disk 
├─sda1                      8:1    0    1M  0 part 
├─sda2                      8:2    0  1.5G  0 part /boot
└─sda3                      8:3    0 62.5G  0 part 
  └─ubuntu--vg-ubuntu--lv 253:0    0 31.3G  0 lvm  /
sdb                         8:16   0  2.5G  0 disk 
├─sdb1                      8:17   0    2G  0 part 
└─sdb2                      8:18   0  511M  0 part 
sdc                         8:32   0  2.5G  0 disk 
```

5. 
```
vagrant@vagrant:~$ sudo sfdisk -d /dev/sdb | sudo sfdisk /dev/sdc
Checking that no-one is using this disk right now ... OK

Disk /dev/sdc: 2.51 GiB, 2684354560 bytes, 5242880 sectors
Disk model: VBOX HARDDISK   
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes

>>> Script header accepted.
>>> Script header accepted.
>>> Script header accepted.
>>> Script header accepted.
>>> Created a new DOS disklabel with disk identifier 0xa788ba1b.
/dev/sdc1: Created a new partition 1 of type 'Linux' and of size 2 GiB.
/dev/sdc2: Created a new partition 2 of type 'Linux' and of size 511 MiB.
/dev/sdc3: Done.

New situation:
Disklabel type: dos
Disk identifier: 0xa788ba1b

Device     Boot   Start     End Sectors  Size Id Type
/dev/sdc1          2048 4196351 4194304    2G 83 Linux
/dev/sdc2       4196352 5242879 1046528  511M 83 Linux

The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```
```
vagrant@vagrant:~$ lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0                       7:0    0 61.9M  1 loop /snap/core20/1328
loop1                       7:1    0 67.2M  1 loop /snap/lxd/21835
loop2                       7:2    0 43.6M  1 loop /snap/snapd/14978
loop3                       7:3    0   47M  1 loop /snap/snapd/16292
loop4                       7:4    0   62M  1 loop /snap/core20/1581
loop5                       7:5    0 67.8M  1 loop /snap/lxd/22753
sda                         8:0    0   64G  0 disk 
├─sda1                      8:1    0    1M  0 part 
├─sda2                      8:2    0  1.5G  0 part /boot
└─sda3                      8:3    0 62.5G  0 part 
  └─ubuntu--vg-ubuntu--lv 253:0    0 31.3G  0 lvm  /
sdb                         8:16   0  2.5G  0 disk 
├─sdb1                      8:17   0    2G  0 part 
└─sdb2                      8:18   0  511M  0 part 
sdc                         8:32   0  2.5G  0 disk 
├─sdc1                      8:33   0    2G  0 part 
└─sdc2                      8:34   0  511M  0 part 
```
6.
```
vagrant@vagrant:~$ sudo mdadm --create --verbose /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1
mdadm: Note: this array has metadata at the start and
    may not be suitable as a boot device.  If you plan to
    store '/boot' on this device please ensure that
    your boot-loader understands md/v1.x metadata, or use
    --metadata=0.90
mdadm: size set to 2094080K
Continue creating array? y
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md0 started.

vagrant@vagrant:~$ lsblk
NAME                      MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
loop0                       7:0    0 61.9M  1 loop  /snap/core20/1328
loop1                       7:1    0 67.2M  1 loop  /snap/lxd/21835
loop2                       7:2    0 43.6M  1 loop  /snap/snapd/14978
loop3                       7:3    0   47M  1 loop  /snap/snapd/16292
loop4                       7:4    0   62M  1 loop  /snap/core20/1581
loop5                       7:5    0 67.8M  1 loop  /snap/lxd/22753
sda                         8:0    0   64G  0 disk  
├─sda1                      8:1    0    1M  0 part  
├─sda2                      8:2    0  1.5G  0 part  /boot
└─sda3                      8:3    0 62.5G  0 part  
  └─ubuntu--vg-ubuntu--lv 253:0    0 31.3G  0 lvm   /
sdb                         8:16   0  2.5G  0 disk  
├─sdb1                      8:17   0    2G  0 part  
│ └─md0                     9:0    0    2G  0 raid1 
└─sdb2                      8:18   0  511M  0 part  
sdc                         8:32   0  2.5G  0 disk  
├─sdc1                      8:33   0    2G  0 part  
│ └─md0                     9:0    0    2G  0 raid1 
└─sdc2                      8:34   0  511M  0 part  
vagrant@vagrant:~$ 
```
7.
```
vagrant@vagrant:~$ sudo mdadm --create --verbose /dev/md1 --level=0 --raid-devices=2 /dev/sdb2 /dev/sdc2
mdadm: chunk size defaults to 512K
mdadm: Defaulting to version 1.2 metadata
mdadm: array /dev/md1 started.
vagrant@vagrant:~$ lsblk 
NAME                      MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
loop0                       7:0    0 61.9M  1 loop  /snap/core20/1328
loop1                       7:1    0 67.2M  1 loop  /snap/lxd/21835
loop2                       7:2    0 43.6M  1 loop  /snap/snapd/14978
loop3                       7:3    0   47M  1 loop  /snap/snapd/16292
loop4                       7:4    0   62M  1 loop  /snap/core20/1581
loop5                       7:5    0 67.8M  1 loop  /snap/lxd/22753
sda                         8:0    0   64G  0 disk  
├─sda1                      8:1    0    1M  0 part  
├─sda2                      8:2    0  1.5G  0 part  /boot
└─sda3                      8:3    0 62.5G  0 part  
  └─ubuntu--vg-ubuntu--lv 253:0    0 31.3G  0 lvm   /
sdb                         8:16   0  2.5G  0 disk  
├─sdb1                      8:17   0    2G  0 part  
│ └─md0                     9:0    0    2G  0 raid1 
└─sdb2                      8:18   0  511M  0 part  
  └─md1                     9:1    0 1018M  0 raid0 
sdc                         8:32   0  2.5G  0 disk  
├─sdc1                      8:33   0    2G  0 part  
│ └─md0                     9:0    0    2G  0 raid1 
└─sdc2                      8:34   0  511M  0 part  
  └─md1                     9:1    0 1018M  0 raid0 
```
8.
```
vagrant@vagrant:~$ sudo pvcreate /dev/md0 /dev/md1
  Physical volume "/dev/md0" successfully created.
  Physical volume "/dev/md1" successfully created.
```
9.
```
vagrant@vagrant:~$ sudo vgcreate vg0 /dev/md0 /dev/md1
  Volume group "vg0" successfully created

vagrant@vagrant:~$ sudo vgs -a
  VG        #PV #LV #SN Attr   VSize   VFree 
  ubuntu-vg   1   1   0 wz--n- <62.50g 31.25g
  vg0         2   0   0 wz--n-  <2.99g <2.99g
```
10.
```
vagrant@vagrant:~$ sudo lvcreate -L 100M vg0 /dev/md1
  Logical volume "lvol0" created.
```
11.
```
vagrant@vagrant:~$ sudo mkfs.ext4 /dev/vg0/lvol0 
mke2fs 1.45.5 (07-Jan-2020)
Creating filesystem with 25600 4k blocks and 25600 inodes

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (1024 blocks): done
Writing superblocks and filesystem accounting information: done
```
12.
```
vagrant@vagrant:~$ sudo mount /dev/vg0/lvol0 /tmp/new/
```
13.
```
vagrant@vagrant:~$ wget https://mirror.yandex.ru/ubuntu/ls-lR.gz
--2022-07-23 14:00:10--  https://mirror.yandex.ru/ubuntu/ls-lR.gz
Resolving mirror.yandex.ru (mirror.yandex.ru)... 213.180.204.183, 2a02:6b8::183
Connecting to mirror.yandex.ru (mirror.yandex.ru)|213.180.204.183|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 23196510 (22M) [application/octet-stream]
Saving to: ‘ls-lR.gz’

ls-lR.gz                                                          100%[============================================================================================================================================================>]  22.12M  6.67MB/s    in 3.3s    

2022-07-23 14:00:14 (6.67 MB/s) - ‘ls-lR.gz’ saved [23196510/23196510]

vagrant@vagrant:~$ sudo mv ls-lR.gz /tmp/new/
vagrant@vagrant:~$ la -lah /tmp/new/
total 23M
drwxr-xr-x  3 root    root    4.0K Jul 23 14:00 .
drwxrwxrwt 12 root    root    4.0K Jul 23 13:58 ..
drwx------  2 root    root     16K Jul 23 13:57 lost+found
-rw-rw-r--  1 vagrant vagrant  23M Jul 23 11:46 ls-lR.gz
```
14.
```
vagrant@vagrant:~$ lsblk 
NAME                      MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
loop0                       7:0    0 61.9M  1 loop  /snap/core20/1328
loop1                       7:1    0 67.2M  1 loop  /snap/lxd/21835
loop2                       7:2    0 43.6M  1 loop  /snap/snapd/14978
loop3                       7:3    0   47M  1 loop  /snap/snapd/16292
loop4                       7:4    0   62M  1 loop  /snap/core20/1581
loop5                       7:5    0 67.8M  1 loop  /snap/lxd/22753
sda                         8:0    0   64G  0 disk  
├─sda1                      8:1    0    1M  0 part  
├─sda2                      8:2    0  1.5G  0 part  /boot
└─sda3                      8:3    0 62.5G  0 part  
  └─ubuntu--vg-ubuntu--lv 253:0    0 31.3G  0 lvm   /
sdb                         8:16   0  2.5G  0 disk  
├─sdb1                      8:17   0    2G  0 part  
│ └─md0                     9:0    0    2G  0 raid1 
└─sdb2                      8:18   0  511M  0 part  
  └─md1                     9:1    0 1018M  0 raid0 
    └─vg0-lvol0           253:1    0  100M  0 lvm   /tmp/new
sdc                         8:32   0  2.5G  0 disk  
├─sdc1                      8:33   0    2G  0 part  
│ └─md0                     9:0    0    2G  0 raid1 
└─sdc2                      8:34   0  511M  0 part  
  └─md1                     9:1    0 1018M  0 raid0 
    └─vg0-lvol0           253:1    0  100M  0 lvm   /tmp/new
```
15. Ok
16. 
```
vagrant@vagrant:~$ sudo pvmove /dev/md1 /dev/md0
  /dev/md1: Moved: 88.00%

vagrant@vagrant:~$ 
```
17.
```
vagrant@vagrant:~$ sudo mdadm /dev/md0 --fail /dev/sdc1
mdadm: set /dev/sdc1 faulty in /dev/md0
```
18.
```
vagrant@vagrant:~$ dmesg | grep md0
[ 1840.861205] md/raid1:md0: not clean -- starting background reconstruction
[ 1840.861208] md/raid1:md0: active with 2 out of 2 mirrors
[ 1840.861234] md0: detected capacity change from 0 to 2144337920
[ 1840.862795] md: resync of RAID array md0
[ 1851.002738] md: md0: resync done.
[ 3289.018270] md/raid1:md0: Disk failure on sdc1, disabling device.
               md/raid1:md0: Operation continuing on 1 devices.
```
19.
```
vagrant@vagrant:~$ gzip -t /tmp/new/ls-lR.gz && echo $?
0
```
20.
```
▒▓    ~/Documents/Learning/vagrant ▓▒░ sudo vagrant destroy                                                                                                                                                             ░▒▓ ✔  took 56m 18s   at 17:11:24  ▓▒░
[sudo] password for rikill:         
Sorry, try again.
[sudo] password for rikill:         
    default: Are you sure you want to destroy the 'default' VM? [y/N] y
==> default: Forcing shutdown of VM...
==> default: Destroying VM and associated drives...
░▒▓    ~/Documents/Learning/vagrant ▓▒░       
```































