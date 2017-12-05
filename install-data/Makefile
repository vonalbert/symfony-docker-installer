# Create a container on-the-fly and run a command and remove it
RUN=docker-compose run --rm app

build:
	docker-compose up -d --build --remove-orphans
	@-$(RUN) composer install --no-progress --no-suggest --no-interaction
	@-$(RUN) npm install
	@-$(RUN) npm run dev
	@-$(RUN) chmod 777 -Rf node_modules vendor .env
	@-$(RUN) bin/console doctrine:schema:update --force
	@-$(RUN) rm -rf var
	@-$(RUN) bin/console cache:warmup
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
