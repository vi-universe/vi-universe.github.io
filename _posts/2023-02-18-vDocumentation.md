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

![vdocumentation](/assets/vdocumentation.png)


Als Basis nutze ich die Module von vDocumentation und habe diese um den Export der Firewall erweitert. Zudem konvertiere ich mir die CSV-Dateien in eine HTML zur besseren Ansicht um.

[Hier geht es zu meiner angepassten Version](https://github.com/vi-universe/VMware-Public/blob/ed55b018d3e6d52e74f34188336da882b25a7e0e/PowerCLI/VMware%20Sphere%20vDoc.ps1)
