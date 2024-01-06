---
layout: post
title: "vSAN Space reclamation - Trim Unmap"
categories: [VMware, vSAN]
tags: [VMware, ESXi-7.*, vSAN, Efficency]
---

Thin Provisioning ist eine Möglichkeit, Speicher effektiv zu nutzen.
"Thin Provisioned" Festplatten wachsen dynamisch an. Geben aber Speicherplatz nicht frei, selbst wenn die Daten im Gast-Betriebsystem gelöscht wurden.
Mithilfe von Trim/Unmap Befehlen kann für das jeweilige ATA und SCSI Protokoll der Speicherplatz wieder zurückgewonnen werden.
VMware vSAN erkennt vollständig vom Gastbetriebssysteme diese Befehle und kann den zugewiesenen Speicher als freien Speicherplatz zurückfordern.

Als primärer Vorteil steht die daraus resultierende Effizienz im Fokus, allerdings ergeben sich daraus auch sekundäre Vorteile.

- Schnellere Reparatur, da zurückgewonnene Blöcke im Falle eines Gerätesausfalls nicht neu ausgeglichen oder neu gespiegelt werden müssen.
- Dirty-Cache-Seiten werden entfernt, was zu einer Entlastung des Cache führt.

![vSAN Trim/Unmap](/assets/2023-02-01-vSAN_space_reclamation_trim_unmap​​​​​/vsan-space-reclamation.png)

### Anforderungen

- Min. Hardwareversion 11 virtuelle Maschinen für Windows
- Min. Hardwareversion 13 virtuelle Maschinen für Linux
- Nach Aktivierung auf Clusterebene müssen alle virtuelle Maschinen neu gestartet werden
- Das Flag "disk.scsiUnmapAllowed" darf nicht auf "false" gesetzt sein. Standardwert ist "true".

Mit folgenden Befehlen, kann der Status von Trim/Unmap abgefragt werden und Trim/Unmap aktiviert bzw. auch deaktiviert werden.

```powershell
#Installation des PowerCLI Moduls
Install-Module VMware.PowerCli
#Verbindung zum vCenter
Connect-VIServer "vCenter FQDN"
#Auflistung aller Cluster
Get-Cluster
#Trim/Unmap Status für vSAN Cluster anzeigen
Get-Cluster -Name "Clustername" | Get-vsanclusterconfiguration | ft GuestTrimUnmap
#Trim/Unmap aktivieren
Get-Cluster -Name "Clustername" | Set-vsanclusterconfiguration -GuestTrimUnmap:$true
#Optional Trim/Unmap deaktivieren
Get-Cluster -Name "Clustername" | Set-vsanclusterconfiguration -GuestTrimUnmap:$false
```

