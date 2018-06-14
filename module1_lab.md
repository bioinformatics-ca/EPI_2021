---
layout: tutorial_page
permalink: /epigenomics_2018_module1_lab
title: Epigenomics Lab 1
header1: Workshop Pages for Students
header2: Epigenomic Data Analysis 2018 Module 1 Lab
image: /site_images/CBW_Epigenome-data_icon.jpg
home: https://bioinformaticsdotca.github.io/epigenomics_2018
description: This module will cover the basics of how to login to the cluster, launch jobs and perform a basic QC analysis of the data sets.
author: Martin Hirst
modified: 2017-08-10
---

# Module 1: Introduction to ChIP sequencing & analysis 

## Important notes:
* Please refer to the following guide for instructions on how to connect to the workshop server and required modules [Using Compute Canada](http://bioinformaticsdotca.github.io/epigenomics_2017_hpc_2017)  
* The user **class99** is provided here as an example. You should replace it by the username that was assigned to you at the beginning of the workshop.


## Introduction

### Description of the lab
This module will cover the basics of how to login to the cluster, launch jobs and perform a basic QC analysis of the data sets.

### Local software that we will use
* ssh
* Web browser to visualize FastQC output


## Tutorial

### Getting started

#####  Connect to the Workshop server
```
ssh class99@workshop103.ccs.usherbrooke.ca
```

You will be in your home folder. 

##### Prepare directory for module 1
```
rm -rf ~/module1
mkdir -p ~/module1
cd ~/module1
```

##### Prepare environment for module 1
```
module load mugqic/java mugqic/fastqc
```

### Assessing FASTQ file quality with FastQC

##### Copy locally the FASTQ file that we will need for our FastQC analysis
```
cp /home/partage/epigenomics/chip-seq/H1/data/H3K27ac/H3K27ac.H1.fastq.gz
```

##### Check files

At this point if you type ```ls``` should have something like:
```
class99@workshop103$ ls
H3K27ac.H1.fastq.gz
```

#####  Check FastQC options 
```
fastqc -h
```

#####  Run the FastQC command 
```
fastqc H3K27ac.H1.fastq.gz
```

##### Check files
At this point if you type ```ls``` should have something like:

```
class99@workshop103$ ls
H3K27ac.H1_fastqc.html	H3K27ac.H1_fastqc.zip  H3K27ac.H1.fastq.gz
```

#####  Download the results to your local computer
```
scp class99@workshop103.ccs.usherbrooke.ca:/home/class99/module1/H3K27ac.H1_fastqc.html .
```

#####  Open the downloaded file in a web browser

Open the folder and then double-click the file 
```
open .
```

Or directly from the command line using a command such as
```
firefox H3K27ac.H1_fastqc.html
```
