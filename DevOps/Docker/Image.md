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

## ENV

* [Docker ARG, ENV and .env - a Complete Guide](https://vsupalov.com/docker-arg-env-variable-guide/)

## CMD and ENTRYPOINT

* [Docker RUN vs CMD vs ENTRYPOINT](http://goinbigdata.com/docker-run-vs-cmd-vs-entrypoint/)

Use array to run the command "as-is" without prepend `/bin/sh -c` to the command.

```dockerfile
# If you don't use array, it will prepend /bin/sh -c to it
CMD ["/bin/bash", "-l"]

# Can be parameters only. In which case you need ENTRYPOINT
CMD ["-f", "--verbose"]
```

Can be overridden by `docker run` command.

* Can only ever have one `CMD`, since container execute only one main process (PID=1)
* Use Supervisor if you want to run multiple processes or commands

## Shell vs Exec

```
# Shell form
# /bin/sh -c <COMMAND>
RUN apt-get install node
CMD echo "Hello"

# Exec form
# Call the executable directly and shell processing does not happen
# Preferred??
RUN ["apt-get", "install", "node"]
ENTRYPOINT["/bin/bash", "-c", "echo Hello, $name"]
```

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

