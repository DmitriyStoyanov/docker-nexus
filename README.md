# docker-nexus

A container image for Sonatype Nexus Repository Manager OSS, based on Alpine Linux.

[![Docker Pulls](https://img.shields.io/docker/pulls/scorpio2002/docker-nexus)](https://hub.docker.com/r/scorpio2002/docker-nexus/tags?page=1&ordering=last_updated)

# History

This repo created as fork of the repo https://github.com/travelaudience/docker-nexus/ with updating version and preparing PRs into main repo.
But PRs review and merges into main repo too long, because of that, I've changed info in my repo, created automatical push into my dockerhub repo. So you can use latest images from dockerhub for the moment.

## Current software

* Alpine Linux 3.18
* OpenJDK JRE 8u212
* Nexus Repository Manager OSS 3.68.1 ([release notes](https://help.sonatype.com/en/sonatype-nexus-repository-3-68-0-release-notes.html))

## Running

Running it locally (for the latest tag, check [scorpio2002/docker-nexus](https://hub.docker.com/r/scorpio2002/docker-nexus/tags):

```shell
docker run -p 8081:8081 --name nexus scorpio2002/docker-nexus:3.68.1
```

## Reasoning

The Official Sonatype Nexus Docker image: https://hub.docker.com/r/sonatype/nexus3/ is suitable for most use cases. But as discussed in this blog post:
https://www.sonatype.com/travel-audience-devops-pipeline-solution
being able to `restore` from a backup requires stopping the nexus service. And this is not possible with the official image, as described in this bug report: https://issues.sonatype.org/browse/NEXUS-23442

So while `travel audience` would prefer to support the official image, this is not possible at this time, and we hope that this lightweight image provides a suitable alternative to the community in the meantime.

The travel audience Nexus Docker image provides the following features that are not present in the official image:

* uses `runit` to run nexus under a secondary process
* uses an Alpine base image, instead of RedHat's UBI8
* provides an optional flag to make sure all mounted data is owned by the `nexus` user _(nexus will have issues if that's not the case)_
