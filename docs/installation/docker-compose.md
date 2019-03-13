# Install with Docker Compose

Official documentation [here](https://github.com/wekan/wekan/wiki/Install-Wekan-Docker-for-testing)

!!! warning
    This installation is suitable only for developpement, not for production. See [here](https://github.com/wekan/wekan/wiki/Docker#development)

## 1. Prerequisites

* [Docker](https://docs.docker.com/install/) must be installed.
* [Docker Compose](https://docs.docker.com/compose/install/) must be installed.

## 2. Download the docker-compose.yml

```shell
wget https://raw.githubusercontent.com/wekan/wekan/devel/docker-compose.yml
```

## 3. Configuration

For a quick start, **comment** or modify these lines in `docker-compose.yml`:

```yml
- MAIL_URL=smtp://user:pass@mailserver.example.com:25/
- MAIL_FROM='Example Wekan Support <support@example.com>'
```

## 4. Start containers

```shell
docker-compose up
```

## 5. Web access

So now, you can access to wekan at http://localhost/
