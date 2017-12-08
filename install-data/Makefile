# Create a container on-the-fly and run a command and remove it
RUN=docker-compose run --rm app

build: stop
	docker-compose build --force-rm
	docker-compose up -d
.PHONY: build


start:
	docker-compose up -d
.PHONY: start


stop:
	docker-compose stop
	docker-compose rm -fv
.PHONY: stop


shell:
	@-docker-compose exec app sh
	@echo "\n"
.PHONY: shell
