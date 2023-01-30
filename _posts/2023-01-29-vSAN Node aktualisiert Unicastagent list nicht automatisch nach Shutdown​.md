---
layout: post
title: "vSAN Node aktualisiert Unicastagent list nicht automatisch nach Shutdown"
categories: [VMware, vSAN]
tags: [VMware, ESXi-7.*, vSAN]
---

Hin und wieder muss man für Wartungsarbeiten etc. seine vSAN Umgebung herunterfahren. Normalerweise ist dieser Vorgang nicht unbedingt kritisch, dennoch bin ich in letzter Zeit öfters darüber gestolpert, dass ein vSAN Node seine Partner nicht mehr gefunden hat.
Meine Umgebung umfasst 8 vSAN Nodes als Stretched Cluster + Witness.
Nach einem "Cluster Shutdown" fanden nur noch 7 von 8 Nodes ihre vSAN-Partner.  
Auf meinem Screenshot erkennt man die "Command-Ausgabe" von Node04.  
In der Zeile "Sub-Cluster Member HostName" ist deutlich zu erkennen das seine vSAN Partner fehlen.

```PowerShell
esxcli vsan cluster get
```

<p>Der Blick in die "Unicastagent list" bestätigt dies. Normalerweiße sollten hier alle Nodes aufgeführt sein, außer der jeweilige Node selbst.

```PowerShell
esxcli vsan cluster unicastagent list
```

Also gut... Was gilt es zu überprüfen.

Mit diesem Command lasse ich mir meine Netzwerk-Interface anzeigen um zu überprüfen ob der Link Status "Up" ist.

```PowerShell
esxcli network nic list
```

Anschließend lasse ich mir anzeigen auf welchem VMKernel Port vSAN Traffic aktiviert ist.

```PowerShell
esxcli vsan network list
```

VMK3 Traffic Type: vSAN<br>

Mit dieser Information, kann ich mit folgenden Befehl

```PowerShell
vmkping -I vmk3 *IP VMK3 der anderen Nodes*
```

überprüfen, ob mein Node04 über das vSAN Netzwerk alle anderen Nodes erreicht.
So far so good - Ich konnte über VMKernelport vmk3 alle anderen Nodes inkl. Witness erreichen.

Beide Interfaces "Up" - vmkping auch erfolgreich.

Dann helfen wir Node04 manuell auf die Beine.

Configuring vSAN Unicast networking from the command line (2150303)

Zu diesem Zeitpunkt waren keine VMs gestartet und alle Nodes im Wartungsmodus

```PowerShell
esxcli system maintenanceMode set -e true -m noAction
```

Dieser Command deaktiviert temporär die automatischen Updates der Unicastagent List.

Diesen Command führe ich auf allen Nodes im Cluster aus.

```PowerShell
esxcfg-advcfg -s 1 /VSAN/IgnoreClusterMemberListupdates
```

Nachdem ich auf allen Nodes, dass automatische Update deaktiviert habe, notiere ich mir die UUID aller Nodes in Notepad.

```
cmmds-tool whoami
```

Nun füge ich auf meinem betroffen Node04 alle anderen vSAN Partner manuell hinzu.

Node04 selbst darf nicht eingetragen werden

```PowerShell
esxcli vsan cluster unicastagent add -t node -u <Host_UUID> -U true -a <Host_VSAN_IP> -p 12321
```

Um den vSAN-Witness hinzuzufügen, muss der Command etwas geändert werden.

```PowerShell
esxcli vsan cluster unicastagent add -t witness -u <Host_UUID> -U true -a <Host_VSAN_IP> -p 12321
```

Mal sehen ob wieder alle vSAN Partner am Start sind ;)

```PowerShell
esxcli vsan cluster get
```

Danach wieder das automatische Update aktivieren.

```PowerShell
esxcfg-advcfg -s 0 /VSAN/IgnoreClusterMemberListupdates
```

```PowerShell
esxcli vsan cluster get
```

```PowerShell
esxcli vsan cluster unicastagent list
```

```PowerShell
esxcli network nic list-> esxcli vsan network list
```

```PowerShell
vmkping -I vmk3 *IP VMK3 der anderen Nodes*
```
