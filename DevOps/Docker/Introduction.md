# Docker Introduction

* Networking - Acquire SocketPlane
* Storage - Acquire Infinit
* Swarm

## Docker for Mac

* Moby (xhyve virtual machine)

## Timezone

```
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