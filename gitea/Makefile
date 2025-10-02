.PHONY: help server runner rm

help:
	@echo "Run specific commands instead of make."
	@echo "Commands:"
	@echo "    server - start Gitea server"
	@echo "    runner - start Gitea Actions runner"
	@echo "    rm     - shutdown and remove all Gitea containers and related resources"
	@echo ""

server:
	@podman compose up -d gitea-server

runner:
ifndef REGISTRATION_TOKEN
	@$(error REGISTRATION_TOKEN undefined!)
else
	@podman compose up -d gitea-runner
endif

rm:
	-@podman pod stop pod_gitea  &> /dev/null || true
	-@podman pod rm pod_gitea    &> /dev/null || true
	-@yes | podman network prune &> /dev/null || true
	-@yes | podman volume prune  &> /dev/null || true
	@echo "Gitea and Gitea Actions removed."
	@echo "Containers:"
	@podman ps -a | sed "s/^/    /"
	@echo "Volumes:"
	@podman volume ls | sed "s/^/    /"
	@echo "Networks:"
	@podman network ls | sed "s/^/    /"
