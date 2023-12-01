---
layout: post
title: "VxRail Log-Bundle"
categories: [VxRail]
tags: [VMware, DELL, VxRail, Troubleshooting]
---

#### Log-Bundle per SSH
Das Log-Bundle kann direkt auf dem VxRail Manager erstellt werden und anschließend heruntergeladen werden. 
Der Pfad zu dem Log-Bundle ist nach der Erstellung -> /tmp/mystic/dc/ 

```console
python /mystic/generateLogBundle.py -v
```
#### Log-Bundle per vCenter GUI
Alternativ kann das Log-Bundle über das vCenter und der VxRail Integration erstellt werden. 

#### Log-Bundle Gui
![Log-Bundle Gui](/assets/VxRail Log-Bundle.png)


