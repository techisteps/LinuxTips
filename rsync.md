# Rsync

### Folder sync

Trailing "/" makes difference. 
- If "/" is present then it'll copy content of that folder to the destination location.
- If "/" is NOT present then it'll copy folder to the destination location.

```bash
# Copy folder to /tmp
rsync -a /opt/folder /tmp/
```
Output:
```
/tmp/folder/
```

```bash
# Copy folder contents to /tmp
rsync -a /opt/folder/ /tmp/
```
Output:
```
/tmp/
```
