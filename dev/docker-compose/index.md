# 1. Simple

```yml
version: '3.0'
services:

  my-image:
    image: my-image
    container_name: my-image
    build:
      context: ./
      dockerfile: Dockerfile.local
    volumes:
      - './apps:/home/app/apps' # mount volumes exterbal:internal
    ports:
      - 3001:3001               # port forward external:internal
    networks:
      - mydockernet             # access service via "mydockernet"
    env_file:
     - .my-env                   # choose env-file
    command: /bin/bash          # overwrite, do nut run ENTRYPOINT
    stdin_open: true
    tty: true

networks:
  mydockernet:
    driver: bridge
```

```shell
docker-compose --env-file .my-env -f docker-compose.yml up -d 
# --env-file  : file env
# -f          : file docker-compose
# up          : start docker
# -d          : not follow logs
```

```shell
# .env file
host.docker.internal #call outer http
```
