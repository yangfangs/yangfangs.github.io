---
layout: post
title: Linux 命令行挂载 U 盘
categories: Linux
description: 挂载U盘
keywords: U盘, Linux
---

  在使用 Linux OS(Fedora)　时候，会碰到内核版本更新后无法进入　KDE　桌面的情况，需要重新编译下最新显卡驱动，无法进入桌面只能进入命令行模式进行操作,　使用 `Ctrl+Alt+F2`　进入一个终端，需要用一个　U盘 来拷贝一个最新的　N　卡驱动到本地，那么如何挂载一个外置硬盘或者 U盘 呢，记录一下挂载方法


### 1.需要Root权限

```bash
su
********

```

### 2.在 `/mnt` 下建一个需要挂载的文件夹

* 这里就命名为 USB　为例

```bash
mkdir /mnt/USB

```


### 3.使用　`fdisk -l` 查看磁盘分区情况和 U盘位置



```bash
[root@localhost mnt] # fdisk -l
Disk /dev/sda: 1.8 TiB, 2000398934016 bytes, 3907029168 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0xa4456369

Device     Boot     Start        End    Sectors   Size Id Type
/dev/sda1            2048 3907028991 3907026944   1.8T  f W95 Ext'd (LBA)
/dev/sda5            4096  419670015  419665920 200.1G  7 HPFS/NTFS/exFAT
/dev/sda6       419672064  838866943  419194880 199.9G  7 HPFS/NTFS/exFAT
/dev/sda7  *    838868992  839892991    1024000   500M 83 Linux
/dev/sda8       839895040 3907028991 3067133952   1.4T 8e Linux LVM




Disk /dev/sdb: 29.8 GiB, 32017047552 bytes, 62533296 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x83f9dd74

Device     Boot Start      End  Sectors  Size Id Type
/dev/sdb1  *     2048 62531583 62529536 29.8G  7 HPFS/NTFS/exFAT


Disk /dev/mapper/fedora-root: 50 GiB, 53687091200 bytes, 104857600 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes


Disk /dev/mapper/fedora-swap: 7.8 GiB, 8388608000 bytes, 16384000 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes


Disk /dev/mapper/fedora-home: 1.4 TiB, 1508288495616 bytes, 2945875968 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes


```

* 在这里面可以看到各个分区的的挂载情况
* 插入U盘再次执行 `fdisk -l`

```bash
[root@localhost mnt] # fdisk -l
Disk /dev/sda: 1.8 TiB, 2000398934016 bytes, 3907029168 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disklabel type: dos
Disk identifier: 0xa4456369

Device     Boot     Start        End    Sectors   Size Id Type
/dev/sda1            2048 3907028991 3907026944   1.8T  f W95 Ext'd (LBA)
/dev/sda5            4096  419670015  419665920 200.1G  7 HPFS/NTFS/exFAT
/dev/sda6       419672064  838866943  419194880 199.9G  7 HPFS/NTFS/exFAT
/dev/sda7  *    838868992  839892991    1024000   500M 83 Linux
/dev/sda8       839895040 3907028991 3067133952   1.4T 8e Linux LVM




Disk /dev/sdb: 29.8 GiB, 32017047552 bytes, 62533296 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x83f9dd74

Device     Boot Start      End  Sectors  Size Id Type
/dev/sdb1  *     2048 62531583 62529536 29.8G  7 HPFS/NTFS/exFAT


Disk /dev/mapper/fedora-root: 50 GiB, 53687091200 bytes, 104857600 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes


Disk /dev/mapper/fedora-swap: 7.8 GiB, 8388608000 bytes, 16384000 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes


Disk /dev/mapper/fedora-home: 1.4 TiB, 1508288495616 bytes, 2945875968 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes


Disk /dev/sdg: 14.6 GiB, 15614803968 bytes, 30497664 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xcad4ebea

Device     Boot Start      End  Sectors  Size Id Type
/dev/sdg4  *      256 30497663 30497408 14.6G  c W95 FAT32 (LBA)


```

* 会发现再最后没多了一个 14.6 GB 的分区，这个就是刚插入的 U盘 驱动是 `/dev/sdg4`　这就需要挂载到 USB　下使用的位置


### 4.使用 `mount` 挂载


* 挂载

```bash

mount -t vfat /dev/sdg4 /mnt/USB

```

* 可以查看挂载上的　U盘

```bash
ls -la /mnt/USB/

drwxr-xr-x   5 root root      8192 Jul 11  2015 boot
-rwxr-xr-x   1 root root    395268 Jul 11  2015 bootmgr
-rwxr-xr-x   1 root root   1152864 Jul 11  2015 bootmgr.efi


```
* 也可以进入挂载的 U盘的目录

```bash
cd /mnt/USB/

```

### ５．使用 `unmount`　卸载　U盘

* 为了避免直接拔出　U盘　可能造成文件丢失，使用完了需要卸载一下

```bash
umount /mnt/USB

```

*若提示　U盘繁忙

```bash
umount: /mnt/USB: target is busy
        (In some cases useful info about processes that
         use the device is found by lsof(8) or fuser(1).)

```

* 执行 ｀cd ../..｀　再卸载
