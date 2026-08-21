# Forgejo

![Tested on Podman](https://shields.io/badge/Tested-on_Podman/Windows11_(WSL2)-green)

This folder holds configuration for [Forgejo](https://forgejo.org). 


## Prerequisites

You'll need an OCI container engine which supports OCI compose specification (e.g. `docker-compose`, `podman-compose`, etc.). I use [Podman](https://podman.io) as my container engine and [podman-compose](https://github.com/containers/podman-compose) as my compose tool.

## Composing up

Run `podman compose up` or `task up` to compose the forgejo container up.

| Task command | Effect                                 |
| ------------ | -------------------------------------- |
| `up`         | Compose the container up               |
| `down`       | Compose the container down             |
| `clean`      | Shutdown the container and remove data |