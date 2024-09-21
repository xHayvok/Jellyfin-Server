# Jellyfin-Server
Describing my Jellyfin Server setup to make maintenance easier. This repository could hopefully be used to setup a clone of my exact server, in the case something catastrophic happens.


## Server Machines

### Server 1 (minecraft)
This server is running Debian 12 with no desktop environment.
Nicknamed "minecraft" as this was originally used as just a minecraft server for friends. I wont go into detail about the actual minecraft server as its irrelevant to Jellyfin, how ever it was initially setup following [this tutoial](https://youtu.be/bAGTwBURBXc?si=ozyF0t9Y1e66vMRb).
Going forward "minecraft" or "minecraft server" will refer to the physical server itself, and not the minecraft world currently running on it.
#### Hardware
Started from a low tier gaming PC, slowely upgrade over the years, usually when I upgraded my personal gaming rig. lshw was used to find most of the hardware information.
- MOBO:
    - MSI MPG Z390 GAMING PLUS (MS-7B51)
    - LGA1155 Socket
    - Intel Z390 Chipset
    - 4 DDR4 RAM slots
    - Gigabit Ethernet
- CPU:
    - Intel Core i7-9700F
    - 8 cores, 8 threads
    - Running at 3.6 GHz
        - Boost to 4.9 GHz
- RAM:
    - 4 8GiB @ 2933MHz
        - Corsair Vengence
- GPU:
    - Nvidia GTX 1060 6GB
- PSU:
    - 500w? Corsair?
- Storage:
    - Boot: 1 TB WD NVMe SN550
    - Videos: 4 TB WD HDD
        - GoPro Footage, only in this system due to lack of a better place

### Server 2 (qvex)
This server is running Debian 12 with a default desktop environment for not other reason than I thought I might use it in the future.
Nicknamed "qvex" because I wanted something easy to remember and hard to confuse with anything else.
This server is effectively just a NAS, but also does any downloading and file organizing required for my libraries.
#### Hardware
This is a Dell Optiplex 7010 from around 2014.
- MOBO:
    - Dell 0GY6Y8
    - LGA1155 Socket
    - Intel Q77 Chipset
    - 4 DDR3 RAM slots
    - Gigabit Ethernet
- CPU:
    - Intel Core i3-3240
    - 2 cores, 4 threads
    - Running at 3.4 GHz
- RAM:
    - Stock: 2 Samsung 4GiB @ 1600MHz
    - Added: 1 Hynix 4GiB @ 1600MHz
- PSU:
    - 275W Stock Dell PSU
- Storage:
    - Boot: Stock 500 GB HDD
    - Downloads: Used 8 TB HDD
        - Shucked WD External drive (I believe)
    - Storage: 2 WD Red 10 TB HDD
        - RAID 1 array for redundency


## CasaOS
CasaOS is the main interface I used for initial setup, as well as maintenance.

- Minecraft:
    - Crafty
       - Crafty Controller is used to manage my Minecraft servers, not relevant to the scope of ths repository. Mostly stock from CasaOS app store, though  did have to add a port for the Voice Chat mod.
    - Homarr
        - Homarr Dashboard is a really pretty collection of links from both servers. It also has widgets for torrents, Jellyseerr requests, Jellyfin sessions, media requests stats, and a calender for upcomng releases.
    - Jellyfin
        - Jellyfin is the media server which is the heart of this whole project. More information on plugins listed below.
    - Jellystat
        - Jellystat tracks statistics from Jellyfin and presents it in a very nice webUI.
    - Jellyseerr
        - Jellyseerr is a really nice way to request new media. Its integrated with Radarr and Sonarr.
    - Octoprint
        - Octoprint is a web interface for controlling my 3D printer. Not relevant to this repository
    - AdGuard Home
        - AdGuard Home is a DNS server that automatically blocks unwanted trackers and ads. Not currently used, i'm planning on using PiHole instead at some point in the future.
    - bTop
        - bTop is a system monitor tool that looks pretty cool
    - Netdata
        - Netdata is a system monitor that gives more information than bTop, but doesnt look as nice, and is harder to read.
    - Wireguard Easy
        - Wireguard is a VPN tunneling tool, I currently us NordVPN Meshnet for this, but wireguard seems to be a more straight forward, so I'm going to look into using it in the future.
    - Home Assistant
        - Home Assistant is use to control smart home devices. I dont have any, and have not set up HA. I added this so I can look into it in the future, to turn my 3D printer on and off.

- Qvex:
    - qBitTorrent
        - qBitTorrent is used to download new media through bittorrent protocol
    - FlareSolverr
        - FlareSolverr is a bypass for indxers that use Cloudflare. Added with custom Docker Compose.
    - Prowlarr
        - Prowlarr is an indexer manager. Part of the Servarr suite. Added with custom Docker Compose. Integrated with Radarr, Sonarr, Lidarr, and Readarr.
    - Radarr
        - Radarr is used to search for new movies. Part of the Servarr suite. Added with custom Docker Compose. Integrated with Prowlarr, qBitTorrent and JellySeerr.
    - Sonarr
        - Sonarr is used to search for new TV shows. Part of the Servarr suite. Added with custom Docker Compose. Integrated with Prowlarr, qBitTorrent and JellySeerr.
    - Lidarr
        - Lidarr is used to search for new music. Part of the Servarr suite. Added with custom Docker Compose. Integrated with Prowlarr and qBitTorrent.
    - Readarr
        - Readarr is used to search for new books. Part of the Servarr suite. Added with custom Docker Compose. Integrated with Prowlarr and qBitTorrent.
    - Bazarr
        - Bazarr is use to grab subtitles. Currently its unused as something else seems to be grabbing subs, or every download already comes with them. May be removed in the future. Added with custom Docker Compose.
    - [Gluetun](https://github.com/qdm12/gluetun)
        - Gluetun is a VPN app. Using my NordVPN account I'm able to put all previously mentioned programs on Qvex behind a VPN, though most dont need it. Added with custom Docker Compose.
    - bTop
        - bTop is a system monitor tool that looks pretty cool
    - Autobrr
        - Added for a reason I'm sure, cant remember it though. Will review in the future.

### Repositories
Minecraft and Qvex have these CasaOS app store repositories added:
- [Big Bear CasaOS App Store](https://github.com/bigbeartechworld/big-bear-casaos)
- [CasaOS Coolstore](https://github.com/WisdomSky/CasaOS-Coolstore)


## Jellyfin Setup
### Libraries
I believe all libraries are setip mostly identicle with the following settings: Prefered download language: English, Country: United States, Realtime nonitoring enabled, Automatically add to collection, Fanart is first for images, save artwork into media folders, Trickplay enabled extract with library scan. Metadata heirarchy is pretty straight forward, for movies TMDB goes first, TV its TVDB first. 
### Transcoding
Nvidia NVENC hardware acceleration. Enable hardware decoding for: H264, HEVC, MPEG2, VC1, VP9, HEVC 10bit. Enable enhanced NVDEC decoder. Enable hardware encoding. Encoding format options: Allow encoding in HEVC format. The rest should be left to defaults I believe, Throttle Transcodes is disabled.
### Plugins
a list of plugins currently deployed in Jellyfin
- Stock Plugins: AudioDB, MusicBrainz, OMDb, Studio Images, TMDb
- Added Plugins: Fanart.TV, Into Skipper, Merge Versions, Playback Reporting, Reports, SkinManager, TMDb Box Sets, TVmaze, TheTVBD, Webhook

### Repositories 
- [Jellyfin Plugin Manifest](https://github.com/danieladov/JellyfinPluginManifest)
- [Jellyfin Webhook Plugin](https://github.com/jellyfin/jellyfin-plugin-webhook)
- [Intro Skipper (beta)](https://github.com/jumoog/intro-skipper)


## Useful links
- [Software RAID Walkthrough](https://wiki.debian.org/SoftwareRAID)
- [Add nvidia runtime to docker runtimes](https://stackoverflow.com/questions/59008295/add-nvidia-runtime-to-docker-runtimes)
- [NVIDIA Drivers for Debian 12 - Step by Step](https://www.reddit.com/r/linux4noobs/comments/18n34c3/nvidia_drivers_for_debian_12_step_by_step/)
- [Video Encode and Decode GPU Support Matrix](https://developer.nvidia.com/video-encode-and-decode-gpu-support-matrix-new)
- [How to mount smb share on ubuntu 18.04](https://askubuntu.com/questions/1050460/how-to-mount-smb-share-on-ubuntu-18-04)
- https://ipleak.net
- [Servarr Docs](https://wiki.servarr.com)
- [TRaSH Guides](https://trash-guides.info)
- Adding drives to linux
    - [How to Mount and Access Windows NTFS Drives in Linux](https://www.makeuseof.com/mount-ntfs-windows-drives-in-linux/)
    - [What is the equivalent for switching drives in terminal on Linux?](https://askubuntu.com/questions/100568/what-is-the-equivalent-for-switching-drives-in-terminal-on-linux)