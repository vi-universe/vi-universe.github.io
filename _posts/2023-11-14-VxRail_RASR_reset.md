---
layout: post
title: "DELL-VxRail RASR Reset"
categories: [VxRail]
tags: [VMware, DELL, VxRail,]
---

#### VxRail RASR
Um einen VxRail-Node in den Auslieferungszustand zu versetzen, ist es notwendig, einen RASR-Reset durchzuführen. 
Ein RASR-Reset löscht alle Daten und Einstellungen. Notwendig ist dies, wenn zum Beispiel die initiale Installation fehlschlägt.
Ab der Generation 15 (E/P/V/D/S/G) 6XX , sind keine SD-Karten mit dem RASR-Image in der VxRail verbaut. Um das RASR-Image zu erhalten, benötigt man die "solve-prozedur" welche unter solve.dell.com erstellt werden kann.
Anschließend muss der VxRail-Node mit dem RASR-Image gestartet werden. 

#### VxRail RASR-Reset 1 (vor Gen 15)
Boot in den Boot Manager -> F11 
![Rasr-Schritt1](/assets/2023-11-14-VxRail_RASR_reset/vxrail-rasr1.JPG)

#### VxRail RASR-Reset 1 (Gen 15)
Die Weboberfläche des iDRACs über die IP-Adresse im Browser aufrufen, und sich mit Benutzername und Kennwort anmelden. Anschließend kann die "Virtuelle Konsole" gestartet werden. Im separaten Fenster der "virtuellen Konsole" kann entsprechend das RASR-ISO als "virtual CD/DVD" verbunden werden.
Über den Button "Boot" kann dann von der "virtual CD/DVD/ISO" der VxRail-Node gestartet werden.
![Rasr-Schritt1 (Gen 15)](/assets/2023-11-14-VxRail_RASR_reset/vxrail-rasr1.1.jpg)

#### VxRail RASR-Reset 2 (vor Gen 15)
One-shot UEFI Boot Menu auswählen
![Rasr-Schritt2](/assets/2023-11-14-VxRail_RASR_reset/vxrail-rasr2.JPG)

#### VxRail RASR-Reset 3 (vor Gen 15)
Internal SD: auswählen
![Rasr-Schritt3](/assets/2023-11-14-VxRail_RASR_reset/vxrail-rasr3.JPG)

#### VxRail RASR-Reset 4 
Factory Reset mit F auswählen
![Rasr-Schritt4](/assets/2023-11-14-VxRail_RASR_reset/vxrail-rasr4.JPG)

#### VxRail RASR-Reset 5
Mit "Yes" bestätigen
Anschließend muss mit "Disconnect" bestätigt werden, dass alle externen Storage Devices (FC, iSCSI etc.) entfernt wurden.
![Rasr-Schritt5](/assets/2023-11-14-VxRail_RASR_reset/vxrail-rasr5.JPG)

#### VxRail RASR-Reset 6
Der RASR Vorgang dauert ca. 1-1,5Std.
Nach erfolgreichen Abschluss "Successfully completed!" muss mit der Enter-Taste das "Continue" bestätigt werden und der Node führt einen Neustart durch.

#### Optional: Wird der RASR-Reset mit Fehler abgeschlossen
Der komplette RASR-Prozess wird im fist.log auf dem lokalen Datastore gespeichert.

```console
cd /vmfs/volumes
find . -name fist.log 
```

