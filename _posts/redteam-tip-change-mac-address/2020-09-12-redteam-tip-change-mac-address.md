---
title: RedTeam Tip - Change MAC address in endpoint
date: 2020-09-12 10:00:00 +07:00
tags: [redteam, endpoint, pentest]
description: Change MAC Address in endpoint machines.
---

In Most of the RedTeam/Pentest engagements, smart guys always change MAC address in compromise endpoints to bypass Security detection tools.

##### Change MAC Address - Powershell (Windows OS):
```powershell
Set-NetAdapter -Name "<Network Interface>" -MacAddress "<Random MAC Address>"
#Set-NetAdapter -Name "Ethernet 1" -MacAddress "00-10-18-57-1B-0D"
```
##### Change MAC Address - Command line (Linux/Mac OS):
```bash
$sudo ifconfig <interface> ether <Random MAC Address>
$sudo ifconfig en0 ether 00:18:57:1B-0D
```
