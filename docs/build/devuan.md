# Build Debian OFT package with Docker

!!! warning
    OFT Packages = Only For Testing Packages : This packages are not suitable for production.

!!! info
    You can then build yourself the debian package for the following operating systems:

    * [Debian Wheezy 7 64 bit](https://www.debian.org/)
    * [Devuan Jessie 1 64 bit](https://devuan.org/)
    * [Devuan Ascii 2 64 bit](https://devuan.org/)

!!! Notes
    AppImage:

    * First we make an AppImage package, it reduces the size occupied on the disk once installed and considerably increases the installation speed of the debian package.
    * This also allows the nodejs runtime to be embedded in a confined way.

    So, in the Docker command:
    
    * `--device /dev/fuse` in order to use AppImage inside docker
    * `--privileged` in order to allow fuse inside docker

## 1. Prerequisites

* [Docker](https://docs.docker.com/install/) must be installed.

## 2. Build with Docker

* Clone this repository: `git clone https://github.com/soohwa/wekan-deb.git && cd wekan-deb`
* Build the debian package: `make deb`
* Clean the build repository: `make clean`
* The wekan debian package is created inside the `build` folder.

## 3. Release number configuration

* Nodejs: `NODE_RELEASE` in `Dockerfile-BuildPackage` (do `make image` after the change)
* AppImage: `APPIMAGE_RELEASE` in `Dockerfile-BuildPackage` (do `make image` after the change)
