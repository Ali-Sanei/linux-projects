# Raid 1 rocky linux
### after adding disk 
```bash

lsblk

```
![Alt text](lsblk.jpg)

### see the 2 disk added sdb and sdc.

## Now create partion with fdisk

```bash

fdisk /dev/sdb

```

![Alt text](fdisk1.jpg)

### type 'm' for help
m

![Alt text](fdisk2.jpg)

### As you can see in screenshot for create new partition type n

n 

![Alt text](fdisk3.jpg) 

### Now type 'p' for select primary or press enter

p

### press enter key for defaul partition number

### can type the first sector or press enter for default 

### also for end sector

### type 'm' for show help menu 

![Alt text](fdisk2.jpg)

### As you can see in screenshot for change partition type , type 't'

### if you know hex code for partition type , enter that or you don't know enter " Shift + L " for list 

![Alt text](partition_type.jpg)

### As you can see on screenshot , partition type for raid is marked , that's hex code is "fd" 

fd

#### changed type of partition 'Linux' to 'Linux raid autodetect' 

### press 'w' for write and exit from fdisk enviroment 

## Now create partition for sdc disk

## Create partion with fdisk

```bash

fdisk /dev/sdc

```

![Alt text](fdisk1.jpg)

### type 'm' for help
m

![Alt text](fdisk2.jpg)

### As you can see in screenshot for create new partition type n

n 

![Alt text](fdisk3.jpg) 

### Now type 'p' for select primary or press enter

p

### press enter key for defaul partition number

### can type the first sector or press enter for default 

### also for end sector

### type 'm' for show help menu 

![Alt text](fdisk2.jpg)

### As you can see in screenshot for change partition type , type 't'

### if you know hex code for partition type , enter that or you don't know enter " Shift + L " for list 

![Alt text](partition_type.jpg)

### As you can see on screenshot , partition type for raid is marked , that's hex code is "fd" 

fd

#### changed type of partition 'Linux' to 'Linux raid autodetect' 

### press 'w' for write and  exit from fdisk enviroment 

## install mdadm 

```bash

yum install -y mdadm

``` 
## create array 

```bash

mdadm --create --verbos /dev/md0 level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1 

lsblk

```
![Alt text](end_lsblk.jpg)

# Add disk to array ( add disk to raid)

### after adding disks to system 

```bash

lsblk

```
![Alt text](lsblk2.jpg)

### see the 2 disk added sdd and sde.

## Now create partion with fdisk

```bash

fdisk /dev/sdd

```

![Alt text](fdisk1.jpg)

### type 'm' for help
m

![Alt text](fdisk2.jpg)

### As you can see in screenshot for create new partition type n

n 

![Alt text](fdisk3.jpg) 

### Now type 'p' for select primary or press enter

p

### press enter key for defaul partition number

### can type the first sector or press enter for default 

### also for end sector

### type 'm' for show help menu 

![Alt text](fdisk2.jpg)

### As you can see in screenshot for change partition type , type 't'

### if you know hex code for partition type , enter that or you don't know enter " Shift + L " for list 

![Alt text](partition_type.jpg)

### As you can see on screenshot , partition type for raid is marked , that's hex code is "fd" 

fd

#### changed type of partition 'Linux' to 'Linux raid autodetect' 

### press 'w' for write and exit from fdisk enviroment 

## Now create partition for sde disk

## Create partion with fdisk

```bash

fdisk /dev/sde

```

![Alt text](fdisk1.jpg)

### type 'm' for help
m

![Alt text](fdisk2.jpg)

### As you can see in screenshot for create new partition type n

n 

![Alt text](fdisk3.jpg) 

### Now type 'p' for select primary or press enter

p

### press enter key for defaul partition number

### can type the first sector or press enter for default 

### also for end sector

### type 'm' for show help menu 

![Alt text](fdisk2.jpg)

### As you can see in screenshot for change partition type , type 't'

### if you know hex code for partition type , enter that or you don't know enter " Shift + L " for list 

![Alt text](partition_type.jpg)

### As you can see on screenshot , partition type for raid is marked , that's hex code is "fd" 

fd

#### changed type of partition 'Linux' to 'Linux raid autodetect' 

### press 'w' for write and  exit from fdisk enviroment

## show new partitions 

```bash 

lsblk

```
![Alt text](after-lsblk.jpg) 

## Create a raid 0 with new disks added (sdd1 and sde1) then add exist raid1 disks to the new raid 0 disks 

```bash 

mdadm --create --verbos /dev/md10 level=0 --raid-devices=2 /dev/sdd1 /dev/sde1

```

![Alt text](mdadm1.jpg)

```bash

mdadm --add /dev/md127 /dev/md10

```

![Alt text](mdadm2.jpg)

## Remove md127 

```bash

mdadm --remove /dev/md127 /dev/md10

```
![Alt text](mdadm3.jpg) 

## Remove super block

```bash 

mdadm --stop /dev/md10
mdadm --zero-superblock /dev/sde1 /dev/sdd1 

```
![Alt text](super_block_remove.jpg)









