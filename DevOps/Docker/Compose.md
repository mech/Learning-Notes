# Docker Compose

## Installation

* [Documentation on installing docker-compose](https://docs.docker.com/compose/install/#install-compose)

## YAML

```
version: '3'

services:
  web:
    build: .
    ports:
      - '5000:5000'
    volumes:
      - .:/code
    depends_on:
      - redis

  redis:
    image: redis
```


