---
layout: post
title:  "vSAN Node aktualisiert Unicastagent list nicht automatisch nach Shutdown"
categories: [VMware, vSAN]
tags: [VMware, ESXi-7.*, vSAN]
---

<p>Hin und wieder muss man für Wartungsarbeiten etc. seine vSAN Umgebung herunterfahren. Normalerweise ist dieser Vorgang nicht unbedingt kritisch, dennoch bin ich in letzter Zeit öfters darüber gestolpert, dass ein vSAN Node seine Partner nicht mehr gefunden hat.<br>
Meine Umgebung umfasst 8 vSAN Nodes als Stretched Cluster + Witness. <br>
Nach einem "Cluster Shutdown" fanden nur noch 7 von 8 Nodes ihre vSAN-Partner. <br>                         
Auf meinem Screenshot erkennt man die "Command-Ausgabe" von Node04. <br>                                        
In der Zeile "Sub-Cluster Member HostName" ist deutlich zu erkennen das seine vSAN Partner fehlen.<p>

```
esxcli vsan cluster get
```
<br>
<p>Der Blick in die "Unicastagent list" bestätigt dies. Normalerweiße sollten hier alle Nodes aufgeführt sein, außer der jeweilige Node selbst.<br>
<br>
```
esxcli vsan cluster unicastagent list
```
<br>
Also gut... Was gilt es zu überprüfen.
<br>
Mit diesem Command lasse ich mir meine Netzwerk-Interface anzeigen um zu überprüfen ob der Link Status "Up" ist.<br>
<br>
```
esxcli network nic list
```
<br>
Anschließend lasse ich mir anzeigen auf welchem VMKernel Port vSAN Traffic aktiviert ist.<br>
<br>
```
esxcli vsan network list
```
<br>
VMK3 Traffic Type: vSAN<br>
<br>
Mit dieser Information, kann ich mit folgenden Befehl<br>
<br>
```
vmkping -I vmk3 *IP VMK3 der anderen Nodes*
```
<br>
überprüfen, ob mein Node04 über das vSAN Netzwerk alle anderen Nodes erreicht.<br>
So far so good - Ich konnte über VMKernelport vmk3 alle anderen Nodes inkl. Witness erreichen.<br>
<br>
Beide Interfaces "Up" - vmkping auch erfolgreich. <br>
<br> 
Dann helfen wir Node04 manuell auf die Beine.<br>
<br>
Configuring vSAN Unicast networking from the command line (2150303)<br>
<br>
Zu diesem Zeitpunkt waren keine VMs gestartet und alle Nodes im Wartungsmodus<br>
<br>
```
esxcli system maintenanceMode set -e true -m noAction
```
Dieser Command deaktiviert temporär die automatischen Updates der Unicastagent List.<br>

Diesen Command führe ich auf allen Nodes im Cluster aus.<br>
```
esxcfg-advcfg -s 1 /VSAN/IgnoreClusterMemberListupdates
```
Nachdem ich auf allen Nodes, dass automatische Update deaktiviert habe, notiere ich mir die UUID aller Nodes in Notepad.<br>
```
cmmds-tool whoami
```
Nun füge ich auf meinem betroffen Node04 alle anderen vSAN Partner manuell hinzu.<br>

Node04 selbst darf nicht eingetragen werden<br>
```
esxcli vsan cluster unicastagent add -t node -u <Host_UUID> -U true -a <Host_VSAN_IP> -p 12321
```
Um den vSAN-Witness hinzuzufügen, muss der Command etwas geändert werden.<br>
```
esxcli vsan cluster unicastagent add -t witness -u <Host_UUID> -U true -a <Host_VSAN_IP> -p 12321
```
Mal sehen ob wieder alle vSAN Partner am Start sind ;)<br>
```
esxcli vsan cluster get
```
Danach wieder das automatische Update aktivieren.
```
esxcfg-advcfg -s 0 /VSAN/IgnoreClusterMemberListupdates
```
<br>
```
esxcli vsan cluster get
```
```
esxcli vsan cluster unicastagent list
```
```
esxcli network nic list-> esxcli vsan network list
```
```
vmkping -I vmk3 *IP VMK3 der anderen Nodes* 
```