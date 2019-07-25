---
description: What is Ashtray?
---

# About

## What is it

{% embed url="https://github.com/streambinder/ashtray" caption="" %}

**Ashtray** is a custom and private `eopkg` repository. `eopkg` is the packaging format conceived and adopted by [Solus-Project](https://getsol.us), a Linux desktop distribution built from scratch.

This private repository was born by the need of having a place where to put custom packages which were not included by default on official repository.

The most important component hosted on this repository is Pantheon Desktop, which is the Desktop Environment developed by the [Elementary OS](https://elementary.io) team and which hasn't been included on Solus-Project repository due to [legitimate reasons](https://discuss.getsol.us/d/1500-how-to-generate-custom-iso/12). This is the answer I got from one of the development team members as a reply to my _why won't Pantheon Desktop be officially supported?_:

> Because Pantheon, first-and-foremost, is designed **for** elementary OS. To such a degree that I had to patch Granite, their toolkit that everything of theirs uses, to not segfault when using DateTime APIs when it **assumed** you had their Pantheon schemas for time set. And working with them as a downstream would be miserable, they can't even merge a single one of my PRs in. Fixing an entire desktop and all their applications to work **as we expect** them to? That's a hard nope.
>
> Pantheon, like Cinnamon, XFCE, etc. will never be supported or provided by us.

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

You may notice in the first case `solus.davidepucci.it` host name gets used, while in the latter you would be pointing directly to the GitHub repository: I get more in depth about this on the [Infrastructure page](infrastructure.md#packages-free-hosting).

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



