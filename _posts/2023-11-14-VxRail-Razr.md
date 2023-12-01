---
layout: post
title: "DELL-VxRail RASR Reset"
categories: [VxRail]
tags: [VMware, DELL, VxRail]
---

#### VxRail Rasr 
Um einen VxRail-Node in den Auslieferungszustand zu versetzen, ist es notwendig, einen RASR-Reset durchzuführen. 
Ein RASR-Rest löscht alle Daten und Einstellungen. Notwendig ist dies, wenn zum Beispiel die initiale Installation fehlschlägt.

#### Schritt 1
Boot in den Boot Manager -> F11 

#### VxRail Rasr Schritt 1
![Rasr-Schritt1](/assets/vxrail/VxRail-Rasr-1.jpg)

#### Schritt 2
One-shot UEFI Boot Menu auswählen

#### VxRail Rasr Schritt 2
![Rasr-Schritt2](/assets/vxrail/VxRail-Rasr-2.jpg)

#### Schritt 3
Internal SD: auswählen

#### VxRail Rasr Schritt 3
![Rasr-Schritt3](/assets/vxrail/VxRail-Rasr-3.jpg)

#### Schritt 4
F auswählen für Factory Reset

#### VxRail Rasr Schritt 4
![Rasr-Schritt4](/assets/vxrail/VxRail-Rasr-4.jpg)


#### Schritt 5
Mit "Yes" bestätigen 
Anschließend muss mit "Disconnect" bestätigt werden, dass alle externen Storage Devices (FC, iSCSI etc.) entfernt wurden.

#### VxRail Rasr Schritt 5
![Rasr-Schritt5](/assets/vxrail/VxRail-Rasr-5.jpg)




