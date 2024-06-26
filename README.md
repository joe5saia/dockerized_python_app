# Dockerized Python Script

This repo contains a very simple Dockerized python application that makes use of Docker and requirements.txt to
create a reproducible enviroment for exectuing this script. 

## How to Use

To use this container we first need to build it and then run it. To build the container
we need to use the "docker build" command. "Building" a container means taking the container
definition in the Dockerfile and turning it into a useable artifact that can be executed. This
is done using the following command

```bash
docker built -t my_script_app .
```

The `-t` argument stands for "tag" and it gives the container a user friendly name. The "."
argument tells the docker build command to look for the Dockerfile in the current directory.

## Running the script within the container

To run the script we can use the `docker run` command. Because our script takes 
arguments, we need to overwrite the "CMD" in the Dockerfile with the full command
we want to use, including the arguments. 

```bash
docker run -t my_script_app python script.py --first_name John --last_name Doe
```

`docker run -t my_script_app` tells docker to run the container with tag `my_script_app`

`python script.py --first_name John --last_name Doe` tells docker the command that we
want to execute within the container.


## Running Interactively

To run code interactively you can use the following command to start the docker container
and then have access to it's terminal.

```bash
docker run -it -t my_script_app python 
```

the `-it` flag stands for "interactive". We also changed the command to run within the container to just `python` to 
open the Python terminal. At this point we can copy and paste code from our file into the terminal to run it, and also
enter any python commands we want to help test and debug.


## Docker Setup

To set up Docker Desktop, you can follow these steps:

Download Docker Desktop for your operating system from the official Docker website: https://www.docker.com/products/docker-desktop.

Install Docker Desktop by running the downloaded installer and following the on-screen instructions.

Once the installation is complete, open Docker Desktop and ensure that it is running properly.

Verify the installation by opening a terminal or command prompt and running the command 

```bash
docker --version
```
You should see the version information for both the Docker client and server.

By following these steps, you will have Docker Desktop set up on your machine, allowing you to build, run, and manage Docker containers. For more detailed instructions, you can refer to the official Docker documentation: https://docs.docker.com/desktop/.


## Creating requirements.txt file

If you need to create a new requirements.txt file do the following.

1. Create an empty `requirements.txt` file if it does not exist already
2. Build the container `docker built -t my_script_app .`
3. Start the container and gain access to it's bash shell `docker run -it -t my_script_app bash`
4. Run `pip install package1 package2 ...` to install the packages in the container
5. Run `pip freeze` to print the exact version of every package
6. Copy the outputs of the `pip freeze` command into the `requirements.txt` file on your local machine
7. Exit the container by typing `exit` into the container bash shell
8. Rebuild the container using `docker built -t my_script_app .`
