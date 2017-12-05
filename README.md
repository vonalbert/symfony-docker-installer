# Symfony Docker Installer
This software is designed to bootstrap a development environment based on Symfony Flex and Docker without having the php executable installed on your host machine.

The only requirement to build the project are docker-ce and a bash shell.

The installer was developed and tested on ubuntu 17.10.

## Installation
To run the project just download the zip file from github or clone the repository. At that point cd into the project dir and fire `sudo bash install`.

When the process is complete the installer is removed and you should have your project built and running.

## Daily usage
When you have built your project you can use `make` to control the environment. The make targets are:

*build*: useful if you need to reset your environment for any reason or when you make changes to the files in the `docker/` directory or to any file related to the docker environment setup.

*start*: it just run the docker environment.

*stop*: stops and removes the containers.

*shell*: starts a shell inside the application container.


For a daily usage when you start to work to the project just fire `make start`, perform tasks inside the application container with `make shell` and finally, when you're done working with the project, fire `make stop` to stop docker.

By default, when you start the environment, the application is available at `localhost` port 80.
