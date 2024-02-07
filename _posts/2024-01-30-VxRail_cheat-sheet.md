---
layout: post
title: "DELL-VxRail Cheat-Sheet"
categories: [VxRail]
tags: [VMware, DELL, VxRail, Troubleshooting]
---

#### Standard Passwörter

Component      | Username | Default Password           | Network (Default)
--------       | -------- | --------                   | --------
iDRAC          | root     | calvin                     | DHCP
ESXi root      | root     | Passw0rd!                  | DHCP
VxRail Manager | mystic   | VxRailManager@201602!      | 192.168.10.200
VxRail Manager | root     | Passw0rd!                  | 192.168.10.200

#### Loudmouth Services

```ESXi
/etc/init.d/loudmouth [start|stop|status|restart]
```

```VxRail  Manager
systemctl [start|stop|status|restart] vmware-loudmouth
```
 

#### Zeit 

```ESXi 
esxcli system time get 
esxcli system time set d|–day -H|–hour -m|–min -M|–month -s|–sec -y|–year
```

```VxRail Manager
date
date -s “30 JAN 2024 12:30:00”
```

#### VxRail Manager IP-Einstellung

```ESXi
vxrail-primary --config --vxrail-address XXX.XXX.XXX.XXX --vxrail-netmask XXX.XXX.XXX.XXX --vxrail-gateway XXX.XXX.XXX.XXX
```

#### VxRail Manager 

```ESXi
esxcli vm process list

vim-cmd vmsvc/getallvms
vim-cmd vmsvc/power.shutdown vmid
vim-cmd vmsvc/power.getstate vmid
vim-cmd vmsvc/power.on vmid
vim-cmd vmsvc/power.getstate vmid

/usr/lib/vmware-loudmouth/bin/loudmouthc query | grep -o "applianceID=..............." | sort
```

#### VxRail Manager Installation-Logs

```VxRail Manager
cat dayone.log
tail -f dayone.log
tail -f dayone.log | grep ERROR
tail -n 100 dayone.log
more dayone.log
```