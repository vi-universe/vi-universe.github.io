---
layout: post
title: "DELL-VxRail Report to MS-Teams"
categories: [VxRail]
tags: [VMware, DELL, VxRail, Troubleshooting]
---

Da ich mir ohnehin seit längerem vorgenommen habe, mir die VxRail PowerShell Module anzusehen, bin ich auf die Idee gekommen, mir einen Report über alle Support-Relevanten Daten zu erstellen und mir den Report in Teams "posten" zu lassen. 

![TeamsNotify](/assets/2024-03-05-VxRail-Report-to-teams/TeamsNotify.png)


[Link zu dem Script -> VxRail Report to Teams ](https://github.com/vi-universe/VxRail/blob/6769f389b127367d386f61b0c56edab5e2da1aca/reporting/vxrail_marvin-report-teams.ps1)

[Link zu den PowerShell Modulen -> VxRail PowerShell-Module ](https://github.com/vi-universe/VxRail/tree/6769f389b127367d386f61b0c56edab5e2da1aca/VxRail-PowerShell-Module)

Kleine Anleitung zum einrichten der "Webhooks" in Teams

![weebhook](/assets/2024-03-05-VxRail-Report-to-teams/webhook.png)

![weebhook2](/assets/2024-03-05-VxRail-Report-to-teams/webhook2.png)

Unbedingt die URL kopieren, diese benötigt man im Script. (Zeile22 URI = 'uri')

![weebhook3](/assets/2024-03-05-VxRail-Report-to-teams/webhook3.png)