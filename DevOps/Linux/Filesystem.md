# Filesystem

```
// Display filesystem type
▶ df -T
▶ df -T | awk '{print $1,$2,$NF}' | grep "^/dev"

▶ mount | grep "^/dev"
▶ sudo file -sL /dev/sda1
▶ cat /etc/fstab
```

## Ext

Ext3 add journaling to Ext2. Ext3 has 2TB file size limit. Most modern system use Ext4 which has 6TB limit.