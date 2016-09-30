[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/index.php/irc/
[podcasturl]: https://www.linuxserver.io/index.php/category/podcast/

[![linuxserver.io](https://www.linuxserver.io/wp-content/uploads/2015/06/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/photoshow
[![](https://images.microbadger.com/badges/image/lsioarmhf/photoshow.svg)](https://microbadger.com/images/lsioarmhf/photoshow "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/photoshow.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/photoshow.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-armhf/lsioarmhf-photoshow)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-armhf/job/lsioarmhf-photoshow/)
[hub]: https://hub.docker.com/r/lsioarmhf/photoshow/

[Photoshow][photoshowurl] is gallery software at its easiest, it doesn't even require a database. 

[![photoshow](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/photoshow-icon.png)][photoshowurl]
[photoshowurl]: https://github.com/thibaud-rohmer/PhotoShow

## Usage

```
docker create \
--name=photoshow \
-v <path to data>:/config \
-v <path to pictures>:/Pictures:ro \
-v <path to store thumbs>:/Thumbs \
-e PGID=<gid> -e PUID=<uid> \
-e TZ=<timezone> \
-p 80:80 \
lsioarmhf/photoshow
```

**Parameters**

* `-p 80` - port for the webui
* `-v /config` - stores config and logs for nginx base
* `-v /Pictures` - your local folder of photos you wish to share
* `-v /Thumbs` - local folder to store thumbnails of your images
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` - for timezone information *eg Europe/London, etc*

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it photoshow /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application 
`IMPORTANT... THIS IS THE ARMHF VERSION`

On first run create an admin account, any folder and its subfolders that you map to /Pictures will be presented as a webgallery. Config settings are persistent and stored as a subfolder of the /Thumbs mapping.


## Info

* To monitor the logs of the container in realtime `docker logs -f photoshow`.


## Versions
+ **30.09.16:** Initial Release. 
