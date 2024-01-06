---
layout: post
title: "VMware vSphere Standard Switch - Migrationsscript"
categories: [VMware, PowerCLI]
tags: [VMware, ESXi, PowerCLI]
---

![vDS-Switch](/assets/2023-02-18-VMware_vSS_Migrationsscript/vSphere-Standard-Switch.png)

Wer kennt es nicht, gefühlt 100 Port-Groups auf einem vSphere "Standard Switch".
Und dann kommt der Zeitpunkt, an dem ein neuer ESXi-Host im Cluster dazu kommt und man genau diese 100 Port-Groups fein säuberlich am besten noch ohne Fehler von Hand anlegen darf.
Oder man betreibt eine kleine vSphere Umgebungen mit nur einem ESXi-Host und muss diese auf einen neuen ESXi-Host migrieren. 

Dafür habe ich folgendes Script zusammengestellt.  
[Migrationstool_vSphere-StandardSwitch](https://github.com/vi-universe/VMware-Public/blob/df9136c734c7d90199a82c892bfeae6adc99d9c3/PowerCLI/Migrationstool_vSphere-StandardSwitch.ps1)