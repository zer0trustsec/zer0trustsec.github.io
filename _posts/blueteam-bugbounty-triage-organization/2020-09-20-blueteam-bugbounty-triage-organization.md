---
title: Blue Team - Bug Bounty Triage - Challenges & Triage Workflow for CSIRT teams
date: 2020-09-20 1:00:00 +07:00
tags: [blueteam, bugbounty, triage, workflow, bugs]
description: Workflow for Bug Bounty Submissions
---

 In these days bug bounty programs were popular and most of the organisations were enrolled to multiple bug bounty platforms or running their own vulnerability disclosure programs. While running these programs, most of the security researchers/hunters actively scanning/enumerating particular scope of company external infrastructure.

##### Bug bounty Platforms:
1. [HackerOne](https://hackerone.com/security)
2. [Bug Crowd](https://www.bugcrowd.com/bug-bounty-list/)
3. [Yogosha](https://yogosha.com/)

Most of the organizations doesn't have idea on what challenges CSIRT/SOC/InfoSec teams will face while handling Bug Bounty Incidents/Submissions, sometimes they don't have proper IR plan/Workflow to handle Bug Bounty Incidents/Submissions. So, Here I shared some insights about the common challenges & bug-bounty triage workflows which can helpful for Blue Teams (CSIRT/SOC/InfoSec)

### Common challenges for CSIRT / SOC teams - Handling Bug Bounty Incidents:

- Most of the security researchers/bug-bounty hunters will scan the company infrastructure and generate lot of traffic on external perimeter. While doing scanning activity, our security teams will get high volume of security alerts in their Defense tools.
- Lot of organisations doesn’t have proper internal documentation for handling the Bug bounty incidents.(Direct/ Platforms)
- Skill gap: Lack of knowledge on AppSec and not able to understand the security researcher POC submission.
- Developers Team: Even security teams able to explain the application vulnerability to Dev/App teams, they were unable to understand why this flaw came and no knowledge on fixing part.  


### Preparation - Bug Bounty/Vulnerability Disclosure Program:

- Asset management is very critical for any of the organisations. If assets information is regularly maintained/updated by Sysadmins/DevOps/Dev/App teams, our security teams can easily identify the assets / application own information.
- Good Sync with App/Developer/Test teams. While reporting about the incident to appropriate team, we have to provide in-detailed technical information and recommendations as well. If they have any challenges while fixing the issue, security teams should have support them.  
- Based on the critical of the bug, security teams should have SLAs with other teams while handling these incidents. It should be integrated with ticketing system.
- External perimeter critical devices/apps IP/Host/Owner information should be captured in Vulnerability Management Systems.(Qualys/Nessus etc.)

### Key players to Triage Bug Bounty Incidents:

##### Platform:
These days companies are enrolling multiple bug-bounty platforms like hacker one etc.Those platforms provides the company vulnerability disclosure program information like policies, scope of the infrastructure, guidelines etc. And if any security researcher/hunter submitted bugs their platform, they will validate and informed to company’s security team.
##### Security Analyst:
Each company having access to bug bounty portal access to see all bug bounty submissions. Analyst will analyse and inform this to Senior Engineers to get understand about the bug.
#####  Sr.Security Engineer (AppSec/Vulnerability Management):
Security engineers will understand the exact vulnerability and identify affected applications. Get more information about the technical and internal owner information and schedule meeting with appropriate internal teams. (Dev/App/SysAdmin/Cloud)
##### Lead Engineer:
If any bug is critical which can impact the production or confidential data exposure, they will co-ordinate with legal/PR/Technical teams to understand about the vulnerability or data exposure. If any old vulnerability is becomes a data-breach, they will informed to Management.
#####  Manager:
These people is continuously monitor the engineers how they were triaging and coordinate with other internal teams. If any gaps found, manager's should discuss with team members and get more ideas/inputs from them. Based on those inputs, they have to change their internal process documents for handling these Bug bounty incidents. If any critical escalations/data-breach linked bugs, they have to present in-front of C-suite to get their attention on these critical incidents.
##### System Admin Team:
Most of the companies having different offices across the world. So, local IT/Sysadmin teams were very critical while handling these type of incidents. Security teams always maintains good repo with these teams. It would be very helpful them to track down the asset/application/server owners information in their region.
##### Development/Application Team:
Most of the developers were focusing on their Product portfolio and features and maintenance. These days few organisations introduced DevSecOps culture to fix critical bugs/vulnerabilities in initial phases of the Development model. Developers also should have security knowledge to fix vulnerabilities in their applications.
##### Legal/Public Relations Team:
If any bug bounty incident is becomes a data breach incident, this team should have a visibility. Once it's confirmed, they will take necessary actions based on the data privacy laws.(GDPR regulations etc.)

### Types of Bug Bounty Submissions/Incidents:

1. Critical Vulnerabilities/Exploits (CVEs old version apps/softwares/packages etc.)
2. Web Application Vulnerabilities (OWASP Top 10, Authorization/ Logical flaws, Domain/Account takeover, OTP bypass, Injection attacks, XSS etc.)
3. Application Vulnerabilities (Buffer overflows, RCE, Reversing Exploits etc)
4. 3rd party apps (Other vendor app vulnerabilities)
5. Confidential Data Disclosure (Exposed Databases/Cloud Instances, Source code disclosure, Default credentials, Weak passwords, Misconfigurations (Cloud/Servers/Apps), Enumeration, Cryptographic)


#### Bug Bounty Triage - Workflow:

<figure>
<img src="https://raw.githubusercontent.com/zer0trustsec/zer0trustsec.github.io/master/_site/blueteam-bugbounty-triage-organization/bbwrkflow.png" alt="Bug Bounty Workflow">
<figcaption> BlueTeam - Bug Bounty Workflow </figcaption>
</figure>

##### Bug Bounty Triage - Steps:

1. Bug bounty portal will send alerts to security team when researcher's submitting their bugs/vulnerabilities.
2. Security teams will understand the impact of the bug bounty submission and prioritise accordingly (P1/P2/P3). They will create an incident in Ticketing system/ SOAR platforms.
3. Identify if submission related data leak/data breach incident. We have to inform the Legal/Public relation teams.  
4. Legal/PR teams will assess the impact and take necessary actions based on data privacy regulations and laws. Prepare the final report and send the data breach notification to affected users/orgs.
5. If submitted bug related to vulnerability/exploit/source code disclosure security teams will inform the specific technical teams to get more information about the specific application hosted location/owner/IP address etc.
6. Local IT teams/Application/SysAdmin/DevOps/Dev/Cloud teams will communicate with their internal teams based on initial information provided by Security Teams about the Vulnerability/Bug information.
7. Once identified the application owner/Asset/dev team, they have to fix the vulnerability/bug in their end.
8. Replicate/Validate the same bug on specific application by AppSec team/bug bounty researcher. Once it’s fixed it will be communicate the same to Security teams (CSIRT/SOC).
9. If this bug is not fixed properly, again go back to developers team and again explain the same by AppSec team.
10. Once bug is fixed specific application owner/Local IT team will inform the security team.
11. Security team will do investigation based on the bug/vulnerability. Here is below things to check.
```text
    (i).  Impact of the Vulnerability.
    (ii). If specific bug is used to exposing any confidential data.
    (iii).If this bug is already exposed by external threat actors or not.
    (iv). Any data exfiltrated via those apps using specific vulnerability/bug.
    (v).  Investigate affected vulnerable device/machine/application server. ( Forensic investigation)
```
12. Security (CSIRT/SOC) team will do investigate using SIEM logs on specific hits Server/DB/Application/affected devices.
13. Track the threat actors who were already exploited specific bug/vulnerability.
14. Prepare the final investigation report submitted to Management.
15. Close the incident in their Ticketing/SOAR systems once whole investigation completion.

#### Best Practices
- CSIRT/SOC/InfoSec should have knowledge on Application Security and able to understand the bug submissions. Train your analysts in AppSec space and organise Internal CTFs.
- AppSec & Dev teams should maintain good relations and give weekly sessions on AppSec space with Dev Teams.
- Security teams always support sysadmin/devops/cloud teams while handling these type of incidents. Train them on best security & hardening techniques while configure apps/servers/etc.
