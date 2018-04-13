# Docker Image

```dockerfile
FROM XXX

LABEL maintainer="xxx@example.com"

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

## Multi-Stage Builds

Multiple `FROM` instruction

```dockerfile
FROM node:latest AS storefront
COPY react-app .
RUN npm install
RUN npm run build

FROM maven:latest AS appserver
COPY pom.xml .
RUN mvn -B -f pom.xml -s ...

FROM java:8 AS production
WORKDIR /static
COPY --from=storefront /usr/src/app/react-app/build .
WORKDIR /app
COPY --from=appserver /usr/src/target/snapshot.jar .
```

## Example

/var/lib/docker

```
▶ docker image pull redis
▶ docker image ls --digests
```

