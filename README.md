## Alpine microcontainer with Apache2

This is a micro docker container [![](https://images.microbadger.com/badges/image/krosh961/apache-alpine3.7.svg)](https://microbadger.com/images/krosh961/apache-alpine3.7 "Get your own image badge on microbadger.com") based on Alpine OS and Apache version 2.

There images are build on [krosh961/alpine3.7-docker](https://hub.docker.com/r/krosh961/alpine3.7-docker/) [![](https://images.microbadger.com/badges/image/krosh961/apache-alpine3.7.svg)](https://microbadger.com/images/krosh961/apache-alpine3.7 "Get your own image badge on microbadger.com") which are a modified version of Alpine OS with a working init process, cron, logrotate  and syslog. All services are started by runit daemon, for more information about how it works and setup of new services please visit <https://hub.docker.com/r/krosh961/alpine3.7-docker/> for more information.

The container also have a backup system with cron schedule, number of copies to save etc, for information about the backup system please visit the [README.md for the backupsystem](https://github.com/nimmis/backup/blob/master/README.md)


#### starting the container as a daemon

	docker run -d --name apache krosh961/apache-alpine3.7

This will start the container with apache process running, to access the container use

	docker exec -ti apache /bin/sh

#### Static web folder

The images exposes a volume at /web. The structure is

| Directory | Function |
| --------- | -------- |
| /web/html | web root |
| /web/cgi-bin | cgi bin folder |
| /web/config | apache config directory |
| /web/logs | apache log directory |
| /web/internal | internal pages, error pages etc

To use this start the container with

	docker run -d --name -apache -v /path/to/web:/web krosh961/apache-alpine3.7

if the folders are missing they will be created each time the container is started.

#### Accessing apache from outside the container

To access the webserver from external you can the **-P/-p** paramter, with **-P** the ports 80 and 443 is automaticly exposed and assign a random port.

or use the **-p** command to assign other ports, the syntax is

	-p <external port on host>:<local port in container>

so to access the apache server port 80 on port 8080 you should use the command

	docker run -d --name apache -p 8080:80 krosh961/apache-alpine3.7

or assigning 80->80 and 443->443 use

	docker run -d --name apache -p 80:80 -p 443:443 krosh961/apache-alpine3.7

#### Successsful setup

If everything worked and you where able to expose the correct port and type the correct adress in a webbrowser the following page should appear.

![screenshot](https://github.com/nimmis/docker-alpine-apache/blob/master/images/screenshot.png?raw=true "Screenshot")