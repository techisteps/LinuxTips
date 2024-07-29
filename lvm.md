# LVM (Logical Volume Manager)

``` mermaid
block-beta
  columns 5
  blockArrowId0<["File Systems"]>(right)
  fs1["/root"]:1
  fs2["/swap"]:1
  fs3["/home"]:1
  fs4[" "]:1


  blockArrowId1<["Logical Volumns"]>(right)
  lv1["/dev/vg0/lv_root"]:1
  lv2["/dev/vg0/lv_swap"]:1
  lv3["/dev/vg0/lv_home"]:1
  lv4["Free"]:1


  blockArrowId2<["Volumn Group"]>(right):1
  vg1["VG"]:2
  vg2["VG"]:2

  
  blockArrowId3<["Physical Volumns"]>(right)
  block:pv1:2
    p1[("/dev/sda1")] p2[("/dev/sda2")]
  end  
  block:pv2:2
    p3[("/dev/sdb1")]    
  end

  
  blockArrowId4<["Partitions"]>(right)
  block:diskpart1:2
    dp1[("/dev/sda1")] dp2[("/dev/sda2")]
  end
  block:diskpart2:2
    dp3[("/dev/sdb1")]    
  end


  blockArrowId5<["Hard Drives"]>(right)
  block:disk:4
    d1[("/dev/sda")] d2[("/dev/sdb")]
  end


  classDef disk fill:#000,stroke:#666,stroke-width:4px
  class d1,d2 disk

  classDef diskpart fill:#735400,stroke:#333,stroke-width:4px
  class dp1,dp2,dp3 diskpart
  
  classDef lvs fill:#bbf,stroke:#f66,stroke-width:2px,color:#fff,stroke-dasharray: 5 5
  class lv1,lv2,lv3 lvs
```


## Check if using LVM
```bash
cat /etc/fstab
```
>>> `/dev/vg0/lv_root`        /       ext4    rw,relatime 0 1  
>>> UUID=5d8ed2fd-1d33-4a7a-b948-89f1073874f6       /boot   ext4    rw,relatime 0 2  
>>> `/dev/vg0/lv_swap`        swap    swap    defaults        0 0  
>>> /dev/cdrom      /media/cdrom    iso9660 noauto,ro 0 0  
>>> /dev/usbdisk    /media/usb      vfat    noauto  0 0  
>>> tmpfs   /tmp    tmpfs   nosuid,nodev    0       0  


```bash
lsblk
# Also check `lsblk -f`
```
>>> NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS  
>>> sda               8:0    0    2G  0 disk  
>>> ├─sda1            8:1    0  300M  0 part /boot  
>>> └─sda2            8:2    0  1.7G  0 part  
>>>   ├─vg0-lv_swap 253:0    0  512M  0 `lvm`  [SWAP]  
>>>   └─vg0-lv_root 253:1    0  1.2G  0 `lvm`  /  
>>> sdb               8:16   0    2G  0 disk  
>>> sdc               8:32   0    1G  0 disk  
>>> sr0              11:0    1 1024M  0 rom  

```bash
# Also check 
lsblk -f
df -h
```
Above highlighted text gives indication.


## LVM Operations

You can create a partition and create a PV from it or you can use complete drive for it.

```bash

# Create PV from complete disk
pvcreate /dev/sdb
```

or

```bash
# Create one or two partitions
fdisk /dev/sdb
# For them as ext4
mkfs.ext4 /dev/sdb1
mkfs.ext4 /dev/sdb2
# Create PV from partitions
pvcreate /dev/sdb1
pvcreate /dev/sdb2
```

#### CMD
```bash
pvdisplay | grep "PV Name"
```
#### Output
```
  PV Name               /dev/sda2
  PV Name               /dev/sdb1
  PV Name               /dev/sdb2
```

#### CMD
```bash
vgdisplay | grep "VG Name"
```
#### Output
```
  VG Name               vg0
```

#### CMD
```bash
alpinehost:~# df -h | grep vg0
```
#### Output
```
/dev/vg0/lv_root  1.2G   74M  1.1G   7% /
```
#### CMD
```bash
alpinehost:~# vgdisplay | grep "Free"
```
#### Output
```
  Free  PE / Size       0 / 0
```
#### CMD
```bash
alpinehost:~# vgextend vg0 /dev/sdb1
```
#### Output
```
  Volume group "vg0" successfully extended
```
#### CMD
```bash
alpinehost:~# vgextend vg0 /dev/sdb2
```
#### Output
```
  Volume group "vg0" successfully extended
```
#### CMD
```bash
alpinehost:~# df -h | grep vg0
```
#### Output
```
/dev/vg0/lv_root  1.2G   74M  1.1G   7% /
```

#### CMD
```bash
alpinehost:~# vgdisplay | grep "Free"
```
#### Output
```
  Free  PE / Size       510 / 1.99 GiB
```

#### CMD
```bash
alpinehost:~# vgs
```
#### Output
```
  VG  #PV #LV #SN Attr   VSize  VFree
  vg0   3   2   0 wz--n- <3.70g 1.99g
```

#### CMD
```bash
alpinehost:~# vgscan
```
#### Output
```
  Found volume group "vg0" using metadata type lvm2
```

```
# alpinehost:~# vgreduce vg0 /dev/sdb1
#   Removed "/dev/sdb1" from volume group "vg0"
# alpinehost:~# vgreduce vg0 /dev/sdb2
#   Removed "/dev/sdb2" from volume group "vg0"
```

#### CMD
```bash
alpinehost:~# lvresize --extents +100 /dev/vg0/lv_root
```
#### Output
```
  Size of logical volume vg0/lv_root changed from 2.20 GiB (564 extents) to 2.59 GiB (664 extents).
  Logical volume vg0/lv_root successfully resized.
```


#### CMD
```bash
apk add e2fsprogs-extra
resize2fs /dev/vg0/lv_root
```
#### Output
```

```







#### CMD
```bash
alpinehost:~# df -h | grep vg0
```
#### Output
```
/dev/vg0/lv_root  2.6G   76M  2.4G   4% /
```

#### CMD
```bash
```
#### Output
```
```


alpinehost:~# lvextend --size +1G /dev/vg0/lv_root
  Size of logical volume vg0/lv_root changed from 1.20 GiB (308 extents) to 2.20 GiB (564 extents).
  Logical volume vg0/lv_root successfully resized.


alpinehost:~# lvextend --resizefs --extents +100%FREE /dev/vg0/lv_root
  LV /dev/mapper/vg0-lv_root mounted at / may have been renamed (from /dev/vg0/lv_root).
  File system resizing not supported: fs utilities do not support renamed devices.
alpinehost:~#












```bash
# Get all lvm commands list
lvm

# Display information about a logical volume
lvdisplay
# Display volume group information
vgdisplay
#Display various attributes of physical volume(s)
pvdisplay
```


