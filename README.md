[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://ejurgensen.github.io/forked-daapd/
[hub]: https://hub.docker.com/r/lsioarmhf/daapd-aarch64/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/daapd-aarch64
[![](https://images.microbadger.com/badges/version/lsioarmhf/daapd-aarch64.svg)](https://microbadger.com/images/lsioarmhf/daapd-aarch64 "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/daapd-aarch64.svg)](http://microbadger.com/images/lsioarmhf/daapd-aarch64 "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/daapd-aarch64.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/daapd-aarch64.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/arm64/arm64-daapd)](https://ci.linuxserver.io/job/Docker-Builders/job/arm64/job/arm64-daapd/)

[Forked-Daapd][appurl] (iTunes) media server with support for AirPlay devices, Apple Remote (and compatibles), Chromecast, MPD and internet radio.

[![daapd](https://raw.githubusercontent.com/linuxserver/beta-templates/master/lsiodev/img/daapd-git.png)][appurl]

## Usage

```
docker create \
--name=daapd \
-v <path to data>:/config \
-v <path to music>:/music \
-e PGID=<gid> -e PUID=<uid>  \
--net=host \
lsioarmhf/daapd-aarch64
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `--net=host` - must be run in host mode
* `-v /config` - Where daapd server stores its config and dbase files.
* `-v /music` - map to your music folder
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it daapd /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application 
`IMPORTANT... THIS IS THE ARM64 VERSION`

Map your music folder, open up itunes on the same LAN to see your music there.
For further setup options of remotes etc, check out the daapd website, [Forked-daapd][appurl].

## Logs and shell
* To monitor the logs of the container in realtime `docker logs -f daapd`.
* Shell access whilst the container is running: `docker exec -it daapd /bin/bash`

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' daapd`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/daapd-aarch64`

## Versions

+ **03.12.17:** Initial Release.