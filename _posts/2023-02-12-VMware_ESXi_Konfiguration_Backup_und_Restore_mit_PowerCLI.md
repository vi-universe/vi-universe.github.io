---
layout: post
title: "VMware ESXi Konfiguration „Backup und Restore“ mit PowerCLI"
categories: [ESXi]
tags: [VMware, ESXi-7.*, PowerCLI]
---

Besonders vor kritischen Arbeiten oder Update/Upgrades ist es sinnvoll, die Konfiguration eines ESX-Hosts
zu sichern. 

#### ESXi Konfiguration Backup

```powershell
write-host "Specify local backup destination path" -ForegroundColor Green 
$Path= Read-Host "Enter backup destination path on your local device" 


write-host "Specify ESXi IP" -ForegroundColor Green 
$ESXiHost= Read-Host "Enter your ESXi IP" 


write-host "Connecting to Host" -ForegroundColor Green
Connect-VIServer $ESXiHost

Get-VMHost | Get-VMHostFirmware -BackupConfiguration -DestinationPath $Path
```
#### ESXi Konfiguration Restore

```powershell
write-host "Specify local backup destination path and the config file" -ForegroundColor Green 
$Path= Read-Host "Enter backup destination path on your local device" 


write-host "Specify ESXi IP" -ForegroundColor Green 
$ESXiHost= Read-Host "Enter your ESXi IP" 


write-host "Connecting to Host" -ForegroundColor Green
Connect-VIServer $ESXiHost

Get-VMHost | Set-VMHost -State Maintenance

Get-VMHost | Set-VMHostFirmware -Restore -Force -SourcePath $Path
```
