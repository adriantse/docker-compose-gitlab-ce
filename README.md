# docker-compose-gitlab-ce

- [Introduction](#introduction)
    - [Changelog](Changelog.md)
- [Contributing](#contributing)
- [Team](#team)
- [Issues](#issues)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Configuration](#configuration)
- [Maintenance](#maintenance)
    - [Creating Backups](#creating-backups)
    - [Restoring Backups](#restoring-backups)
    - [Automated Backups](#automated-backups)
    - [Amazon Web Services (AWS) Remote Backups](#amazon-web-services-aws-remote-backups)
    - [Google Cloud Storage (GCS) Remote Backups](#google-cloud-storage-gcs-remote-backup)
    - [Rake Tasks](#rake-tasks)
    - [Import Repositories](#import-repositories)
    - [Upgrading](#upgrading)
    - [Shell Access](#shell-access)
- [Features](#features)
- [References](#references)

# Introduction

GitLab CE is set up in the Docker image using the [install from source](https://gitlab.com/gitlab-org/gitlab-ce/blob/master/doc/install/installation.md) method as documented in the the official GitLab documentation.

For other methods to install GitLab please refer to the [Official GitLab Installation Guide](https://about.gitlab.com/installation/) which includes a [GitLab image for Docker](https://gitlab.com/gitlab-org/gitlab-ce/tree/master/docker).

# Contributing


# Team


# Issues



# Prerequisites

# Installation


# Quick Start

Using [docker-compose](https://docs.docker.com/compose/).

Start GitLab using:

```bash
docker-compose up -d
```

# Configuration


# Maintenance

## Creating backups


```bash
docker-compose run --rm gitlab app:rake gitlab:backup:create
```

## Restoring Backups


Before performing a restore make sure the container is stopped and removed to avoid container name conflicts.

```bash
docker stop gitlab && docker rm gitlab
```

If this is a fresh database that you're doing the restore on, first
you need to prepare the database:

```bash
docker run --name gitlab -it --rm [OPTIONS] \
    gitlab app:rake db:setup
```

Execute the rake task to restore a backup. Make sure you run the container in interactive mode `-it`.

```bash
docker run --name gitlab -it --rm [OPTIONS] \
    gitlab:10.8.3-1 app:rake gitlab:backup:restore
```

## Import Repositories

Copy all the **bare** git repositories to the `repositories/` directory of the [data store](#data-store) and execute the `gitlab:import:repos` rake task like so:

```bash
docker run --name gitlab -it --rm [OPTIONS] \
    gitlab app:rake gitlab:import:repos
```

## Shell Access

```bash
docker exec -it gitlab bash
```

# References

* https://github.com/gitlabhq/gitlabhq
* https://github.com/gitlabhq/gitlabhq/blob/master/doc/install/installation.md
