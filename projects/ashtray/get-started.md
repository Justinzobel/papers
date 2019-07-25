---
description: Quick start instructions
---

# Get started

## Installation

As any other Solus-Project handled repository, you can use `eopkg *-repo` subcommands to handle this one. Hence, the installation instruction is pretty straightforward:

```text
eopkg add-repo streambinder https://solus.davidepucci.it/eopkg-index.xml.xz
```

If you want it to point to a specific GitHub release - represented by the `$TAG` variable:

```text
eopkg add-repo streambinder https://github.com/streambinder/ashtray/releases/download/$TAG/eopkg-index.xml.xz
```

You may notice in the first case `solus.davidepucci.it` host name gets used, while in the latter you would be pointing directly to the GitHub repository: I get more in depth about this on the [Infrastructure page](infrastructure.md#packages-free-hosting).

## Uninstall

```text
eopkg remove-repo streambinder
```

## Enable / Disable

```text
eopkg enable-repo streambinder
eopkg disable-repo streambinder
```

