---
layout: post
title: "DELL-VxRail missing vmk1 idrac issue"
categories: [VxRail]
tags: [VMware, DELL, VxRail]
---
Seit der VxRail Version 7.0.240/241 wurde die interne Kommunikation zwischen VxRail Manager und ISM von PTAgent auf API Port 9090 umgestellt.  
Intern wird dies LinZhi benannt. 

Auschnitt aus einem vxdiag.log
[ip_linzhi] LinZhi is not listening yet (648 ports checked) [bmc] LinZhi IP xxx.xxx.xxx.xxx, Port 9090 

Die Kommunikation ist zwingend erforderlich, da darüber der VxRail Manager den Node überwacht und managed. 

#### Auf folgenden Screenshot existiert der vmk1 
![VxRail-VMK1](/assets/VxRail-vmk1-exist.JPG)

#### Output VxVerify.log

| Warning 201608 | unmap: GuestUnmap Enabled                                                       
| Failure 205769 | idc_swi: idrac queries failed

#### vmk1 nicht existent
![VxRail-VMK01](/assets/VxRail-vmk1-missing.JPG)


Über die ESXi Konsole kann es folgend überprüft werden.

```Shell
/opt/vxrail/tools/ipmitool lan print
```

Could not open device at /dev/ipmi0 or /dev/ipmi/0 or /dev/ipmidev/0: No such file

Dies wird verursacht wenn das IPMI Modul nicht korrekt auf dem ESXi (VxRail-Node) geladen ist.
Dies kann mit folgenden Befehl bestätigt werden.

```Shell
vmkload_mod -l | grep ipmi
```


#### Lösung

1. iDRAC reset
2. IPMI Module manuell laden

```Shell
vmkload_mod ipmi

/etc/init.d/sfcbd-watchdog restart
/etc/init.d/wsman status restart
/etc/init.d/dcism-netmon-watchdog restart
```
