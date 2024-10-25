**Disclaimer:** *This is a personal project and is not supported by the Fates team.*

This repository contains the files needed to run Fates in a container. The container is based on the image `ghcr.io/jamedina09/personal-elm-fates-image:latest`, which I created using inspiration from [Repo 1](https://github.com/serbinsh/elm_containers) and [Repo 2](https://github.com/NGEET/fates-tutorial).

I personally use [Podman](https://podman-desktop.io/downloads) to manage containers, but you can use [Docker](https://www.docker.com/products/docker-desktop/) if you prefer. The instructions below are for Podman, hence the word "podman" at the beginning of each command. If you use Docker, simply replace "podman" with "docker."

You will need to install Podman Desktop (or Docker Desktop) on your machine. When installing Podman Desktop (or Docker Desktop) on your machine, follow all the instructions on their respective websites (linked above). You may need to install additional dependencies, but these will be indicated by the installer, so just follow the prompts and install them.

After installing Podman Desktop (or Docker Desktop), you can follow the instructions below to download the container and run it.

## Directory organization

This is my suggestion, but you can organize your directories as you see fit.

In your home directory, create a directory named `projects`. This directory will contain all the projects you want to run in the container.

```bash
mkdir -p ~/projects
````

Enter the `projects` directory.

```bash
cd ~/projects
````

Once inside the directory, you will need to clone the following [repo](https://github.com/jamedina09/elm-fates-container). This repository contains the files needed to run Fates in a container, and a sample script to run the first test more details below).

To clone the repository, run the following command:

```bash
git clone git@github.com:jamedina09/elm-fates-container.git
````

After cloning the repository, you will have the following directory structure:

```bash
projects
└── elm-fates-container
    ├── docker-compose.yml
    ├── run.md
    └── scripts
        └── e3sm_sample.sh
````



## Downloading the container

The following command will download the container image from the GitHub Container Registry (ghcr.io). This command only needs to be run once.

```bash
podman pull ghcr.io/jamedina09/personal-elm-fates-image:latest
````

## To open and run—just—the Container

Remember that is bad practice to attribute a name, you can let podman create a random name so you don't run into conflicts later on.

```bash
podman run --name personal-elm-fates -it personal-elm-fates-image /bin/bash
````

## To open the container interacting with projects directory

```bash
podman compose up -d     
````

## Enter the container

```bash
podman exec -it personal-elm-fates /bin/bash
````

## To leave the container

```bash
exit
````

## To stop the container

```bash
podman compose down
````

## Prepare first run

There is a file named '.env'. Here, you need to place the directory projects in the variable 'PROJECTS_DIR'. This is the directory where the projects will be stored.

```bash
PROJECTS_DIR=/path/to/your/projects
````

## Create a directory named scripts within the projects directory

```bash
mkdir -p $PROJECTS_DIR/scripts
````

## Move the e3sm sample script to the scripts directory and then run it

```bash

