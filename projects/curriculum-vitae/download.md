---
description: How to catch latest version
---

# Download

To download latest version, please, reach latest GitHub repository release clicking below:

{% embed url="https://github.com/streambinder/curriculum-vitae/releases/latest" caption="CV latest release" %}

Otherwise, if you want to grab it from shell, you can use the following snippet:

```bash
lang="it"
variant="europass"
release="https://github.com/streambinder/curriculum-vitae/releases/latest"
origin="$(curl -I "${release}" | \
    grep ^Location\: | \
    cut -d' ' -f2 | \
    tr -cd "[:print:]" | \
    sed 's/\/tag\//\/download\//g')"
wget "${origin}/${variant}.${lang}.pdf"
```

