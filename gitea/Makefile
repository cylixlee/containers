export REGISTRATION_KEY

help:
	@echo "Please use one of the following commands: [rm, server, runner]"

rm:
	@podman pod stop pod_gitea
	@podman pod rm pod_gitea
	@yes | podman network prune
	@yes | podman volume prune

server:
	@podman compose up -d gitea-server

runner:
	@podman compose up -d gitea-runner

.PHONY: help rm server runner