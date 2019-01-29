# jenkins-master
Containerisation of Jenkins master node

## Pre-requisites
The following applications must be installed and running:
* Docker

## Building docker image
There are two methods of building the image:
```
export VERSION='local'
docker build --rm -t "jenkins-master:${VERSION}" .
```
or
```
./build.sh
```