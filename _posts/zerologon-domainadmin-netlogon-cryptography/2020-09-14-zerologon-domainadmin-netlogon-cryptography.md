---
title: Zerologon (CVE-2020-1472) <-> Red|Blue Teams
date: 2020-09-14 11:00:00 +07:00
tags: [exploit, poc, python, github]
modified: 2020-09-17 21:49:47 +07:00

description: CVE-2020-1472
---

This vulnerability allowed threat actor to foothold on your enterprise network to become a domain admin with single click.

The vulnerability stems from a flaw in a cryptographic authentication scheme used by the Netlogon Remote Protocol, which among other things can be used to update computer passwords. This flaw allows attackers to impersonate any computer, including the domain controller itself, and execute remote procedure calls on their behalf.

#### RedTeam - Offensive Tools/Scripts:

<figure>
<img src="https://raw.githubusercontent.com/zer0trustsec/zer0trustsec.github.io/master/_posts/zerologon-domainadmin-netlogon-cryptography/Exploit.png" alt="">
<figcaption> Python Exploit - ZeroLogon (CVE-2020-1472) </figcaption>
</figure>

- [ZeroLogon- POC Script-1](https://github.com/SecuraBV/CVE-2020-1472)
- [ZeroLogon- POC Script-2](https://github.com/blackarrowsec/redteam-research/tree/master/CVE-2020-1472)
- [ZeroLogon - Mimikatz](https://github.com/gentilkiwi/mimikatz/releases/tag/2.2.0-20200917)
- [Zerologon - Powershell](https://github.com/BC-SECURITY/Invoke-ZeroLogon)

#### BlueTeam - Defense:

Windows Event Correlation:
- Keep an eye our Event ID 4624 followed by a 4742.
- Failed attempts look for Event ID 5805

<figure>
<img src="https://raw.githubusercontent.com/zer0trustsec/zer0trustsec.github.io/master/_posts/zerologon-domainadmin-netlogon-cryptography/zerologon_blueteam.png" alt="">
<figcaption> Windows Events - ZeroLogon (CVE-2020-1472) </figcaption>
</figure>

#### Snort Rule
```bash
alert tcp any any -> [!<domaincontrollers to exclude here] [49152:65535] (msg:"Possible DCSync Detected"; flow:to_server,established; flags:PA; content:"|00 03 10 00 00 00|"; depth:8; content:"|03 00|"; distance:14; classtype:attempted-admin; sid:20166316;)
```

#### Other Detections:

- [EVTX- Simulation Logs by @sbousseaden ](https://github.com/sbousseaden/EVTX-ATTACK-SAMPLES/blob/master/Credential%20Access/remote_pwd_reset_rpc_mimikatz_postzerologon_target_DC.evtx)
- [Detection - Zeek](https://corelight.blog/2020/09/16/detecting-zerologon-cve-2020-1472-with-zeek/)


#### Reference Articles/Posts:
[ZeroLogon Article](https://www.secura.com/blog/zero-logon)
[Twitter - @SBousseaden](https://twitter.com/SBousseaden/status/1306631518618607623)
[Twitter - @joshlemon](https://twitter.com/joshlemon/status/1306487256480460805)
