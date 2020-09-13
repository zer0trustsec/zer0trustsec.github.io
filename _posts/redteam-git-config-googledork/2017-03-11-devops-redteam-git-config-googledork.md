---
title: Redteam Tip -  Google dork for .git folder exposure
date: 2017-03-11 10:00:00 +07:00
tags: [github, googledork, defense]
description: Google dork to identify the git
---

As a part of OSINT/Recon activity to identify sensitive information for specific organisation/website most of the security engineers were using Google dorks. In this article we were identifying the vulnerable websites which exposes .git folders in their web servers.

##### Google Dork - .git folder exposure:

<figure>
<img src="https://raw.githubusercontent.com/zer0trustsec/zer0trustsec.github.io/master/_posts/redteam-git-config-googledork/gdrkgit.png" alt="Google Dork .git">
<figcaption> git folder google dork </figcaption>
</figure>


#### Google Dork:
```text
intext:"index of /.git" "parent directory"
```
#### Defend .git folder exposed Web servers:
```cfg
<Directory ~ “\.git”>
Order deny,allow
Deny from all
</Directory>
```

#### Tools used:
[Google](https://www.google.com)
