# Gitea and Gitea Actions

![Tested on Podman](https://shields.io/badge/Tested-on_Podman/Windows11_(WSL2)-green)

This folder holds configuration for Gitea and Gitea Actions.

- [Gitea and Gitea Actions](#gitea-and-gitea-actions)
  - [Prerequisites](#prerequisites)
  - [Composing up](#composing-up)
    - [with Podman](#with-podman)
    - [with other OCI engine (like Docker)](#with-other-oci-engine-like-docker)


[Gitea](https://gitea.com) is an open source self-hosted Git service written in Go, while [Gitea Actions](https://docs.gitea.com/usage/actions/overview) are the built-in CI/CD platform for Gitea.

If you're familiar with [GitHub](https://github.com) and [GitHub Actions](https://github.com/features/actions), you can think of Gitea and Gitea actions are open source alternatives to them:

|             | Open source   | Closed source  |
| ----------- | ------------- | -------------- |
| Git service | Gitea         | GitHub         |
| CI/CD       | Gitea Actions | GitHub Actions |

> <small>Gitea Actions is compatible to GitHub Actions.</small>

## Prerequisites

You'll need an OCI container engine which supports OCI compose specification (e.g. `docker-compose`, `podman-compose`, etc.). I use [Podman](https://podman.io) as my container engine and [podman-compose](https://github.com/containers/podman-compose) as my compose tool.

> **For Windows users**
>
> If you're using Windows, it's highly recommended to enter the WSL2 environment before you run `docker` or `podman` commands.
> 
> For example, you should `podman machine ssh` into the WSL2, and then run `podman compose` commands. This is because some Linux paths need to be mounted into containers, and if you're running `docker` or `podman` on Windows, things will go wrong.
>
> Specifically, in this project, the `/var/run/docker.sock` must be mounted into the `gitea-runner` container, which utilizes OCI container engine to run CI/CD jobs.

## Composing up
### with Podman
This project comes with a handwritten `Makefile` for Podman users. You can setup Gitea and Gitea Actions step by step:

1. **Start Gitea server**
   
   Run `make server`, and the `gitea-server` container shall run. You can visit `http://localhost:3000` to perform first-time installation.

   After that, go to *Site Administration* > *Actions* > *Runners* > *Create new Runner* and you should see a registration token. Copy the token for the next step.

2. **Start Gitea Actions runner**
   
   Run `make runner REGISTRATION_TOKEN="<Your registration token>"` with the registration token you copied. This should pull up the Gitea Actions runner automatically.

Done! If something goes wrong, you can check the logs and clean up all the containers and resources with `make rm` and start again.

### with other OCI engine (like Docker)
It's okay if you're using other OCI containers and it *should* (but not guaranteed to) work. Let's take Docker for example:

1. **Start Gitea server**
   
   Run `docker compose up -d gitea-server`, then go to `https://localhost:3000` for graphical first-time installation. You'll need to copy the registration token at *Site Administration* > *Actions* > *Runners* > *Create new Runner*.

2. **Start Gitea Actions runner**
   
   Set the environment variable `REGISTRATION_TOKEN` to the token you copied in step 1, and run `docker compose up -d gitea-runner`.