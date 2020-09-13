---
title: DevOps Security - Scanning SSH keys for Weak credentials
date: 2017-02-21 21:00:00 +07:00
tags: [Devops, Security, Metasploit]
description: Scanning SSH keys for Weak credentials.
---

Most of the enterprise companies were migrating their infrastructure to cloud. They focused mainly on security in cloud, and DevOps teams were implementing CI/CD pipeline and integrating their tools with security tooling. In our article i would like to discuss to detect weak SSH credentials in DevOps environments using Metasploit tool.

#### DevOps Environment - Security Checks (SSH Keys):

1. Most of the DevOps environment VMs/Machines are using default credentials (vagrant/vagrant , root/vagrant)
2. Scanning the default SSH keys using metasploit - ssh_login_pubkey module.
3. Identify the weak SSH keys versions after the scan.
4. Login with Private key.
5. Get the vagrant/root shell.

##### DevOps - SSH weak keys scan:

<figure>
<img src="https://raw.githubusercontent.com/zer0trustsec/zer0trustsec.github.io/master/_posts/devops-vagrant-default-cred-check/Vagrant_SSH.gif" alt="DevOps - Security Checks">
<figcaption> Steps to Reproduce - DevSecOps (SSH Keys) </figcaption>
</figure>


#### Tools used:
[Metasploit](https://github.com/rapid7/metasploit-framework)
