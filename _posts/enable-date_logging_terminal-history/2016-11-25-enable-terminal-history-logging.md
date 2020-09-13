---
title: Security Admin Tip- Enable terminal history logging
date: 2016-11-22 07:50:00 +07:00
tags: [linux, admin, history]
description: Lazy Linux admins should enable below history logging.
---

Most of the times, When i was handling some IR investigations, I found some missing part and important artifacts in Linux machines. As a DFIR investigator, we do timeline analysis and look at malicious command execution history in linux machines.

But most of the lazy linux administrators were not enabling the history logging with date in linux machines. We don't see those command logging capabilities in most of the organisations, It will be very challenging for DFIR investigators while handling the incidents.

I would like to share some quick tip for all lazy linux administrators.

#### Bash command history date logging configuration
```bash
$ echo 'export HISTTIMEFORMAT="%d/%m/%y %T "' >> ~/.bash_profile
$ cat ~/.bash_profile
$ source ~/.bash_profile
$ history
```
