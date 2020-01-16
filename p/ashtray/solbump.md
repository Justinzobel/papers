---
description: Automatic eopkg package files updating system
---

# Solbump

Solbump is a tool to automatically upgrade `eopkg` YAML-formatted source files to latest releases. Hence, the naming similarity with `solbuild`, the tool made from Solus project core team to build `eopkg` packages.

Based on the amount of defined \(and pluggable\) providers, it tries to recognize the format of the tarballs or archives defined as source files from the YAML file and find a matching provider. Then it's able to query for a more updated release and, if so, it fetches the asset, calculates the hashsum and update the original `package.yml` coherently.

## Usage

Before starting using the tool, further actions need to be taken, in order to access all its capabilities. In fact, few providers could be in the need of API tokens or specific configurations. So create the configuration file and, depending on your needs, fill it with data you own:

{% code title="~/.config/solbump" %}
```text
# To obtain the token, go to:
# https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line#creating-a-token
# Solbump does not require any scope to be enabled.
github:
    api: habmfnlzrwmxuopmjganlqfpmccouxieijlouxcl

# To obtain the token, go to:
# https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html
# Solbump requires only the API access scope enablement.
gitlab:
    api: hmlhnbzndrogcifs-akb
```
{% endcode %}

Using the tool is pretty straightforward:

```text
solbump package1.yml package2.yml package3/package.yml
```

## Installation

At the moment, the only way of installing the tool is relying on GO toolset:

```text
go get github.com/streambinder/solbump
```

