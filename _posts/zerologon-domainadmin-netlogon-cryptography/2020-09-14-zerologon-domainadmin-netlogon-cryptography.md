---
title: Zerologon - CVE-2020-1472 (POC)
date: 2020-09-14 11:00:00 +07:00
tags: [exploit, poc, python, github]
description: CVE-2020-1472
---

This vulnerability allowed threat actor to foothold on your enterprise (internal) network to become a domain admin with single click.

The vulnerability stems from a flaw in a cryptographic authentication scheme used by the Netlogon Remote Protocol, which among other things can be used to update computer passwords. This flaw allows attackers to impersonate any computer, including the domain controller itself, and execute remote procedure calls on their behalf.

#### Github Tool:

[ZeroLogon- POC Script -Attacker](https://github.com/SecuraBV/CVE-2020-1472)

#### Tools used:
1. [Python](https://www.python.org/downloads/)
2. [Impacket](https://github.com/SecureAuthCorp/impacket)

#### Reference Article:
[ZeroLogon Article](https://www.secura.com/blog/zero-logon)
