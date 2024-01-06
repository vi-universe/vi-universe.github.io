---
layout: post
title: "vSAN Node aktualisiert unicastagent list nicht automatisch nach Shutdown"
categories: [VMware, vSAN]
tags: [VMware, ESXi-7.*, vSAN]
---

Hin und wieder muss man für Wartungsarbeiten etc. seine vSAN Umgebung herunterfahren. 
Normalerweise ist dieser Vorgang nicht unbedingt kritisch, dennoch bin ich in letzter Zeit öfters darüber gestolpert, dass ein vSAN Node seine Partner nicht mehr gefunden hat.
### vSAN Umgebung
Die vSAN Umgebung umfasst 8 vSAN Nodes als Stretched Cluster + Witness. Also 4+4+N.
### Die Ausgangslage
Nach einem "Cluster Shutdown" fanden nur noch 7 von 8 Nodes ihre vSAN-Partner.  
Auf meinem Screenshot erkennt man die "Command-Ausgabe" von Node04.  
In der Zeile "Sub-Cluster Member HostName" ist deutlich zu erkennen das seine vSAN Partner fehlen.



![vSAN Unicast Agent List](/assets/2023-01-29-vSAN_Node_unicastagent_list/vSANUnicastagentlist.jpg)



```shell
esxcli vsan cluster get
```

Der Blick in die "Unicastagent list" bestätigt dies. Normalerweiße sollten hier alle Nodes aufgeführt sein, außer der jeweilige Node selbst.

```shell
esxcli vsan cluster unicastagent list
```

Also gut... Was gilt es zu überprüfen.

Mit diesem Command lasse ich mir meine Netzwerk-Interface anzeigen um zu überprüfen ob der Link Status "Up" ist.

```shell
esxcli network nic list
```

Anschließend lasse ich mir anzeigen auf welchem VMKernel Port vSAN Traffic aktiviert ist.

```shell
esxcli vsan network list
```

VMK3 Traffic Type: vSAN<br>

Mit dieser Information, kann ich mit folgenden Befehl überprüfen, ob mein Node04 über das vSAN Netzwerk alle anderen Nodes erreicht.
So far so good - Ich konnte über VMKernelport vmk3 alle anderen Nodes inkl. Witness erreichen.

```shell
vmkping -I vmk3 *IP VMK3 der anderen Nodes*
```
Beide Interfaces "Up" - vmkping auch erfolgreich.

Dann helfen wir Node04 manuell auf die Beine.

### Zu diesem Zeitpunkt waren keine VMs gestartet und alle Nodes im Wartungsmodus

```shell
esxcli system maintenanceMode set -e true -m noAction
```

Dieser Command deaktiviert temporär die automatischen Updates der Unicastagent List.

Diesen Command führe ich auf allen Nodes im Cluster aus.

```shell
esxcfg-advcfg -s 1 /VSAN/IgnoreClusterMemberListupdates
```

Nachdem ich auf allen Nodes, dass automatische Update deaktiviert habe, notiere ich mir die UUID aller Nodes in Notepad.
Folgender Befehl gibt mir die Host_UUID aus.
```shell
cmmds-tool whoami
```

Nun füge ich auf meinem betroffen Node04 alle anderen vSAN Partner manuell hinzu.

#### Node04 selbst darf nicht eingetragen werden

```shell
esxcli vsan cluster unicastagent add -t node -u <Host_UUID> -U true -a <Host_VSAN_IP> -p 12321
```

Um den vSAN-Witness hinzuzufügen, muss der Command etwas geändert werden.

```shell
esxcli vsan cluster unicastagent add -t witness -u <Host_UUID> -U true -a <Host_VSAN_IP> -p 12321
```

Mal sehen ob wieder alle vSAN Partner am Start sind ;)

```shell
esxcli vsan cluster get
```

Danach muss wieder das automatische Update der Unicastagent List aktiviert werden.

```shell
esxcfg-advcfg -s 0 /VSAN/IgnoreClusterMemberListupdates
```

```shell 
esxcli vsan cluster get
```

```shell
esxcli vsan cluster unicastagent list
```

```shell 
esxcli network nic list-> esxcli vsan network list
```

```shell
vmkping -I vmk3 *IP VMK3 der anderen Nodes*
```
