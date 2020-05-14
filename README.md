# GOLANGDockerize

## A Brief Introduction

Here is the Dockerize GOLANG setup for development including initial go modules and packages setup, ready to go environment in a Docker container.


## Pre-requisites

One must have Docker installed in his local system for deploying this GOLANG setup easily.


## Running the docker-compose setup

```
docker-compose up -d
```

It will deploy the container named as learningpack, no need of any manual or human intervention. 


## Accessing the container

Using SSH
```
ssh -p 2228 hello@localhost
```

And the password is also
```
hello
```

## Inside the container

The source folder present in the repository, which contains the working code is being pushed inside the container at the following address;

```
/opt/go/src/learningpack
```