---
title: Microsoft Defender Endpoint | Unmanaged Devices - Detection | Not Onboarded Devies
date: 2021-06-03 14:00:00 +07:00
tags: [blueteam, detection, defender, endpoint]
description: Rogue Devices detecting by Microsoft Defender Endpoint
---

Most of the companies having unmanaged/rogue devices inside their network, and not available in their asset inventory management. It will be big risk for enterprises/organisations, so they having to improve their rogue device detection and visbility over the network and asset management. 

### Incident Response Team - Plan

1. Collect asset management data from multiple teams. 
2. Compare the old and updated asset data and identify the new devices. 
3. Look at JIRA/Ticketing tools about those newly detected devices in the network. 
4. Track and contain unknown devices inside the network. 
5. Actively hunt using existing SIEM/EDR technology. 
6. Enable rogue device detections inside your vulnerability management tools.
7. Investigate rogue/unmanaged device traffic and hunt unknown behaviours across the network. 


#### Endpoint Discovery: (Microsoft Defender Endpoint)

```shell
// Devices that are not onboarded
DeviceInfo
| where OnboardingStatus != "Onboarded"
| where isempty( ['MergedToDeviceId'])
| where isnotempty( DeviceName)
| where isnotempty( OSPlatform)
| summarize arg_max(Timestamp,*) by DeviceId
```


#### Nmap Discovery: (DHCP)

```bash
$ nmap -sV --allports -T4 10.1.0.0/24
Nmap scan report for 10.1.0.1
Host is up (0.0038s latency).
Not shown: 995 filtered ports
PORT     STATE SERVICE        VERSION
53/tcp   open  domain         Unbound
80/tcp   open  http           nginx
2022/tcp open  ssh            OpenSSH 7.5 (protocol 2.0)
5000/tcp open  ssl/http-proxy HAProxy http proxy 1.3.1 or later
8443/tcp open  ssl/http       nginx
Service Info: Device: load balancer

Nmap scan report for 10.1.0.2
Host is up (0.82s latency).
Not shown: 992 closed ports
PORT     STATE SERVICE  VERSION
22/tcp   open  ssh      OpenSSH 8.3p1 Debian 1 (protocol 2.0)
80/tcp   open  http     nginx
111/tcp  open  rpcbind  2-4 (RPC #100000)
443/tcp  open  ssl/http nginx
2049/tcp open  nfs      3-4 (RPC #100003)
3260/tcp open  iscsi?
6000/tcp open  http     aiohttp 3.6.2 (Python 3.8)
8080/tcp open  http     Apache httpd 2.4.46 ((Debian) mpm-itk/2.4.7-04 OpenSSL/1.1.1g)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```

#### Nmap Discovery: (UPnP)

```bash
$ sudo nmap --script broadcast-dhcp-discover -e bond0
Starting Nmap 7.70 ( https://nmap.org ) at 2020-10-28 19:24 CDT
Pre-scan script results:
| dhcp:
|   Response 1 of 2:
|     Interface: bond0
|     IP Offered: 10.1.0.78
|     DHCP Message Type: DHCPOFFER
|     Server Identifier: 10.1.0.1
|     IP Address Lease Time: 5m00s
|     Subnet Mask: 255.255.255.0
|     Router: 10.1.0.1
|     Domain Name Server: 10.1.0.1
|     Domain Name: lab.opencloud.io
|   Response 2 of 2:
|     Interface: bond0
|     IP Offered: 10.1.0.27
|     DHCP Message Type: DHCPOFFER
|     Server Identifier: 10.1.0.3
|     IP Address Lease Time: 2m00s
|     Renewal Time Value: 1m00s
|     Rebinding Time Value: 1m45s
|     Subnet Mask: 255.255.255.0
|     Broadcast Address: 10.1.0.255
|     Router: 10.1.0.3
|_    Domain Name Server: 10.1.0.3
WARNING: No targets were specified, so 0 hosts scanned.
Nmap done: 0 IP addresses (0 hosts up) scanned in 10.31 seconds
```
