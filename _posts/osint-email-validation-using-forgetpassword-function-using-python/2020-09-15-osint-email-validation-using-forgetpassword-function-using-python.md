---
title: OSINT - Email validation using forget-password functionality (Python).
date: 2020-09-15 19:00:00 +07:00
tags: [osint, python, email, recon, validation]
description: Validate the emails on multiple websites
---

These days most of OSINT guys were doing their investigations on humans/unknown emails data. Sometimes threat actor/attackers also do mistakes while creating accounts in multiple platforms. We have to take those mistakes as an advantage in our investigations, so most of the email addresses will be unknown in lot of Threat Intel investigations.

In this post, I would like to share one of the interesting github project which can take email address as an input and checking in top websites using "forget password" functionality.


#### Github Project:
[Github- Holehe Project - https://github.com/megadose/holehe](https://github.com/megadose/holehe)
##### Prerequisites:
```bash
pip3 install holehe==1.51
```
##### Installation:
```bash
git clone https://github.com/megadose/holehe.git
cd holehe/
python3 setup.py install
```
##### Demo:
<figure>
<img src="https://raw.githubusercontent.com/zer0trustsec/zer0trustsec.github.io/master/_posts/osint-email-validation-using-forgetpassword-function-using-python/demo.gif" alt="Powershell code">
<figcaption>Powershell command</figcaption>
</figure>

##### Import as Python module:
```python
from holehe import *
print(adobe("test@gmail.com"))
print(lastpass("test@gmail.com"))
```

#### References
- [Github](https://github.com/megadose/holehe-maltego)
