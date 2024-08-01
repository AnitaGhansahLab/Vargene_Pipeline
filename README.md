# Vargene_Pipeline

This repository contains an SOP for setting up a docker container for running the
[Day Lab Vargene Tutorial](https://github.com/UniMelb-Day-Lab/tutorialDBLalpha). 

## Step 1 (Install Docker) 

Go to the [Docker Manuals Page](https://docs.docker.com/desktop/), navigate to the __Install Docker Desktop__ Widget and follow the instructions for installing docker on your operating system. 
## Step 2 (Pull the container from Docker) 

On Pull the docker image from the [repository](https://hub.docker.com/repository/docker/lucifry/ghansahlab/tags) using:

```bash
docker pull lucifry/ghansahlab:latest
```
## Step 3 (Run the Container)

Change your current working directory to the directory that contains the files and scripts you want to work on. 

First, find out what your working directory is: 
```bash
pwd
```

If this directory is not the one that contains the files you want to work on, change the directory using: 
```bash
cd <path-to-your-directory>
```
Remember to replace `<path-to-your-directory>` with the actual path to your working directory. 

Next, run the container using: 
```bash
docker run -it --platform linux/x86_64 -v "$(pwd)":/varpipelines <name/ID-of-image> bash
```

Replace `name/ID-of-image>` with the name of the image that was pulled from docker, in this case, `luci-fry/ghansahlab`

If the above command is successful, you will see that command line will show that you have root access like in the image below: 
![alt text](https://drive.google.com/file/d/1I0U5z2qRS-cPG5fKU-4Mr87DH2U9CiWs/view?usp=drive_link "Root Access")

