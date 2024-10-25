### Disclaimer: This is a personal project and is not supported by the Fates team.

This repository contains the files needed to run FATES in a container. The container is based on the image `ghcr.io/jamedina09/personal-elm-fates-image:latest`, which I created using inspiration from [Repo 1](https://github.com/serbinsh/elm_containers) and [Repo 2](https://github.com/NGEET/fates-tutorial).

I personally use [Podman](https://podman-desktop.io/downloads) to manage containers, but you can use [Docker](https://www.docker.com/products/docker-desktop/) if you prefer. The instructions below are for Podman, hence the word "podman" at the beginning of each command. If you use Docker, simply replace "podman" with "docker." I suggest you use Podman, as it is suggested to be more secure and does not require root access.

You will need to install Podman Desktop (or Docker Desktop) on your machine. When installing Podman Desktop (or Docker Desktop) on your machine, follow all the instructions on their respective websites (linked above). You may need to install additional dependencies, but these will be indicated by the installer, so just follow the prompts and install them.

## Command line Interface (CLI)

To run FATES, you will need to use the command line interface (CLI). The CLI is a text-based interface that allows you to interact with the computer using commands. The CLI is also known as the terminal on Macs or command prompt on Windows.

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

Make yourself familiar with these commands, as you'll use them to interact with FATES, the container, and its a good skill to have in general.

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

Once inside the directory, you will need to clone the following [repo](https://github.com/jamedina09/elm-fates-container). Surprise! It is the repository where you are reading these instructions. This repository contains the files needed to run FATES in a container, and a sample script to run the first test.

To clone the repository, run the following command (if you dont use github, see below):

```bash
git clone git@github.com:jamedina09/elm-fates-container.git
````

NOTE: If you dont use github, you can download the repository as a zip file by clicking on the green button that says "Code" and then "Download ZIP". Once downloaded, extract the zip file and move the folder to the `projects` directory.

After cloning (or downloading) the repository, you will have the following directory structure:

```bash
projects
└── elm-fates-container
    ├── docker-compose.yml
    ├── run.md
    ├── .env
    └── sample_script
        └── e3sm_fates_test.sh
````

The file `docker-compose.yml` is the file that gives the directions to Podman (or Docker). The file `.env` is a file that contains the path to the projects directory. The directory `sample_script` contains the script `e3sm_fates_test.sh`, which is a sample script to run the first test.

The file '.env' is a hidden file, so you need to use the command `ls -a` in your terminal to see it.

We need to edit the `.env` file. Open it with your preferred text editor (VS Code, Emacs, Vim, or any simple text editor available on your computer), and replace the path `/Users/XXX/projects`—which is the path on my machine—with the path to your own `projects` directory.

This is how you open the .env file from your terminal using the default text editor:

```bash
open ~/projects/elm-fates-container/.env
````

Now, let’s create a scripts directory inside the projects directory and move or copy the sample script to the scripts directory.

You can use your mouse, of course, but if you’re feeling adventurous (which I recommend), always use the command line.

```bash
mkdir -p ~/projects/scripts
cp ~/projects/elm-fates-container/sample_script/e3sm_fates_test.sh ~/projects/scripts
````

Now, you'll have the following directory structure:

```bash
projects
├── elm-fates-container
│   ├── docker-compose.yml
│   ├── run.md
│   ├── .env
│   └── sample_script
│       └── e3sm_fates_test.sh
└── scripts
    └── e3sm_fates_test.sh
````


## Downloading the container image

The following command will download the container image from the GitHub Container Registry (ghcr.io). This command only needs to be run once, and you can execute it from any directory. However, I recommend running it from the projects directory, just to ensure you are always in the same location.

```bash
podman pull ghcr.io/jamedina09/personal-elm-fates-image:latest
````

We have now downloaded the container image. Now is time to run the container.

## Running the container

Open your Podman (or Docker) desktop. Podman (or Docker) desktop needs to be running in the background for the container to work. This is the easy way to do it, but you can also run it from the terminal, but I'll skip that step for now. So, open Podman (or Docker) desktop.

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

You are now inside the container.

Type `ls` to see the contents of the container. You should see the `projects` directory; however, it is now called `projects_mirror`, which is the name I chose to clarify its purpose. This directory is a mirror of the projects directory on your machine. You can access the `projects_mirror` directory by running the following command:

```bash
cd projects_mirror
````

Once there, type `ls`, and you’ll see all the files and directories in your `projects` directory on your machine.

## Running the sample script

The sample script is named `e3sm_fates_test.sh`. The extension `.sh` indicates that this is a shell script, which is used to automate tasks in the terminal. The script e3sm_fates_test.sh serves as a sample to run the first test, meaning that all the instructions needed to run the model are defined here. Open it and check what’s inside. You can modify this script to run your own simulations.

Go to the `scripts` directory:

```bash
cd scripts
````

You can run the sample script by running the following command:

```bash
./e3sm_fates_test.sh
````

If you get an error (ignore if no error), you may need to give the script permission to execute. You can do this by running the following command:

```bash
chmod +x e3sm_fates_test.sh
````

Now, run the script again:

```bash
./e3sm_fates_test.sh
````

The script will initiate the first test, which involves a FATES run over a single-point test site in Brazil. After executing the .sh file, you'll notice that the container creates several folders. One of these folders is `inputdata`, which contains the necessary input data for the test. The other folder is `scratch`, where the build process, runtime data, and output will be stored. The inputdata will be downloaded automatically when you run the script. This will be the default data for the test. Or, if you want to run simulations using your own site data, you'll need to prepare your own forcing data and specify where you located it.

If you run this without encountering any errors, congratulations! You have successfully executed FATES in a container.

Once the process is complete, you can check the output. Navigate to the projects folder on your computer (not inside the container; while that is an option, we’ll skip this for now to quickly review the output). From the `projects` directory, go to `scratch`, then to `E3SM_FATES_TEST`, followed by `archive`, then `lnd`, and finally `hist`. At the top, you should find a file named `Aggregated_E3SM_FATES_TEST_Output.nc`—this is not a default name, you can change it. This file contains the output of the test.

This is the path on my machine:

```bash
/Users/XXX/projects/scratch/E3SM_FATES_TEST/archive/lnd/hist/Aggregated_E3SM_FATES_TEST_Output.nc
````

The `.nc` extension indicates that this is a NetCDF file. You can open it with any software that supports NetCDF files, such as Panoply, NCO, or CDO. Alternatively, you can use Python or R. If you are new to these tools, I recommend starting with Panoply, as it is user-friendly.

You can download Panoply from [here](https://www.giss.nasa.gov/tools/panoply/download/). After installing Panoply, open the program and load the file `Aggregated_E3SM_FATES_TEST_Output.nc`, or simply double-click the file to open it. You will see various outputs. Typically, the first variables users explore are GPP (Gross Primary Production) and total biomass in live plants. To view GPP, locate the variable named `FATES_GPP` and click on it. For total biomass in live plants, find `FATES_VEGC` and click on it.

Please note that the model was run for just one year for testing purposes. However, the model can run for an extended period as needed.

## To leave the container

Inside the container, click the following command to exit the container:

```bash
exit
````

## To stop the container

```bash
podman compose down
````

Always remember to stop the container when you are done using it. This will save resources on your computer. Additionally, keep in mind that anything you created inside the container will be lost when you stop it. However, the `inputdata`, `scratch`, `scripts`, and other files you created inside the `projects_mirror` directory will remain in your machine, as we are mirroring the projects directory.