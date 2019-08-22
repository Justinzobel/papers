---
description: What is Chopper?
---

# About

Chopper is a CLI application which has been built to provide a simple way to exchange all-sizes files over the internet.

It relies on generic free storage providers which offer lot of little space: Chopper basically distributes all the parts of the files over those storages building a manifest that keep tracks of all the pieces.

The resulting manifest file can then be exchanged and used to let Chopper reconstruct the original file.

## How to use

The way it can be used is very simple. If you want to _chop_ a file \(upload it and generate an exchangeable file\):

```bash
chopper filename.mp4
```

If you want to increase _chop_ redundancy:

```bash
chopper -r 3 filename.mp4
```

If you want to rebuild a file starting from its manifest:

```bash
chopper build filename.chop
```

