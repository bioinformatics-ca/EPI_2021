---
layout: tutorial_page
permalink: /epigenomics_2018_hpc_2018
title: Epigenomics HPC
header1: Workshop Pages for Students
header2: Using the Compute Canada HPC
image: /site_images/CBW_Epigenome-data_icon.jpg
home: https://bioinformaticsdotca.github.io/epigenomics_2018
description: Using the Compute Canada HPC
author: David Bujold
modified: June 13th 2018
---

# Using the Compute Canada HPC
*by David Bujold, M.Sc.*

This document provides information on how to get started with the Compute Canada HPC setup prepared for this workshop.


## Connecting to the Mammouth HPC workshop node:

**Host:** workshop103.ccs.usherbrooke.ca

**Login / Password:** Provided to you on a separate piece of paper at the beginning of the workshop.


#### Linux/Mac
Use the following line from the command line, replacing ```username``` with your assigned username.
```
ssh username@workshop103.ccs.usherbrooke.ca
```


#### Windows
Connect to the ```workshop103.ccs.usherbrooke.ca``` server using the **Putty** tool that you installed for this workshop.


## The first time you log in
As the ```$MUGQIC_INSTALL_HOME``` environment variable is required by some CVMFS modules, you should set an environment variable to define it.
To do so, we'll add a command to the ```~/.bashrc``` file. which is executed automatically every time you start an interactive session.

```
[lect99@workshop103 ~]$ echo 'export MUGQIC_INSTALL_HOME=/cvmfs/soft.mugqic/CentOS6' >> ~/.bashrc
[lect99@workshop103 ~]$ source ~/.bashrc
```

You can see that the environment variable has been properly set by running the following command:
```
[lect99@workshop103 ~]$ echo $MUGQIC_INSTALL_HOME
/cvmfs/soft.mugqic/CentOS6
```

## Loading a module
All available software are organized as modules that you can load. For example, to start using Java 7, you need to load the Java 7 module.


**1- Get the list of available modules**
```
[lect99@workshop103 ~]$ module avail
```

**2- Load your module of choice**
```
[lect99@workshop103 ~]$ module load mugqic/java/openjdk-jdk1.7.0_60
```

**3- You can now run the module you loaded directly**
The following command will display on screen the current version of Java that's been loaded:
```
[lect99@workshop103 ~]$ javac -version
javac 1.7.0_60-ea
```


### Using a bash script
You can specify a bash script to launch multiple compute jobs directly from the command line, like the ```testjob.sh``` script in this example:
```
#!/bin/bash

module load mugqic/bowtie2/2.2.4 mugqic/bismark/0.17.0
bismark_genome_preparation --bowtie2 --verbose .
```

Here, we load the bowtie2 and bismark modules, and then launch the ```bismark_genome_preparation``` command.



## Downloading a file from the workshop server to your computer

#### Linux/Mac
Use the following from a **local** command line session:
```
cd /path/to/local/destination/folder
scp lect99@workshop103.ccs.usherbrooke.ca:/home/lect99/myfile.txt .
```

To download a full directory (with all sub-directories), add the **-R** option
```
cd /path/to/destination/folder
scp -r lect99@workshop103.ccs.usherbrooke.ca:/home/lect99/myfiles/ .
```

#### Windows
Use the WinSCP software that you installed for this workshop, connecting to ```workshop103.ccs.usherbrooke.ca``` with your login and password.
