# Storage

* [How the graph driver came to be](https://blog.mobyproject.org/where-are-containerds-graph-drivers-145fc9b7255)
* [Understanding Volumes in Docker](http://container-solutions.com/understanding-volumes-docker/)
* [Docker In-depth: Volumes](https://container42.com/2014/11/03/docker-indepth-volumes/)

As of Docker 1.9, Docker has named volumes which replace data-only containers.

Note that none of the environment variables will have any effect if you start the container with a data directory that already contains a database: any pre-existing database will always be left untouched on container startup.

## Union File System

Copy-on-Write non-persistent UFS writable layer. Slow performance. Live and die with the container and is ephemeral.

## Dockerfile VOLUME Instruction

If Dockerfile has the `VOLUME` instruction, it just means `/var/lib/docker` will keep those data there. It will be deleted if you:

1. `docker run --rm`
2. `docker rm -v`

**It will NOT be removed if you simply do `docker rm` without the -v flag**

To really persist volume, you have to either use data-only container (old way) or `docker volume create` or use `--mount`.

## Volume

Volumes are designated directories that bypass the layered **Union File System** to provide **persistent** or **shared data** for Docker. They will not be included when we commit or build an image.

If the container directory doesn't exist Docker will create it.

```
▶ docker volume ls
▶ docker volume create mysqldata
▶ docker volume inspect mysqldata
```

### Attach

```
// We attach the mysqldata storage as well using the jobline-net
docker container run --name mysqldb --network=jobline-net \
--mount source=mysqldata,target=/var/lib/mysql \
--mount type=bind,source=/Backup,target=/docker-entrypoint-initdb.d/ \
-e MYSQL_ROOT_PASSWORD=xxx \
-e MYSQL_DATABASE=yyy \
-d mysql:5.7
```

```
▶ docker run --rm --network=jobline-net -it mysql:5.7 /bin/bash
```

## Backup

```
// This backup container is a throw-away container: --rm
// We mount the current directory inside the container at /backup

▶ docker run --rm \
-v $(pwd):/backup \
--link postgres \

--net jobline-net \

postgres:9.4 sh -c 'exec pg_dump -h postgres -U postgres EVA_production | gzip > /backup/bak.sql.gz'
```

## UID and GID

* [chown -R 9999:9999](https://stackoverflow.com/questions/39397548/how-to-give-non-root-user-in-docker-container-access-to-a-volume-mounted-on-the?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)
* [Add ability to mount volume as user other than root](https://github.com/moby/moby/issues/2259)

```
▶ getent passwd deploy
```

The problem here is that all mounts are mounted as `root`.


## Log

```
// 2 volumes giving us access to Node and Redis log files

▶ docker run -d --name logstash \
--volumes-from redis \
--volumes-from nodeapp \
mech/logstash
```


