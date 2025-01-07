---
layout: post
title: "NSX Cheat-Sheet"
categories: [NSX]
tags: [NSX]
---

## Log & Log-Verzeichnis

Auf NSX-Appliances befinden sich Syslog-Nachrichten in `/var/log/syslog`.

Auf NSX-Appliances können Sie den folgenden NSX-CLI-Befehl verwenden, um die Logs anzuzeigen:

```
get log-file <auth.log | controller | controller-error | http.log | kern.log | manager.log | node-mgmt.log | syslog> [follow]
```

| Name                  | Beschreibung                   |
|-----------------------|--------------------------------|
| auth.log              | Authentifizierungslog         |
| controller            | Controller-Log                |
| controller-error      | Controller-Fehler-Log         |
| http.log              | HTTP-Dienst-Log               |
| kern.log              | Kernel-Log                    |
| manager.log           | Manager-Dienst-Log            |
| node-mgmt.log         | Node-Management-Log           |
| nsx-audit-write.log   | NSX-Audit-Schreib-Log         |
| nsx-audit.log         | NSX-Audit-Log                 |
| syslog                | System-Log                    |

## Syslog Konfiguration

## ESXi
```

esxcli network firewall ruleset set -r syslog -e true

esxcli system syslog config set --loghost=udp://<log server ip>:<Port>


esxcli system syslog reload


esxcli system syslog mark -s "This is a test message"
```

## NSX-Manager Syslog-Konfiguration

```
set logging-server <log server ip or FQDN>:514 proto udp level info
```
```
# Anzeigen der Cluster-Konfiguration
get cluster config

# Anzeigen des API-Zertifikat-Thumbprints
get certificate api thumbprint

# Hinzufügen eines Knotens zum Cluster
join <ip> cluster-id <ID> thumbprint <thumbprint> username <username> password <password>
```

## NSX-Edge
```
get managers


get node-uuid


get vteps


get interfaces


get host-switches


get logical-routers


get route bgp


get bgp neighbor summary


get ospf route


get ospf neighbor
```

## NSX-Edge join management-plane

```
### nsx-manager
get certificate api thumbprint

### nsx-edge 
join management-plane <ip> thumbprint <thumbprint> username <username> password <password>
```

## ESXi Distributed Firewall
```
summarize-dvfilter | grep -A 3 vmm


vsipioctl getrules -f <name nic> -> Option -s Firewall Statistik


vsipioctl getaddrset -f <name nic>


vsipioctl getflows -f <name nic>


vsipioctl getfwconfig -f <name nic>

### Hilfe Menü
vsipioctl -h
```

## pktcap-uw

### ESXTOP
```
ESXTOP -> PORT-ID
```

### Net-stats
```
Net-stats -l -> PortNum
```

### ESXCLI
```
esxcli network nic list -> Name
```

summarize-dvfilter -> Name

–dir 0 – capture incoming traffic
–dir 1 – capture outgoing traffic
–dir 2 – capture both traffic

–stage 0 – before traffic dvfilter
–stage 1 – after traffic dvfilter

### Beispiel für die Verwendung von pktcap-uw
```
pktcap-uw --switchport <port nummer> --dir 0 -o capture.pcap
pktcap-uw –vmk vmk10 –dir 2 -o – | tcpdump-uw -enr –
pktcap-uw --switchport <port nummer> --trace
```