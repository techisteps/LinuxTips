# Password


### Change password for user

`root` user can provide password for all user.
users can set their own password. 
```bash
## below command will provide a prompt to set new password
passwd user
```
---


below command will setup give password with out prompt
```bash
# Username lfs
# Password lfspass
usermod --password $(echo lfspass | openssl passwd -1 -stdin) lfs
```
---

### Check users password
Check if given password is correct without using it.  
CMD:
```bash
# Username lfs
# Password lfs
cat /etc/shadow | grep lfs
```
>output:
```
alpinehost:~# cat /etc/shadow | grep lfs
lfs:$1$ia94Nrvd$qEuTjbHepEwJ6xHTNNmQS.:19919::::::
```
In above ":" separated output line, first column defines the username. Second column contains password details in "$" separated manner. 
- First column shows cryptographic option 
- Second column is salt value
- Third column is hashed password

To check cryptographic options, run `openssl passwd --help` command and refer "Cryptographic options:" section.

Now generate the password hash for given string and match with password hash from shadow file.
CMD:
```bash
# check with correct password
openssl passwd -1 -salt ia94Nrvd lfs
# check with wrong password
openssl passwd -1 -salt ia94Nrvd lfspass
```
>output:
```
alpinehost:~# openssl passwd -1 -salt ia94Nrvd lfs
$1$ia94Nrvd$qEuTjbHepEwJ6xHTNNmQS.
alpinehost:~# openssl passwd -1 -salt ia94Nrvd lfspass
$1$ia94Nrvd$z0h/GBXrU.13EaaqB46N80
```




Commands to cover:  
`passwd`  
`chage`  
`pwck`  
`openssl passwd`  