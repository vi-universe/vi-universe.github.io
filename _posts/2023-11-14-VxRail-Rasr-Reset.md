---
layout: post
title: "DELL-VxRail RASR Reset"
categories: [VxRail]
tags: [VMware, DELL, VxRail]
---

#### VxRail RASR
Um einen VxRail-Node in den Auslieferungszustand zu versetzen, ist es notwendig, einen RASR-Reset durchzuführen. 
Ein RASR-Reset löscht alle Daten und Einstellungen. Notwendig ist dies, wenn zum Beispiel die initiale Installation fehlschlägt.


#### VxRail RASR-Reset 1
Boot in den Boot Manager -> F11 
![Rasr-Schritt1](/assets/vxrail/vxrail-rasr1.JPG)

#### VxRail RASR-Reset 2
One-shot UEFI Boot Menu auswählen
![Rasr-Schritt2](/assets/vxrail/vxrail-rasr2.JPG)

#### VxRail RASR-Reset 3
Internal SD: auswählen
![Rasr-Schritt3](/assets/vxrail/vxrail-rasr3.JPG)

#### VxRail RASR-Reset 4
Factory Reset mit F auswählen
![Rasr-Schritt4](/assets/vxrail/vxrail-rasr4.JPG)

#### VxRail RASR-Reset 5
Mit "Yes" bestätigen
Anschließend muss mit "Disconnect" bestätigt werden, dass alle externen Storage Devices (FC, iSCSI etc.) entfernt wurden.
![Rasr-Schritt5](/assets/vxrail/vxrail-rasr5.JPG)

#### VxRail RASR-Reset 6
Der RASR Vorgang dauert ca. 1-1,5Std.
Nach erfolgreichen Abschluss "Successfully completed!" muss mit der Enter-Taste das "Continue" bestätigt werden und der Node führt einen Neustart durch.

#### Optional: Wird der RASR-Reset mit Fehler abgeschlossen
Der komplette RASR-Prozess wird im fist.log auf dem lokalen Datastore gespeichert.

```console
cd /vmfs/volumes
find . -name fist.log 
```

