# Docker Introduction

* [Play with Docker](https://training.play-with-docker.com/)

---

* Networking - Acquire SocketPlane
* Storage - Acquire Infinit
* Swarm
* LXC to runc

## Installation

### For Ubuntu

```
// Edit /etc/systemd/system/docker.service.d/mydocker.conf

# Override by mech
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd --dns 8.8.8.8 --dns 8.8.4.4 --log-driver=syslog -H fd://
```

## Docker for Mac

* Moby (xhyve virtual machine)

## For Development?

* [Docker As Rails Development Environment](https://medium.com/@sivakumarvadivelu/docker-as-rails-development-environment-9bdb361e992)

## Timezone

* [Docker Container time & timezone (will not reflect changes)](https://serverfault.com/questions/683605/docker-container-time-timezone-will-not-reflect-changes)

```
// Seems to work for jobline-upgrade
▶ docker run -d -e TZ=Asia/Singapore ...

▶ docker run --rm -v /etc/localtime:/etc/localtime:ro busybox date
```

Your container should be timezone independent. For many applications, system timezone is fairly irrelevant and testing outside of one's own timezone can even help catch timezone-related assumptions and bugs.

## Time Sync or Drift

After running Docker container for a long time like 300 days, the time will become out of sync.

```
Aws::S3::Errors::RequestTimeTooSkewed (The difference between the request time and the current time is too large.):
```

```
▶ timedatectl status
```

## cgroups Memory Limit

## Logging

* [Top 10 Docker Logging Gotchas](https://sematext.com/blog/top-10-docker-logging-gotchas/)

## Problems

* [Docker in Production: A History of Failure](https://thehftguy.com/2016/11/01/docker-in-production-an-history-of-failure/)
* [Another reason why your Docker containers may be slow](https://hackernoon.com/another-reason-why-your-docker-containers-may-be-slow-d37207dec27f)

## Videos

* [Good basic introduction to container](https://www.youtube.com/watch?v=EnJ7qX9fkcU)


