---
layout: post
title: "ESXi root entsperren"
categories: [ESXi]
tags: [VMware, ESXi]
---

Sperrt man sich den ESXi-Root Benutzer, ist es wichtig, zu wissen, dass der Zugriff nur noch über die DCUI und die ESXi-Shell möglich ist.
Sämtliche andere Möglichkeiten sind von der Sperre betroffen, wie z.B Web-GUI, SSH etc.
Folgende Anleitung entsperrt den "root" Benutzer oder jeden anderen beliebigen Benutzer.

 

### 1. Login an der DCUI  mit root und Passwort

### 2. ESXi Shell aktivieren > Troubleshooting Options

### 3. In die ESXi-Shell wechseln > STRG+ALT+F1

### 4. Befehl > pam_tally2 --user root -r  