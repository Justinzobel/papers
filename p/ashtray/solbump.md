---
description: Automatic eopkg package files updating system
---

# Solbump

Solbump is a tool to automatically upgrade `eopkg` YAML-formatted source files to latest releases. Hence, the naming similarity with `solbuild`, the tool made from Solus project core team to build `eopkg` packages.

Based on the amount of defined \(and pluggable\) providers, it tries to recognize the format of the tarballs or archives defined as source files from the YAML file and find a matching provider. Then it's able to query for a more updated release and, if so, it fetches the asset, calculates the hashsum and update the original `package.yml` coherently.

## Usage

Using the tool is pretty straightforward:

```text
solbump package1.yml package2.yml package3/package.yml
```

## Installation

At the moment, the only way of installing the tool is relying on GO toolset:

```text
go get github.com/streambinder/solbump
```

