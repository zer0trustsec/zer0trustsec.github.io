---
title: Is your saved passwords were safe in browser?
date: 2016-11-24 09:00:00 +07:00
tags: [browser, access, data, collection, redteam]
description: Stealing saved passwords (Autofill enabled) from browsers POC code
---

In this article, I would like to share the server-side source code for stealing auto-fill saved passwords from modern browsers. It might be useful for Penetration testers or Red Teams.

#### Demo Steps:
1. User's should enter the dummy username/password from available form.
2. Save the password in browser
3. XSS code technique will steal password from auto-filled password field.

##### Server side-source code:

<figure>
<img src="{{site.baseurl}}/stealpasswords-modern-browsers-autofill-privacy/code.png" alt="Server-side source code">
<figcaption>PHP code</figcaption>
</figure>

#### Demo Website

[ Public hosted Attacker Server - May takedown in future](http://133.242.134.241/exploit/password_manager.php)
