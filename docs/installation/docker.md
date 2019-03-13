# Install with Docker

Official documentation [here](https://github.com/wekan/wekan/wiki/Docker#development)


!!! warning
    This installation is suitable only for developpement, not for production. See [here](https://github.com/wekan/wekan/wiki/Docker#development)

## 1. Prerequisites

* [Docker](https://docs.docker.com/install/) must be installed.

## 2. Start MongoDB container

```shell
docker run -d --restart=always --name wekan-db mongo:3.2.21
```

## 3. Start Wekan container

```shell
docker run -d --restart=always --name wekan --link "wekan-db:db" -e "MONGO_URL=mongodb://db" -e "ROOT_URL=http://localhost:8080" -p 8080:8080 quay.io/wekan/wekan
```

## 4. Web access

So now, you can access to wekan at http://localhost:8080/
