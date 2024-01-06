---
layout: post
title: "DELL-VxRail Log-Bundle"
categories: [VxRail]
tags: [VMware, DELL, VxRail, Troubleshooting]
---

#### Log-Bundle (Shell)
Das Log-Bundle kann direkt auf dem VxRail Manager erstellt werden und anschließend heruntergeladen werden. 
Entweder man nutzt ssh und verbindet sich direkt mit dem VxRail-Manager oder nutzt die VM Konsole.
Die Anmeldung am VxRail-Manager erfolgt mit dem Benutzer "Mystic". Nach erfolgreicher Anmeldung wechselt man mit su root auf den "root" Benutzer.

Der Pfad zu dem Log-Bundle ist nach der Erstellung -> /tmp/mystic/dc/ 

#### Vollständiges Log-Bundle (beinhaltet VxRail-Manager, vCenter, ESXi, iDRAC, Plattform)

```console
/mystic/generateLogBundle.py
```

#### VxRail Manager Log-Bundle 

```console 
/mystic/generateLogBundle.py -v
```

#### VMware vCenter Log-Bundle

```console
/mystic/generateLogBundle.py -c
```

#### VMware ESXi Log-Bundle

```console
/mystic/generateLogBundle.py -e
```

#### VxRail iDRAC Log-Bundle

```console
/mystic/generateLogBundle.py -i
```

#### VxRail Plattform Log-Bundle

```console
/mystic/generateLogBundle.py -p
```

#### vSAN Witness Log-Bundle

```console
/mystic/generateLogBundle.py -w
```

#### Log-Bundle per vCenter GUI
Alternativ kann das Log-Bundle im vSphere Client erstellt, heruntergeladen und gelöscht werden. 

![Log-Bundle Gui](/assets/2023-12-01-VxRail_Log_Bundle/VxRail Log-Bundle.png)


