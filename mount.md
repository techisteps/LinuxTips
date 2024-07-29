If while umount getting error as `targer is busy` then:
```bash
# Error
root@jaiserver:~# umount /mnt/usb
umount: /mnt/usb: target is busy.

# Check which process is accessing that location
root@jaiserver:~# lsof /mnt/usb/
COMMAND PID USER   FD   TYPE DEVICE SIZE/OFF  NODE NAME
bash    952 root  cwd    DIR   8,17     4096 27905 /mnt/usb/root
# --- Exited from the bash which was access this location

# Check which process is accessing that location
root@jaiserver:~# lsof /mnt/usb/
# --- None good to umount

root@jaiserver:~# umount /mnt/usb
# --- Success
```
