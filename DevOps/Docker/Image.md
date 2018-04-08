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

## CMD and ENTRYPOINT

Use array to run the command "as-is" without prepend `/bin/sh -c` to the command.

```dockerfile
# If you don't use array, it will prepend /bin/sh -c to it
CMD ["/bin/bash", "-l"]
```

Can be overridden by `docker run` command.

* Can only ever have one `CMD`
* Use Supervisor if you want to run multiple processes or commands


