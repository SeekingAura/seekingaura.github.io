---
title: Partition resize
permalink: /docs/dev_notes/linux_server-debian_based/disk/partition_resize/
toc: true
---


This guide will give example about how resize case

# Get info about disk and partitions
To manage partitions, check how the disks are configured on your system. With that information, you can make a plan and make decisions.

## Get Current partitions structure
To get how the partitions are structured run the next command 
```shell
sudo lsblk --output NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL,MODEL,PATH
```

example output
```
NAME                      FSTYPE       SIZE MOUNT LABEL MODEL                          PATH
sda                                    100G             Virtual disk                   /dev/sda
├─sda1                                   1M                                            /dev/sda1
├─sda2                    ext4           2G /boot                                      /dev/sda2
└─sda3                    LVM2_member   49G                                            /dev/sda3
  └─ubuntu--vg-ubuntu--lv ext4          49G /                                          /dev/mapper/ubuntu--vg-ubuntu--lv
sr0                                   1024M             VMware Virtual SATA CDRW Drive /dev/sr0
```

The first level is **device**, second level is **Partition** and the third level is **Volume partition**, on the example are 2 devices **sda** is disk and **sr0** is something like a CD

## Get LV Paths (lvs alternative)
The LV Path is required for the next commands for disk resize operations over Logical Volumes that already exist
```shell
sudo lvs --all --options lv_path,devices
```

example output
```
Path                     Devices     
/dev/ubuntu-vg/ubuntu-lv /dev/sda3(0)
```

**NOTE:** With `lsblk` command we can get the LV path, but there is an alternative for command that uses LVS command
{: .notice}

# Manage partition
## Resize Partition
In some cases, there is free disk space, and we want to increase the size of one or more partitions (as in the [Get Current partitions structure](#get-current-partitions-structure) example). To do that, we will use `parted` on the `sda` device with the remaining free space. 

Execute `parted` with the `/dev/sda` path that corresponds to the `sda` device.
```shell
sudo parted /dev/sda
```

When this is executed, the shell will show this at the beginning.
```
(parted)
```

For this example, we will resize partition 3 to use 100% of the remaining space.
```
(parted) resizepart 3 100%
```

Then you can check with `lsblk` command the new disk status

# Manage Volume
## Resize Volume
If the partition has available storage, you can resize the volumes that are already there. For this example, we will resize sda3 with all the remaining partition space (example case after the [Resize Partition](#resize-partition) is done).

```shell
sudo pvresize /sda/sda3
```

for specific resize run
```shell
sudo pvresize --setphysicalvolumesize 10G /dev/sda3
```

## Extend logical Volume
Now, if the volume where the Logical Volume is located has free space, we can extend the volume with the remaining space using the following command. (example case after the [Resize Partition](#resize-volume) is done).

```shell
sudo lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
```

## Resize file system of new space from LV 
Once volume is extended their space can not be used for file system, for that requires do execute for example case `resize2fs`
```shell
sudo resize2fs /dev/ubuntu-vg/ubuntu-lv
```

For other file systems have specific command and parameters

