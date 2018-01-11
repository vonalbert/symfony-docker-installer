# Symfony Docker Installer
This software is designed to bootstrap a development environment based on Symfony Flex and Docker without having the php executable installed on your host machine.

The only requirement to build the project are docker-ce and a bash shell.

The installer was developed and tested on ubuntu 17.10.

## Installation
To run the project just download the zip file from github. If you want you can even `git-clone` this repository, but you have to remove the *.git* folder inside it. This is needeb because the `install` script verifies if the git's folder is there to guess where to create the application:
- if git is found it will create the project in a git-ignored directory. This setup is used for testing the installer.
- if git is not there, then the script will create the application in the current directory, then removes itself when done.

When you placed the script in the right directory, cd into it and run `bash install`.

When the process is complete the installer is removed and you should have your project built and running.


## Daily usage
When you have built your project you can use `make` to control the environment. The make targets are:

*build*: useful if you need to reset your environment for any reason or when you make changes to the files in the `docker/` directory or to any file related to the docker environment setup.

*start*: it just run the docker environment.

*stop*: stops and removes the containers.

*shell*: starts a shell inside the application container.


For a daily usage when you start to work to the project just fire `make start`, perform tasks inside the application container with `make shell` and finally, when you're done working with the project, fire `make stop` to stop docker.

By default, when you start the environment, the application is available at `localhost` port 80.


## Enable assets compilation

1. Run `npm install --save jquery sass-loader node-sass` in the docker-machine shell
2. Add the following entries in webpack.config.js
```
.addEntry('scripts', './assets/js/app.js')
.addStyleEntry('style', './assets/css/app.scss')
.createSharedEntry ('vendor', [
    'jquery',
])
```
3. Uncomment the npm-related lines in `docker/app/appinit` to enable automatic assets compilation when docker-machine is built


## Credits
This project is highly based on the [dunglas' work](https://github.com/dunglas/symfony-docker).
