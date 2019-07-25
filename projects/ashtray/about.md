---
description: What is Ashtray?
---

# About

**Ashtray** is a custom and private `eopkg` repository. For the ones who do not know what `eopkg` actually is, it is the packaging format conceived and adopted by [Solus-Project](https://getsol.us), which is a Linux desktop distribution built from scratch.

This private repository was born by the need of having a place where to put custom packages which were not included by default on official repository.

The most important component hosted on this repository is Pantheon Desktop, which is the product developed by the [Elementary OS](https://elementary.io) team and which wasn't to be included on Solus-Project repository due to [legitimate reasons](https://discuss.getsol.us/d/1500-how-to-generate-custom-iso/12).

## Getting started

### Installation

As any other Solus-Project handled repository, you can use `eopkg *-repo` subcommands to handle this one. Hence, the installation instruction is pretty straightforward:

```text
eopkg add-repo streambinder https://solus.davidepucci.it/eopkg-index.xml.xz
```

If you want it to point to a specific GitHub release - represented by the `$TAG` variable:

```text
eopkg add-repo streambinder https://github.com/streambinder/ashtray/releases/download/$TAG/eopkg-index.xml.xz
```

You may notice in the first case `solus.davidepucci.it` host name gets used, while in the latter you would be pointing directly to the GitHub repository: the repository is actually hosted on GitHub and not anywhere else, but I get more in depth about this on a dedicated page.

### Uninstall

```text
eopkg remove-repo streambinder
```

### Enable / Disable

```text
eopkg enable-repo streambinder
eopkg disable-repo streambinder
```

### 



