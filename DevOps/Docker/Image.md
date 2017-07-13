# Docker Image

```dockerfile
FROM XXX

# To prevent: dpkg-preconfigure: unable to re-open stdin
ENV DEBIAN_FRONTEND noninteractive

# Or use this?
# https://github.com/moby/moby/issues/27988
RUN apt-get install -y dialog apt-utils

RUN apt-get update && \
    apt-get install -y libjpeg-progs && \
    apt-get install -y ghostscript && \
    apt-get install -y imagemagick
```