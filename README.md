# Content of repository

This repository contains a docker version of ELK running on one host...

## Installation of ELK

clone the repository onto a centos 7 machine prepared with the ```ansible_docker```. See README in directory.

### Storage
Make sure the ```storage``` directory is owned as described in directory README.

## Start ELK

Run the command:

    docker-compose up -d

In a few minutes this should be running...


## The filebeat and metricbeat

The 2 directories contains the settings needed for filebeat and metricbeat. Follow the installation guides found there.


## NOTE

Prerequistes is that the server running ELK is ```elasticsearchhost``` 
