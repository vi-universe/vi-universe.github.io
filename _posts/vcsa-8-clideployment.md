---
layout: post
title: "VCSA-8 CLI deployment"
categories: [VMware, vSphere8]
tags: [VMware, vCenter]
---
Gerade wenn es darum geht, unkompliziert und schnell eine vCenter Appliance bereitzustellen, ist es wirklich smart, diese Möglichkeit zu nutzen.
Nachdem das VMware VCSA ISO File gemountet wurde, findet man unter folgenden Pfad bereits einige Templates.

![vCSA-8-Deployment](/assets/vcsa8-clideployment.png)

##### --> VMware VCSA/vcsa-cli-installer/templates

Unter folgenden link findet man eine Übersicht aller Parameter für das JSON-File.

[Docs-VMware](https://docs.vmware.com/en/VMware-vSphere/8.0/vsphere-vcenter-installation)

Für das Deployment führt man folgenden Befehl in der Konsole (CMD oder Terminal) aus.

```powershell
'/VMware VCSA/vcsa-cli-installer/lin64/vcsa-deploy' install 'Pfad zu,JSON.json' --accept-eula
```
Als Beispiel mein "Quick and Dirty" json file für ein schnelles VCSA Deployment ohne DNS Server. 

```json-file
{
   "__version": "2.13.0",
    "__comments": "Sample template to deploy a vCenter Server Appliance to an ESXi host without a DNS and NTP server",
    "new_vcsa": {
        "esxi": {
            "hostname": "172.30.1.128", --> ESXi IP-Adresse
            "username": "root",
            "password": "VMware123!",
            "deployment_network": "VM Network",
            "datastore": "datastore1"
        },
        "appliance": {
            "thin_disk_mode": true,
            "deployment_option": "tiny",
            "name": "vcsa01"
        },
        "network": {
            "ip_family": "ipv4",
            "mode": "static",
            "system_name": "172.30.1.10", --> IP Adresse der VCSA
            "ip": "172.30.1.10",
            "prefix": "24",
            "gateway": "172.30.1.254",
            "dns_servers": [
                "127.0.0.1"
            ]
        },
        "os": {
            "password": "VMware123!",
            "time_tools_sync": true,
            "ssh_enable": true
        },
        "sso": {
            "password": "VMware123!",
            "domain_name": "vsphere.local"
        }
    },
    "ceip": {
        "settings": {
            "ceip_enabled": false
        }
    }
}
```