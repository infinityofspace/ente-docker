# ente-docker

## About

This project offers prebuild Docker images from the ente server (so called museum) and web app, as there are no official prebuild Docker images
or Dockefile for the web app.

The web app Dockerfile is based on these [discussion](https://github.com/ente-io/ente/discussions/1183).

## Usage

You can pull the server image with:

```commandline
docker pull ghcr.io/infinityofspace/ente-server:latest
```

And the web server image with:

```commandline
docker pull ghcr.io/infinityofspace/ente-web:latest
```

Or build the images yourself:

```commandline
git clone https://github.com/ente-io/ente.git
cd ente/server
docker build -t ghcr.io/infinityofspace/ente-server .
```

```commandline
git clone https://github.com/ente-io/ente.git
git clone https://github.com/infinityofspace/ente-docker.git
cp -r ente-docker/web/* ente/web
cd ente/web
git submodule update --init --recursive
docker build -t ghcr.io/infinityofspace/ente-web .
```

## Copyright Notices

ente is not affiliated with this project. The docker images are licensed with the original license of the server and web app,
which can be found [here](https://github.com/ente-io/ente/blob/main/LICENSE).

The ente repository can be found [here](https://github.com/ente-io/ente).
