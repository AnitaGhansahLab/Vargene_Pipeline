# Vargene_Pipeline

This repository contains an SOP for setting up a docker container for running the
[Day Lab Vargene Tutorial](https://github.com/UniMelb-Day-Lab/tutorialDBLalpha). 

## Step 1 (Install Docker) 

Go to the [Docker Manuals Page](https://docs.docker.com/desktop/), navigate to the __Install Docker Desktop__ Widget and follow the instructions for installing docker on your operating system. 
## Step 2 (Pull the container from Docker) 

From your terminal, pull the docker image from the [repository](https://hub.docker.com/repository/docker/lucifry/ghansahlab/tags) using:

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

Replace `<name/ID-of-image>` with the name of the image that was pulled from docker, in this case, `luci-fry/ghansahlab`.

If the above command is successful, you will see that command line will show that you have root access like in the image below: 

<img width="230" alt="root" src="https://github.com/user-attachments/assets/6195e765-20ea-4315-acec-97024c02edf4">

You can now go ahead and list the files in the root directory: 
```bash
ls       
```

The output should look like this: 

<img width="1406" alt="Home" src="https://github.com/user-attachments/assets/f96479e4-f095-4599-aa42-e4ea4d5c7078">

Your files can be found in the `varpipelines` directory. 

## Step 4 (Activate the Anaconda Environment) 

An Anaconda (conda) environment has been set up within the container to house more packages that are necessary for running the [DBLalpha Tutorial](https://github.com/UniMelb-Day-Lab/tutorialDBLalpha). The conda environment in this container is called DBLa. You can activate it using: 

```python
conda activate DBLa
```

Now you are ready to run the [DBLalpha Tutorial](https://github.com/UniMelb-Day-Lab/tutorialDBLalpha) !


## Running the [DBLalpha Tutorial](https://github.com/UniMelb-Day-Lab/tutorialDBLalpha) 

The scripts needed for each step in the [DBLalpha Tutorial](https://github.com/UniMelb-Day-Lab/tutorialDBLalpha) can be found in the Scripts directory. **Note** that the only change that has been made to these scripts is the inclusion of the actual paths (locations) of the software dependencies within the docker container. It is therefore advised to obtain the script from the [DBLalpha Tutorial](https://github.com/UniMelb-Day-Lab/tutorialDBLalpha) tutorial page in case any updates are made. The path (locations) of the software dependencies can then be retrieved from the scripts in the Scripts folder. 


