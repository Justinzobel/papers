---
description: Quick start instructions
---

# Installation

Spotitube binaries and packages are hosted on GitHub, in project's [_Releases_ section](https://github.com/streambinder/spotitube/releases). It actually supports all the common platforms known, such as generic Linux/Unix systems and Windows.

{% embed url="https://github.com/streambinder/spotitube/releases" %}

For Solus-Project, RedHat-based, Debian-based distributions users, there's an installable package, while for the others Linux/Unix systems users a generic binary can be used. For Windows users, an _exe_ binary variant is there, too.

### Dependencies

| Dependency | Version | Type |
| :--- | :--- | :--- |
| `youtube-dl` | _none in particular_ | Runtime |
| `ffmpeg` | _none in particular_ | Runtime |
| `golang` | 1.7+ | Compilation |

## Updating

Theoretically, Spotitube is taught to be self-updated if not running an updated version. Anyway, nothing forbids you to download and install latest package/binary over the old one.

## Building from source

Behind this tool there's a Spotify application that gets called during the authentication phase, which Spotify gives permissions to, to read many informations, such as the user name, library and playlists. When you use _Spotitube_ for the very first time, Spotify will ask you if you really want to grant this informations to it.

The Spotify application gets linked to this go-lang code using the `SPOTIFY_ID` and the `SPOITIFY_KEY` provided by Spotify to the user who created the application \(me\). It's not a good deal to hardcode these application credentials into the source code \(as I previously was doing\), letting anyone to see and use the same ones and letting anyone to pretend to be _Spotitube_, being then able to steal such informations, hiding his real identity. This is the reason behind the choice to hide those credentials from the source code, and applying - expliciting as environment variables - them during the compilation phase.

If you want, you can easily create an application to the Spotify [developer area](https://beta.developer.spotify.com/dashboard/applications) and use your own API credentials.

For the ones moving this way, keep in mind:

1. `SPOTIFY_KEY` is associated to `SPOTIFY_ID`: if you create your own app, remember to override both values provided to you by Spotify developers dashboard. In order to do so, keep in mind these points:
   1. During the compilation phase, if `SPOTIFY_KEY` and `SPOTIFY_ID` variables are shell-exported as environment keys, the `Makefile` will hardcode them into the binary.
   2. If no environment key is found, the resulting binary will need ones everytime its getting executed \(still, as environment keys\).
2. By default, the application is coded to use the following redirect URIs:

   1. `http://127.0.0.1:8080/callback`
   2. `http://localhost:8080/callback`
   3. `http://spotitube.local:8080/callback`

   Assure you configure your Spotify application to allow them.

### Effective build

```bash
git clone https://github.com/streambinder/spotitube
cd spotitube
make
```

The resulting binary will be placed inside newly created `./out` folder. If you want to install it widely in the system:

```bash
sudo make install
```

#### Passing Spotify API credentials

```bash
# the following SPOTIFY_ID and SPOTIFY_KEY are bogus
SPOTIFY_ID=YJ5U6TSB317572L40EMQQPVEI2HICXFL \
    SPOTIFY_KEY=4SW2W3ICZ3DPY6NWC88UFJDBCZJAQA8J \
    make
```

### Running on Windows

1. Install [GnuWin32](https://sourceforge.net/projects/gnuwin32/files/make/3.81/make-3.81.exe/download)
2. Create a folder `Spotitube` wherever you want
3. Download [`youtube-dl`](https://ytdl-org.github.io/youtube-dl/download.html) and place it inside `Spotitube` folder
4. Download [`ffmpeg`](https://ffmpeg.zeranoe.com/builds/) \(choose the `shared` version\) and place it inside `Spotitube` folder 
5. Download latest Spotitube `exe` variant release and place it inside `Spotitube` folder
6. Enter `Spotitube` folder using GnuWin32 and enjoy Spotitube

