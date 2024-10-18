## Download the container

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

