
<!-- ![](assets/images/lvm.png) -->


```mermaid
block-beta
  columns 4
  a["LVM"]:4

  block:group1:3
    columns 2
    h i j k
  end

  g

  block:test1:4
    columns 4
    aa["LVM"]
    block:test2
        columns 2
        hh ii jj kk
    end    
  end

  block:group2:4
    %% columns auto (default)
    sa[("/dev/sda")] sb[("/dev/sdb")] sc[("/dev/sdc")] sd[("/dev/sdd")]
  end

  classDef db fill:#636,stroke:#333,stroke-width:4px
  class sa,sb,sc,sd db
  
  style a fill:#bbf,stroke:#f66,stroke-width:2px,color:#fff,stroke-dasharray: 5 5

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

Above highlighted text gives indication.


## Commands



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


