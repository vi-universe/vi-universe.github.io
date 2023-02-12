---
layout: post
title: " PowerCLI 13 Update / Installation QuickGuide"
categories: [VMware, ESXi]
tags: [VMware, ESXi, PowerCLi]
---

### Quick Guide mit allen Links und Informationen für die PowerCLI Version 13

```powershell
 # Deinstallation 

Get-Module VMware.PowerCLI -ListAvailable | Uninstall-Module -Force
 
# Installation 

Install-Module vmware.powercli -SkipPublisherCheck
```
### Python 3.7 
[Python 3.7 Donwload](https://www.python.org/downloads/release/python-370/)

### Pip3
[Pip3 Download](https://bootstrap.pypa.io/get-pip.py)


```terminal
<python3.7-directory>\python.exe <get-pip-directory>\get-pip.py 
<python3.7-directory>\Scripts\pip3.7.exe install six psutil lxml pyopenssl
```

```powershell
# Python Pfad Powershell
Set-PowerCLIConfiguration -PythonPath <python3.7-directory>\python.exe -Scope User
```

### Issues
 The old certificate that we used had expired and we had to replace it with a new one, which however was from different publisher. And it seems like PowerShell has some issues with that. Just remove the old version and install from scratch.

 ### Links
[PowerCli-13-is-now-ga](https://blogs.vmware.com/PowerCLI/2022/11/powercli-13-is-now-ga.html)
[Developer VMware install powercli](https://developer.vmware.com/docs/15315/powercli-user-s-guide/GUID-2DD2454B-2B1E-4A7D-9134-B442254F0681.html)
[Developer VMware install configure python](https://developer.vmware.com/docs/15315/powercli-user-s-guide/GUID-9081EBAF-BF85-48B1-82A0-D1C49F3FF1E8.html)