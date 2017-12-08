# Build the container and force an initialization of the project.
# The init command is ran here because the RUN directives of the makefile are cached, so
# it would be executed the first time only.
build: stop
	docker-compose build --force-rm
	docker-compose run --rm app appinit
	@-echo "Project correctly built."
	@-echo "To start/stop the project use 'make start' and 'make stop'."
	@-echo "To get shell access use 'make shell'."
.PHONY: build


# Start the containers - this won't build the image. To build it use the `build` target
start:
	@-docker-compose up -d --no-build --no-recreate || echo "To build the container use 'make build'"
.PHONY: start


# Stop the running containers. If there's nothing to stop, this target does nothing
stop:
	docker-compose stop
	docker-compose rm -fv
.PHONY: stop


# Gain access in the application container shell
shell:
	@-docker-compose exec app sh
	@echo "\n"
.PHONY: shell
