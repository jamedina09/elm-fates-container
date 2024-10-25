**Disclaimer: This is a personal project and is not supported by the Fates team.**

This repository contains the files needed to run Fates in a container. The container is based on the image `ghcr.io/jamedina09/personal-elm-fates-image:latest`, which I created using inspiration from [Repo 1](https://github.com/serbinsh/elm_containers) and [Repo 2](https://github.com/NGEET/fates-tutorial).

I personally use [Podman](https://podman-desktop.io/downloads) to manage containers, but you can use [Docker](https://www.docker.com/products/docker-desktop/) if you prefer. The instructions below are for Podman, hence the word "podman" at the beginning of each command. If you use Docker, simply replace "podman" with "docker."

You will need to install Podman Desktop (or Docker Desktop) on your machine. When installing Podman Desktop (or Docker Desktop) on your machine, follow all the instructions on their respective websites (linked above). You may need to install additional dependencies, but these will be indicated by the installer, so just follow the prompts and install them.

After installing Podman Desktop (or Docker Desktop), you can follow the instructions below to download the container and run it.

## Command line Interface (CLI)

To run Fates, you will need to use the command line interface (CLI). The CLI is a text-based interface that allows you to interact with the computer using commands. The CLI is also known as the terminal on Maca or command prompt on Windows.

There are some key commands that you will need to know. These commands are:

- `ls`: This command lists the files and directories in the current directory.
- `ls -a`: This command lists all the files and directories in the current directory, including hidden files.
- `cd`: This command changes the current directory.
- `mkdir`: This command creates a new directory.
- `rm`: This command removes a file or directory.
- `cp`: This command copies a file or directory.
- `mv`: This command moves a file or directory.
- `touch`: This command creates a new file.
- `cat`: This command displays the contents of a file.
- `nano`: This command opens a text editor.

Make yourself familiar with these commands, as you'll use them to interact with Fates, the container, and its a good skill to have in general.

## Directory organization

This is my suggestion, but you can organize your directories as you see fit.

In your home directory, create a directory named `projects`. This directory will contain all the projects you want to run in the container, as well as the input data, scripts, outputs; basically everything.

```bash
mkdir -p ~/projects
````
The `-p` flag is used to create the directory and any parent directories that do not exist.
The `~/` is a shortcut for your home directory. It is equivalent to `/Users/your-username/` on Mac or `C:\Users\your-username\` on Windows.

Enter the `projects` directory.

```bash
cd ~/projects
````

Once inside the directory, you will need to clone the following [repo](https://github.com/jamedina09/elm-fates-container). This repository contains the files needed to run Fates in a container, and a sample script to run the first test.

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
    ├── .env
    └── sample_script
        └── e3sm_sample.sh
````

The file `docker-compose.yml` is the file that gives the directions to Podman. The file `.env` is a file that contains the path to the projects directory. The directory `scripts` contains the script `e3sm_sample.sh`, which is a sample script to run the first test.

The file '.env' is a hidden file, so you need to use the command `ls -a` in your terminal to see it.

We need to edit the `.env` file. Open it with your preferred text editor (VS Code, Emacs, Vim, or any simple text editor available on your computer), and replace the path `/Users/MedinaJA/projects`—which is the path on my machine—with the path to your own `projects` directory.

This is how you open it from your terminal using the default text editor:

```bash
open ~/projects/elm-fates-container/.env
````

## Downloading the container image

The following command will download the container image from the GitHub Container Registry (ghcr.io). This command only needs to be run once, and you can execute it from any directory. However, I recommend running it from the projects directory, just to ensure you are always in the same location.

```bash
podman pull ghcr.io/jamedina09/personal-elm-fates-image:latest
````

We have now downloaded the container image. Now is time to run the container.

## Running the container

Open your Podman (or Docker) desktop. Podman desktop needs to be running in the background for the following commands to work.

Access the directory where the `docker-compose.yml` file is located.

```bash
cd ~/projects/elm-fates-container
````

Now, run the following command to start the container:

```bash
podman compose up -d
````
You are now running the container. You can access the container by running the following command:

```bash
podman exec -it personal-elm-fates /bin/bash
````

You are now inside the container. You can run the sample script by running the following command:



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

