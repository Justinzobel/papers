---
description: What is Spotitube?
---

# About

![](../../.gitbook/assets/sample.gif)

Impressive description apart, Spotitube is a CLI application to programmatically authenticate to your Spotify account, fetch some music and download the best YouTube results for it, keeping playlists files, metadata informations, album artworks, songs lyrics and maximizing _mp3_ files quality.

This project was born as per two needs:

1. I wanted to learn some _GO-lang_ basics.
2. I needed to automate the process of synchronize the songs I wanted to download. This process is composed by several phases:
   * Keep track of music I want to download
   * Find the best song file I can
   * Download it
   * Apply correct metadata

Spotitube basically solves these two major problems in a simple, elegant, but especially rapid way.

## Usage

The most common way to use it is to synchronize your library:

```bash
spotitube -folder ~/Music
```

If you want to synchronize a playlist:

```bash
spotitube -folder ~/Music -playlist spotify:user:$USERNAME:playlist:$PLAYLIST_ID
```

### Troubleshooting

Few additional flags have been implemented to simplify the troubleshooting and bugfixing process:

1. `-log` will append every output line of the application to a logfile, located inside the `-folder` the music is getting synchronized in.
2. `-debug` will show additional and detailed messages about the flow that brought the code to choose a song, instead of another, for example. Also, this flag will disable parallelism, in order to have a clearer and more ordered output.
3. `-simulate` will make the process flow till the download step, without proceeding on its way. It's useful to check if searching for results and filtering steps are doing their job.
4. `-disable-gui` will make the application output flow as a simple CLI application, dropping all the noise brought by the GUI-like aesthetics.

