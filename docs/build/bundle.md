# Build Wekan bundle with Docker

## 1. Prerequisites

* [Docker](https://docs.docker.com/install/) must be installed.

## 2. Build with Docker

* Clone this repository: `git clone https://github.com/soohwa/wekan-deb.git && cd wekan-deb`
* Build the wekan bundle: `make bundle`
* After the build, you can find inside the `dist` folder:
    * Wekan bundle: `dist/wekan.tar.gz`
    * Wekan REST API HTML documentation: `dist/wekan.html`
    * Wekan Release Number: `dist/WEKAN_RELEASE`
