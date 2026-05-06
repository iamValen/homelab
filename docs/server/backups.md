There's a CRON job that backs up important [[VMs]] to a separate dataset.

In case of [[TrueNAS]] I don't want it to backup the full drives I added to it so I added the option `backup=0` to the VM config after each disk:
```c 
...
scsi0: local-lvm:vm-106-disk-0,iothread=1,size=32G
scsi1: /dev/disk/by-id/ata-ST4000VN006-3CW104_ZW63H2FB,size=3907018584K,backup=0
scsi2: /dev/disk/by-id/ata-ST4000VN006-3CW104_ZW63H2M7,size=3907018584K.backup=0
...
``` 


