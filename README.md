# jenkins-master
Containerisation of Jenkins master node

## Pre-requisites
The following applications must be installed and running:
* Docker

## Build docker image
There are two methods of building the image:
```
export VERSION='local'
docker build --rm -t "jenkins-master:${VERSION}" .
```
or
```
./build.sh
```

## Running locally
In order to run the Docker image (generated above) locally, a few items will need to be defined and mounted as demonstrated.

```
docker run --rm -p 8080:8080 -p 50000:50000 \
                -v "${PWD}/job_repos.txt":/usr/share/jenkins/data/job_repos.txt \
                -v "${PWD}/ssh_config/config":/var/jenkins_home/.ssh/config \
                -v "${HOME}/.ssh/id_rsa":/var/jenkins_home/.ssh/id_rsa \
                -v "${HOME}/.ssh/id_rsa.pub":/var/jenkins_home/.ssh/id_rsa.pub \
                jenkins-master:{VERSION}
```
`{VERSION}` - globally defined in build step

A key item to be wary of is the mounting of the private and public ssh keys utilised when connecting to the repositories (github in this instance). In this example, we are mounting the keys located within our local `.ssh` directory.