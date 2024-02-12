---
layout: post
title: "vDocumentation"
categories: [VMware, PowerCLI]
tags: [VMware, ESXi, PowerCLI]
---

Ein tolles Tool zur Erfassung der VMware vSphere Umgebung ist vDocumentation von
Ariel Sanchez Mora.
[vDocumentation](https://github.com/arielsanchezmora/vDocumentation)

Mit folgenden Befehlen lassen sich wichtige Informationen auslesen und in eine Excel oder CSV Datei exportieren.  

![vdocumentation](/assets/2023-02-18-vDocumentation/vdocumentation.png)


Als Basis nutze ich die Module von vDocumentation und habe diese um den Export der Firewall erweitert. Zudem konvertiere ich mir die CSV-Dateien in eine HTML zur besseren Ansicht um.

[Hier geht es zu meiner angepassten Version](https://github.com/vi-universe/vmware/blob/1b8cb303fd68010e9ef9a23e4ffb655d45aa2cb7/PowerCLI/VMware%20Sphere%20vDoc.ps1)
