[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://github.com/jfurrow/flood
[hub]: https://hub.docker.com/r/linuxserver/flood/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# linuxserver/flood
[![](https://images.microbadger.com/badges/version/linuxserver/flood.svg)](https://microbadger.com/images/linuxserver/flood "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/linuxserver/flood.svg)](http://microbadger.com/images/linuxserver/flood "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/linuxserver/flood.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/linuxserver/flood.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io/linuxserver-flood)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io/job/linuxserver-flood/)

[Flood][appurl], a modern web UI for rTorrent with a Node.js backend and React frontend.

[![flood](https://s3.amazonaws.com/johnfurrow.com/share/flood-screenshot-a-0606.png)][appurl]

## Usage

```
docker create \
  --name=flood \
  -v <path to data>:/config \
  -v <path to downloads>:/downloads \
  -e PGID=<gid> -e PUID=<uid>  \
  -p 3000:3000 \
  linuxserver/flood
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`



* `-p 3000` - the port(s)
* `-v /config` - where flood should store it's config files
* `-v /downloads` - path to your downloads folder
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it flood /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application


## Info

* Shell access whilst the container is running: `docker exec -it flood /bin/bash`
* To monitor the logs of the container in realtime: `docker logs -f flood`

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' flood`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' linuxserver/flood`

## Versions

+ **dd.MM.yy:** Initial Release.
