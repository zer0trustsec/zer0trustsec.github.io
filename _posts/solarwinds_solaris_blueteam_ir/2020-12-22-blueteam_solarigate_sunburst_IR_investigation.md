---
title: Solarigate/Sunburst Incident Response Playbook & Investigation/Hunting/MindMap for CSIRT/SOC/InfoSec/SecOps Teams
date: 2020-12-22 4:00:00 +07:00
tags: [blueteam, solarwinds, triage,ir, investigation,forensics]
description: Solarigate/Sunburst IR plan & Investigation Strategy
---

Last few days, Solarigate aka Sunburst zero-day backdoor is being very popular in Infosec world. There was lot of enterprise/govt/nationalagencies/organisations were affected by this backdoor and most of the CSIRT/SOC/SecOps teams were very busy with handling related to solarwinds backdoor incidents.

In this article, I would like to share some IR tips/experiences/plan and threat model on this incident and most of organisations and teams were looking for proper IR plan and investigation steps with proper remediation.

Most of the smart/advanced SecOps teams not wait for SIEM/Threat Intel hits/alerts to handle the these type of incidents. They will start hunting in their environment and create a plan & execute threat hunting hypothesis on these type of emerging threats.

### Threat Hunting Assumptions: Solarigate/Sunburst

Let's assume below of threat hunting hypothesis in your environment.
```text
  1. Identify the specific vulnerable backdoor package identification & timeline. (Ex:Aug 2019 onwards)
  2. Check whether specific vulnerable servers/application logs covered/stored in your SIEM/Logging solutions.
  3. Threat actor is compromised external faced solarwinds Orion servers and gather privileged level access like administrative / user accounts.
  4. Threat actor is able communicate via C2 channel to Vulnerable servers and exfiltration activity was happend.
  5. There was no malicious activity was identified on specific vulnerable servers (not matching with any IOCs/detections but that specific server is vulnerable).
```

### Incident Response Plan and Playbook/Workflow :

#### Notify/Detect:
- If any existing IOCs/hash/detections was triggered in your environment, identify the affected servers and user accounts.
- Update your security products with latest Threat Intel feed on specific threat adversary.

#### Confirmation:
- In this adversary is mainly focusing on supply chain attacks, we don't conclude based on our detections.
Because we don't know how those IOC/IOAs were entered into your environment.
- So, before that communicate with Vulnerability Management/Asset Management teams and get confirmation about the specific affected devices/servers/VMs.

#### Investigation:
- In any IR incident investigation, we have to look at different possible places. So, we should look at multiple log sources and different patterns.

#####  Different Scenarios:

```text
    1. Solarwinds Orion server compromise
    2. Gather privileged local/Domain connected administrator accounts (from Compromised Solarwinds Orion Servers)
    3. Access other resources using compromised AD connected accounts get access to Cloud/On-prime resources
    4. Compromise email accounts and change configs/Inbox rules.
```
##### Steps:
- Take snapshot/image the compromised/vulnerable Solarwinds Orion server.
- Apply yara rules/hashing using multiple forensic/RE tools.
- Finalise the timeline and shortlist the log sources where we were going to investigate in SIEM/3rd party Products.

###### Admin/User Account Level: (Compromised Users/Associated with Solarwinds Orion Servers/VMs)
- List out all of the user accounts used in Solarwinds Orion servers & monitor agent installed VMs/Systems.
- Get the all relevant users login activity details ( Success/Failure events)
```text
      i. Success events by Accountwise ( Sorting Order - Low to High)
      ii. Failed events by Accountwise ( Sorting Order - Low to High)
      iii. Newly created accounts by Serverwise ( Specified timeline)
```
- Once you identify the compromised accounts, look at those user account activities on perimeter level. (Cloud/AD/VPN logs etc.)
- Look at the compromised accounts email box configurations (Login activity/Email communications/Permissions/Inbox Rules etc.)

###### Network Level: (Bro/Firewall/Zeek/Other Products)
- Check whether any C2/IP/domain (Solarigate/Sunburst IOCs) communication/hits in the environment.
- Check whether vulnerable/compromised servers/VMs is communicate with internal systems. ( Specific Timeline)
- Check compromised accounts activities over network. (User Login hits/User session/C2 beaconing etc.)

###### Endpoint Level: (EDR/Sysmon/Winevents etc)
- Check specific backdoor DLL files available in Solarwinds Orion servers/VMs.
- Hunt using IOA/Filenames/Hashes/Filesize/SignedCertificateInfo across multiple endpoint/servers using EDR solutions.
- Digging out if any suspicious processes/activity in Solarwinds Orion server/VMs. (Registry Changes/Suspicious Process/Backdoor DLL/Startup etc.)
- Change all user account passwords and look at the permissions/configurations in Solarwinds Orion server/VMs.
- Look at the EDR/Sysmon suspicious old incidents in Specific timeline. (Linking Incidents/Mapping with MITRE)

#### Containment:
- Isolate the vulnerable/infected SolarWinds Orion servers.
```text
    (i). Look at Digital Forensic team investigation report and add those suspected hashes/files in  block/monitor mode.
    (ii). If you have existing EDR solution please isolate at firewall level (Only server can access EDR console)
    (iii). After forensic imaging and investigation shutdown the servers.  
```
- Look at other service accounts which will access other applications, investigate those application logs take necessary actions. (SQL/SNMP/WMI etc.)
-  Implement IDPS/proxy level defenses in your environment.

#### Eradication:
- Most of the steps were covered in Containment phase.
- Prepare a good plan for securing the user account/ server / network level config management and capture all logs in internal/external perimeter devices/servers.

#### Recovery:
- Backup the server configs/data.
- Design a process for secure configure golden image and Rebuild the all affected servers/VMs.
- Install updated version of Solarwinds Orion.


### SIEM Hunting Queries

#### Splunk

- Search for Event code 4624 (any logins to the Solarwinds server) find out credentials that could be compromised.
``` bash
search index=<windows_events_index> solarwinds* ""EventCode=4624"" Workstation_Name=""solarwinds*""
| stats count min(_time) AS first_time max(_time) AS last_time by Workstation_Name Security_ID Logon_Type
| convert timeformat=""%d/%m/%Y %H:%M:%S"" ctime(*_time)
| sort count
```

- Check Bro for any Solarwinds DNS lookups - find any unknown or test instances of Solarwinds.
``` bash
search index=<bro_logs index>_index sourcetype=bro_dns query=""solarwinds.com""
| rex field=_raw ""(^\d+\.\d+\s\S+\s)(?<src_ip>\d+\.\d+\.\d+\.\d+)""
| search src_ip IN (""solarwinds_ip"",""solarwinds_ip"",""solarwinds_ip"",""solarwinds_ip"")
```

- Check for any historical HTTP/S traffic outbound to published IOCs with any applicable http/s logs
``` bash
search index=<bro_logs index>_index deftsecurity.com OR freescanonline.com OR thedoccloud.com OR thedoccloud.com OR websitetheme.com OR highdatabase.com OR incomeupdate.com OR databasegalore.com OR panhardware.com OR zupertech.com OR appsync-api.eu-west-1.avsvmcloud.com OR appsync-api.eu-west-1.avsvmcloud.com OR appsync-api.us-east-2.avsvmcloud.com OR appsync-api.us-west-2.avsvmcloud.com OR appsync-api.us-west-2.avsvmcloud.com OR appsync-api.eu-west-1.avsvmcloud.com | stats count earliest(_time) AS Earliest, latest(_time) AS Latest by sourcetype source host | eval Earliest=strftime(Earliest,"%+") | eval Latest=strftime(Latest,"%+") | sort - count
```

- Check for any historical IP traffic outbound to the published IOCs with any applicable logs
```bash
search index=<bro_logs_index> 54.193.127.66 OR 54.215.192.52 OR 34.203.203.23 OR 139.99.115.204 OR 5.252.177.25 OR 204.188.205.176 OR 51.89.125.18 OR 167.114.213.199 OR 13.59.205.66 OR 5.252.177.21 | stats count earliest(_time) AS Earliest, latest(_time) AS Latest by index sourcetype source host | eval Earliest=strftime(Earliest,"%+") | eval Latest=strftime(Latest,"%+") | sort - count
```

#### Other References (Azure Sentinel/Azure AD/Yara/ATT&CK/Zeek etc.)

- [Azure Sentinel - Hunting ](https://techcommunity.microsoft.com/t5/azure-sentinel/solarwinds-post-compromise-hunting-with-azure-sentinel/ba-p/1995095)
- [Azure AD Monitor - Hunting](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/azure-ad-workbook-to-help-you-assess-solorigate-risk/ba-p/2010718)
- [Yara Rules - Hunting](https://github.com/fireeye/red_team_tool_countermeasures)
- [Zeek - Hunting](https://corelight.blog/2020/12/22/detecting-sunburst-solarigate-activity-in-retrospect-with-zeek-a-practical-example/)
- [MITRE ATT&CK - Mapping](https://medium.com/mitre-attack/identifying-unc2452-related-techniques-9f7b6c7f3714)

### MindMap - Solarigate/Sunburst Supply chain Attack
<figure>
<img src="https://raw.githubusercontent.com/zer0trustsec/zer0trustsec.github.io/master/_posts/solarwinds_solaris_blueteam_ir/SOLORIGATE_SUNBURST.png" alt="">
<figcaption> Solarigate/Sunburst - Mindmap </figcaption>
</figure>


### Reference Articles:
- [Sophos - Threat Hunting](https://github.com/sophos-cybersecurity/solarwinds-threathunt)
- [TrustedSec - Article](https://www.trustedsec.com/blog/solarwinds-backdoor-sunburst-incident-response-playbook/)
- [Fireeye](https://www.fireeye.com/blog/threat-research/2020/12/evasive-attacker-leverages-solarwinds-supply-chain-compromises-with-sunburst-backdoor.html)
