---
layout: post
title: "DELL-VxRail RASR Reset"
categories: [VxRail]
tags: [VMware, DELL, VxRail]
---

#### VxRail RASR
Um einen VxRail-Node in den Auslieferungszustand zu versetzen, ist es notwendig, einen RASR-Reset durchzuführen. 
Ein RASR-Rest löscht alle Daten und Einstellungen. Notwendig ist dies, wenn zum Beispiel die initiale Installation fehlschlägt.


#### VxRail RASR-Reset 1
Boot in den Boot Manager -> F11 
![Rasr-Schritt1](/assets/vxrail/VxRail-Rasr-1.jpg)

#### VxRail RASR-Reset 2
One-shot UEFI Boot Menu auswählen
![Rasr-Schritt2](/assets/vxrail/VxRail-Rasr-2.jpg)

#### VxRail RASR-Reset 3
Internal SD: auswählen
![Rasr-Schritt3](/assets/vxrail/VxRail-Rasr-3.jpg)

#### VxRail RASR-Reset 4
Factory Reset mit F auswählen
![Rasr-Schritt4](/assets/vxrail/VxRail-Rasr-4.jpg)

#### VxRail RASR-Reset 5
Mit "Yes" bestätigen 
Anschließend muss mit "Disconnect" bestätigt werden, dass alle externen Storage Devices (FC, iSCSI etc.) entfernt wurden.
![Rasr-Schritt5](/assets/vxrail/VxRail-Rasr-5.jpg)




