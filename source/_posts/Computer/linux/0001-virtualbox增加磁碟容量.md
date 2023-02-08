---
title: "virtualbox增加磁碟容量"
date: 2023-02-09 03:55:36
tags:
  - virtualbox
  - linux
categories:
  - Linux
cover: https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTw8aprugTcnSd3UYoL1M51DLb8efKKYZkubFcZQv7fHclZxxXCqclgofZVO_N2RNvUekg&usqp=CAU
feature: true
---

# virtualbox 增加磁碟容量

- [https://www.itread01.com/content/1541161203.html](https://www.itread01.com/content/1541161203.html)

## 1. 新增一個虛擬硬碟


![](https://trello-attachments.s3.amazonaws.com/5e61ca986670c26011a76758/1181x799/b5894f661a74d256bb7e65c342709051/image.png)




## 2. Root權限



```bash
(base) [cabie@centosclean installation]$ sudo -i
[sudo] password for cabie: 
```




## 3. 檢視磁碟情況



```bash
[root@centosclean ~]# fdisk -l /dev/sda

Disk /dev/sda: 42.9 GB, 42949672960 bytes, 83886080 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O 大小 (最小/最佳化)：512 位元組 / 512 位元組
Disk label type: dos
磁碟識別碼：0x000cbc97

所用裝置 開機      開始         結束      區塊   識別號  系統
/dev/sda1   *        2048     2099199     1048576   83  Linux
/dev/sda2         2099200    83886079    40893440   8e  Linux LVM

```

### :bulb:  注意: 新增的是```/dev/sdb```，是sd"b" 。

```bash
[root@centosclean ~]# fdisk -l

Disk /dev/sdb: 16.1 GB, 16106127360 bytes, 31457280 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O 大小 (最小/最佳化)：512 位元組 / 512 位元組


Disk /dev/sda: 42.9 GB, 42949672960 bytes, 83886080 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O 大小 (最小/最佳化)：512 位元組 / 512 位元組
Disk label type: dos
磁碟識別碼：0x000cbc97

所用裝置 開機      開始         結束      區塊   識別號  系統
/dev/sda1   *        2048     2099199     1048576   83  Linux
/dev/sda2         2099200    83886079    40893440   8e  Linux LVM

Disk /dev/mapper/centos-root: 37.7 GB, 37706792960 bytes, 73646080 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O 大小 (最小/最佳化)：512 位元組 / 512 位元組


Disk /dev/mapper/centos-swap: 4160 MB, 4160749568 bytes, 8126464 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O 大小 (最小/最佳化)：512 位元組 / 512 位元組


```



```bash
[root@centosclean ~]# df -lh
檔案系統                 容量  已用  可用 已用% 掛載點
devtmpfs                 1.9G     0  1.9G    0% /dev
tmpfs                    1.9G     0  1.9G    0% /dev/shm
tmpfs                    1.9G  8.6M  1.9G    1% /run
tmpfs                    1.9G     0  1.9G    0% /sys/fs/cgroup
/dev/mapper/centos-root   36G   19G   17G   52% /
/dev/sda1               1014M  184M  831M   19% /boot
tmpfs                    379M     0  379M    0% /run/user/1000
```



## 4. 讀取新磁碟



```bash
[root@centosclean ~]# fdisk /dev/sdb
Welcome to fdisk (util-linux 2.23.2).

Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table
Building a new DOS disklabel with disk identifier 0x0705f895.

命令 (m 以獲得說明)：n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
分割區編號 (1-4, default 1): 1
起初 sector (2048-31457279, 預設 2048)：
使用預設值 2048
最後 sector, +sectors 或 +大小{K,M,G} (2048-31457279, 預設 31457279)：
使用預設值 31457279
Partition 1 of type Linux and of size 15 GiB is set





命令 (m 以獲得說明)：t
Selected partition 1
Hex code (type L to list all codes): 8e
Changed type of partition 'Linux' to 'Linux LVM'






命令 (m 以獲得說明)：w
分割表已變更！

呼叫 ioctl() 以重新讀取分割表。
同步磁碟。
```



## 5. 重新開機


```bash
[root@centosclean ~]# reboot
```

```bash
(base) [cabie@centosclean installation]$ sudo -i
[sudo] password for cabie: 
```



## 6. 查看



```bash
[root@centosclean ~]# vgdisplay
  --- Volume group ---
  VG Name               centos
  System ID             
  Format                lvm2
  Metadata Areas        1
  Metadata Sequence No  3
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               2
  Max PV                0
  Cur PV                1
  Act PV                1
  VG Size               <39.00 GiB
  PE Size               4.00 MiB
  Total PE              9983
  Alloc PE / Size       9982 / 38.99 GiB
  Free  PE / Size       1 / 4.00 MiB
  VG UUID               vhAZPX-lI1Z-0uay-vv9r-sEZm-tb80-5KyRWK
   
```

- 多出了```sdb1```
```bash
[root@centosclean ~]# ls /dev
autofs           fd            network_latency     sdb       tty11  tty26  tty40  tty55  ttyS3    vcsa3
block            full          network_throughput  sdb1      tty12  tty27  tty41  tty56  uhid     vcsa4
bsg              fuse          null                sg0       tty13  tty28  tty42  tty57  uinput   vcsa5
btrfs-control    hpet          nvram               sg1       tty14  tty29  tty43  tty58  urandom  vcsa6
bus              hugepages     oldmem              sg2       tty15  tty3   tty44  tty59  usbmon0  vfio
cdrom            hwrng         port                shm       tty16  tty30  tty45  tty6   usbmon1  vga_arbiter
centos           initctl       ppp                 snapshot  tty17  tty31  tty46  tty60  vcs      vhci
char             input         ptmx                snd       tty18  tty32  tty47  tty61  vcs1     vhost-net
console          kmsg          pts                 sr0       tty19  tty33  tty48  tty62  vcs2     zero
core             log           random              stderr    tty2   tty34  tty49  tty63  vcs3
cpu              loop-control  raw                 stdin     tty20  tty35  tty5   tty7   vcs4
cpu_dma_latency  mapper        rtc                 stdout    tty21  tty36  tty50  tty8   vcs5
crash            mcelog        rtc0                tty       tty22  tty37  tty51  tty9   vcs6
disk             mem           sda                 tty0      tty23  tty38  tty52  ttyS0  vcsa
dm-0             mqueue        sda1                tty1      tty24  tty39  tty53  ttyS1  vcsa1
dm-1             net           sda2                tty10     tty25  tty4   tty54  ttyS2  vcsa2
[root@centosclean ~]# 
[root@centosclean ~]# pvcreate /dev/sdb1
  Physical volume "/dev/sdb1" successfully created.
[root@centosclean ~]# 
[root@centosclean ~]# vgextend centos /dev/sdb1
  Volume group "centos" successfully extended
```



```bash
[root@centosclean ~]# lvdisplay
  --- Logical volume ---
  LV Path                /dev/centos/swap
  LV Name                swap
  VG Name                centos
  LV UUID                KWpCoV-UFx5-MfKl-31L3-vwlh-ONB3-Xhny1e
  LV Write Access        read/write
  LV Creation host, time centosclean, 2018-07-19 23:44:39 +0800
  LV Status              available
  # open                 2
  LV Size                <3.88 GiB
  Current LE             992
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:1
   
  --- Logical volume ---
  LV Path                /dev/centos/root
  LV Name                root
  VG Name                centos
  LV UUID                2nKCA4-S6Jt-5HYf-8k4f-ndPn-IUg9-4VrO9m
  LV Write Access        read/write
  LV Creation host, time centosclean, 2018-07-19 23:44:40 +0800
  LV Status              available
  # open                 1
  LV Size                <35.12 GiB
  Current LE             8990
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:0
   
```



## 7. 延伸磁碟



```bash
[root@centosclean ~]# lvextend /dev/centos/root /dev/sdb1
  Size of logical volume centos/root changed from <35.12 GiB (8990 extents) to 50.11 GiB (12829 extents).  Logical volume centos/root successfully resized.







[root@centosclean ~]# xfs_growfs /dev/centos/root
meta-data=/dev/mapper/centos-root isize=512    agcount=4, agsize=2301440 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=0 spinodes=0
data     =                       bsize=4096   blocks=9205760, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
log      =internal               bsize=4096   blocks=4495, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
data blocks changed from 9205760 to 13136896
```




## 8. 查看是否增加容量



```bash
[root@centosclean ~]# lvscan
  ACTIVE            '/dev/centos/swap' [<3.88 GiB] inherit
  ACTIVE            '/dev/centos/root' [50.11 GiB] inherit




[root@centosclean ~]# df -h
檔案系統                 容量  已用  可用 已用% 掛載點
devtmpfs                 1.9G     0  1.9G    0% /dev
tmpfs                    1.9G     0  1.9G    0% /dev/shm
tmpfs                    1.9G  8.6M  1.9G    1% /run
tmpfs                    1.9G     0  1.9G    0% /sys/fs/cgroup
/dev/mapper/centos-root   51G   19G   32G   37% /
/dev/sda1               1014M  184M  831M   19% /boot
tmpfs                    379M     0  379M    0% /run/user/1000
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkwNzQwNjc4NV19
-->