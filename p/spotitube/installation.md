---
description: Quick start instructions
---

# Installation

Spotitube binaries and packages are hosted on GitHub, in project's [_Releases_ section](https://github.com/streambinder/spotitube/releases). It actually supports all the common platforms know, such as generic Linux/Unix systems and Windows.

{% embed url="https://github.com/streambinder/spotitube/releases" %}

For Solus-Project, RedHat-based, Debian-based distributions users, there's an installable package, while for the others Linux/Unix users a generic binary can be used. For Windows users, an _exe_ binary variant is there, too.

### Dependencies

As already mentioned it heavily uses `youtube-dl` to download tracks from _YouTube_ and `ffmpeg` to convert them to _mp3_. You absolutely need them. Thus, it's written in `GO-lang`: assure you actually own it.

| Dependency | Version | Dependency type |
| :--- | :--- | :--- |
| `youtube-dl` | _none in particular_ | Runtime |
| `ffmpeg` | _none in particular_ | Runtime |
| `golang` | 1.7+ | Compilation |

## Updating

Theoretically, Spotitube is taught to be self-updated if not running an updated version. Anyway, nothing forbids you to download and install latest package/binary over the old one.

## Building from source

Behind this tool there's a Spotify application that gets called during the authentication phase, which Spotify gives permissions to, to read many informations, such as the user name, library and playlists. When you use _Spotitube_ for the very first time, Spotify will ask you if you really want to grant this informations to it.

The Spotify application gets linked to this go-lang code using the `SPOTIFY_ID` and the `SPOITIFY_KEY` provided by Spotify to the user who created the application \(me\). It's not a good deal to hardcode these application credentials into the source code \(as I previously was doing\), letting anyone to see and use the same ones and letting anyone to pretend to be _Spotitube_, being then able to steal such informations, hiding his real identity. This is the reason behind the choice to hide those credentials from the source code, and applying - expliciting as environment variables - them during the compilation phase. On the other hand, this unfortunately means that no one can compile the tool but me \(or anyone else which the keys are granted to\): if you want, you can easily create an application to the Spotify [developer area](https://beta.developer.spotify.com/dashboard/applications) and use your own credentials.

For the ones moving this way, keep in mind:

1. `SPOTIFY_KEY` is associated to `SPOTIFY_ID`: if you create your own app, remember to override both values provided to you by Spotify developers dashboard;
2. If you do not want to manually alter the code to make SpotiTube listen on different URI for Spotify authentication flow completion, you'd better set up `http://localhost:8080/callback` as callback URI of your Spotify app.

Anyway, the effective way to build it is pretty straightforward:

```text
git clone https://github.com/streambinder/spotitube
cd spotitube
# the following SPOTIFY_ID and SPOTIFY_KEY are bogus
# read the "Spotify application keys" section for further informations
SPOTIFY_ID=YJ5U6TSB317572L40EMQQPVEI2HICXFL SPOTIFY_KEY=4SW2W3ICZ3DPY6NWC88UFJDBCZJAQA8J make
# to install system-wide
sudo make install
# otherwise you'll find the binary inside ./bin
```

#### 

### Building on Windows \(thanks to @[Coul33t](https://github.com/Coul33t)\)

**Prerequisites:**

* [Golang](https://golang.org/): Used to compile the code
* [Git](https://git-scm.com/): Used to retrieve the code from Github
* [GnuWin32](https://sourceforge.net/projects/gnuwin32/files/make/3.81/make-3.81.exe/download): Used for the makefile

**Optional:**

* [CMDer](https://cmder.net/): better terminal for Windows \(includes Git\)

**Step by step tutorial**

1. Use `cd` to go to the desired location for the program, _e.g._ `cd C:\Users\YourUsername\Documents\Programmation\Go`
2. Clone the repository here: `git clone https://github.com/streambinder/spotitube.git`
3. Set the GOPATH variable to the code folder location, _e.g._ `SET GOPATH=C:\Users\YourUsername\Documents\Programmation\Go\spotitube`
4. Now, there's a bunch of libraries to download. You can copy and paste all of this into your terminal, this should download everything needed \(else, copy, paste and execute each line after another\):

```text
go get github.com\0xAX\notificator
go get github.com\PuerkitoBio\goquery
go get github.com\agnivade\levenshtein
go get github.com\bogem\id3v2
go get github.com\bradfitz\slice
go get github.com\fatih\color
go get github.com\jroimartin\gocui
go get github.com\gosimple\slug
go get github.com\lunixbochs\vtclean
go get github.com\mozillazg\go-unidecode
go get github.com\zmb3\spotify
```

1. Now, use the GnuWin32 `make` tool to build the project, e.g. `"C:\Program Files (x86)\GnuWin32\bin\make.exe" SPOTIFY_ID=SPOTIFYAPIID SPOTIFY_KEY=SPOTIFYSECRETAPIKEY` \(while you're in the `spotitude` root folder\). You MUST specify the API keys \(see the Spotify application keys section\). This should generate an `out/` folder
2. Go to [https://ytdl-org.github.io/youtube-dl/download.html](https://ytdl-org.github.io/youtube-dl/download.html), download the **Windows exe** and put it into the `spotitube/out/` folder
3. Go to [https://ffmpeg.zeranoe.com/builds/](https://ffmpeg.zeranoe.com/builds/) and download the **SHARED** library \(select **Shared** in the **Linking** column, to the right\). Open the archive, go into the `bin/` folder, and copy/paste everything into the `spotitube/out/` folder
4. You're almost there. Now go on Spotify, and find a playlist you want to export. Right click on it, then go to **share**, then **copy Spotify URI**
5. Now, launch the exe with your terminal
6. Once you've done this, the program will launch, and stop at the `Authentication URL:` line. Copy the URL, and paste it into your browser. Allow the access, and the download should start

