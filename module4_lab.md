---
layout: tutorial_page
permalink: /epigenomics_2018_module4_lab
title: Epigenomics Lab 4
header1: Workshop Pages for Students
header2: Epigenomic Data Analysis 2018 Module 4 Lab
image: /site_images/CBW_Epigenome-data_icon.jpg
home: https://bioinformaticsdotca.github.io/epigenomics_2018
description: Downstream Analyses and Integrative Tools
author: David Bujold
modified: June 16th 2018
---

# Module 4: Downstream analyses & integrative tools
*by David Bujold, M.Sc.*

## Important notes:
* Please refer to the following guide for instructions on how to connect to the Compute Canada cluster: [Compute Canada instructions](https://bioinformaticsdotca.github.io/epigenomics_2018_hpc_2018)
* The user **lect99** below is provided as an example. You should replace it by the username that was assigned to you at the beginning of the workshop.


## Introduction

### Description of the lab
In this module's lab, we will explore some of the tools that were covered in the lecture.

* First, we will learn how to use the IHEC Data Portal's tools to fetch datasets tracks of interest.
* Second, we will explore ChIP-Seq peak prediction files to attempt discovering motifs using HOMER.
* Third, we will use these datasets with the GREAT GO enrichment tool to do functions prediction.
* Last, we'll explore and launch a few jobs on Galaxy.

### Local software that we will use
* A web browser
* ssh
* scp or WinSCP to transfer results from HOMER to your computer


## Tutorial

#####  Connect to the Mammouth HPC

We will need the HPC for some of the steps, so we'll open a shell access now. Replace *lect99* with your login name. (In Windows, you will connect using Putty.)

```
ssh lect99@workshop103.ccs.usherbrooke.ca
```

You will be in your home folder.

##### Prepare directory for module 4

* Remove any ```module4``` folder that could already exist in your home directory with the "rm" command.
* Create a new ```module4``` directory.
* Go to that directory.

```
rm -rf ~/module4
mkdir -p ~/module4
cd ~/module4
```

### 1- IHEC Data Portal

#### Exploring available datasets
* Open a web browser on your computer, and load the URL [http://epigenomesportal.ca/ihec](http://epigenomesportal.ca/ihec) .

* In the Overview page, click on the "View all" button.

* You will get a grid with all available datasets for IHEC Core Assays.
    * You can filter out visible datasets in the grid using the filtering options at the right of the grid.

* Go back to the Overview page, and select the following categories of datasets: "Histone" for the "Muscle" cell type.

* Only these categories will now get displayed in the grid. Expand the "Muscle" category by clicking on the black triangle, and select the following grid cells:

![img](https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_portal_muscle_h3k27ac.png)


#### Visualizing the tracks

* Click on the "Visualize" for the UCSC Genome Browser, at the bottom of the grid.
    * You can see that the datasets are being displayed at a mirror of the UCSC Genome Browser. These are all peaks and signal for the chosen muscle H3K27ac ChIP-Seq datasets. In the Genome Browser, you can expand the tracks by changing visibility from "pack" to "full" and clicking the "Refresh" button.

![img](https://bioinformatics-ca.github.io/2016_workshops/epigenomics/img/module4_portal_fullTrackView.png)
    
* You can also download these tracks locally for visualization in IGV.
    * Go back to the IHEC Data Portal tab.
    * Click on the "Download tracks" button at the bottom of the grid.
    * Use the download links to download a few of the available tracks.
    * Open them in IGV.

#### Tracks correlation
You can get a whole genome overview of the similarity of a group of tracks by using the Portal's correlation tool.

* Back on the grid page, from the filters at the right of the grid, add back datasets for all tissues and all assay types. You can select all checkboxes at once by click on the top checkbox, next to "Category".

![img](https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_portal_selectAllTissues.png)

![img](https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_portal_selectAllAssays.png)

* Select all ChIP-Seq marks for the cell type "Bone Marrow Derived Mesenchymal Stem Cell Cultured Cell", the first 6 columns.

![img](https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_portal_roadmap_chipseq.png)

* At the bottom of the grid, click on the button "Correlate datasets".

* You will see that tracks seem to correlate nicely, with activator marks clustering together and repressor marks forming another group. You can zoom out the view with the buttons at the lower right corner of the popup.

<img src="https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_portal_clusteringPerMark.png" alt="Region" width="750" />

* You can also use the correlation tool to assess whether datasets that are supposed to be similar actually are.
    * Close the correlation popup window with the top right "X" button.
    * Reset grid selection with the "Reset" button at the bottom of the grid.
    * Click on the grid cell for cell type "B Cell", under the "Blood" category, and assay "H3K27ac".
    * Click on "Correlate datasets".
    * One dataset seems to be an outlier... This is either a problem with the quality of the dataset, or the underlying metadata can indicate that something is different (disease status or some other key element).

![img](https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_portal_selectBcell.png)

You should get something like this:

![img](https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_portal_correlationOutlier.png)

### 2- Predicting motifs with HOMER

We will now attempt to detect motifs in peak regions for transcription factor binding sites using HOMER.

* Go back to the default IHEC Data Portal view by clicking "Data Grid" in the top bar.

<img src="https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_HOMER_selectDataGrid.png" alt="Region" width="750" />

* In the filters to the right of the grid, activate non-core IHEC assays, and display only Transcription Factor Binding Sites (```TFBS```) assays for ```ES Cells``` cell type.

![img](https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_HOMER_showNonCoreAssays.png)

![img](https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_HOMER_showTFBS.png)

![img](https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_HOMER_showESCells.png)

* In the grid, select ENCODE datasets for the YY1 assay and the H1hESC cell type.

![img](https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_HOMER_selectYY1.png)

* Go to the track list at the bottom of the grid and select only the dataset for sample "H1-hESC_YY1_Pk__HudsonAlpha_".

<img src="https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_HOMER_selectPeaksTrack.png" alt="Region" width="750" />


* You can get the URL to the track you want by clicking on the "Download tracks" button at the bottom of the grid.
Here, we're interested in ```http://epigenomesportal.ca/tracks/ENCODE/hg19/26900.ENCODE.H1-hESC_YY1_Pk__HudsonAlpha_.YY1.peak_calls.bigBed```.
* Open your Mammouth (Compute Canada) terminal session, create a directory for our HOMER-related files, and go into it. Then, download the BigBed file.

```
mkdir homer
cd homer
wget http://epigenomesportal.ca/tracks/ENCODE/hg19/26900.ENCODE.H1-hESC_YY1_Pk__HudsonAlpha_.YY1.peak_calls.bigBed
```

* Convert the bigBed file into a bed file using the UCSC set of tools. It is available as a CVMFS module.

```
module load mugqic/ucsc/20140212
bigBedToBed 26900.ENCODE.H1-hESC_YY1_Pk__HudsonAlpha_.YY1.peak_calls.bigBed 26900.ENCODE.H1-hESC_YY1_Pk__HudsonAlpha_.YY1.peak_calls.bed
```

* Prepare an output directory for HOMER, and a genome preparsed motifs directory.

```
mkdir output
mkdir preparsed
```

* Run the HOMER software to identify motifs in the peak regions. Please note that there are two modules necessary here:
    * **mugqic/homer/4.9.1** to run HOMER
    * **mugqic/weblogo/3.5.0** to create the nice motifs images that we will visualize in a browser. Don't load another module for weblogo, as the input parameters are very different across versions, and it will not work with HOMER.

```
module load mugqic/homer/4.9.1
module load mugqic/weblogo/3.5.0
findMotifsGenome.pl 26900.ENCODE.H1-hESC_YY1_Pk__HudsonAlpha_.YY1.peak_calls.bed hg19 output -preparsedDir preparsed -p 2 -S 15
```

* HOMER takes a while to execute for a whole genome track like this. Expect this job to take about 30 minutes of runtime, with the current 2 cores setup. In the meantime, we will explore the GO terms enrichment tool GREAT.

### 3- Looking for GO terms enrichment with GREAT

Next, we will try to identify GO terms connected to ChIP-Seq peaks calls using GREAT. We need BED files to use the GREAT portal. We will do the conversion on the HPC.

* In the IHEC Data Portal, go back to the default grid page (by clicking on Data Grid in the top bar). Filter the tissues list to keep only "Bone Marrow" tissues.

![img](https://bioinformatics-ca.github.io/2016_workshops/epigenomics/img/module4_GREAT_activate_all_trackhubs.png)

* Select the datasets for cell type "Myeloid cell" and assay H3K27ac.

![img](https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_GREAT_bone_marrow_h3k27ac.png)

* For this exercise, we will download only two of the bigbeds for available datasets. Pick up the one for the "ERS255952" and "ERS365962" sample.

<img src="https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_GREAT_selectSomeBoneMarrowDatasets.png" alt="Region" width="750" />

* Click "Download tracks" at the bottom of the grid.

* At the top of the download page, click on the link that says "Alternatively, you can click here to obtain a text list of all the tracks". This will give you a text list with all tracks of interest. Copy the link to this page in your clipboard, using the address provided in your browser's URL bar.

![img](https://bioinformatics-ca.github.io/2016_workshops/epigenomics/img/module4_GREAT_batch_download.png)

* Open another terminal connection to get into Mammouth.

* Go to your module4 directory and create a place to put the material we will download.

```
cd ~/module4
mkdir great
cd great
```

* For you own analyses, you can download a bunch of tracks at the same time by using wget on a list of URLs.
    * Use the **wget** command to download the text file that contains the list of tracks.

```
wget -O trackList.txt http://epigenomesportal.ca/cgi-bin/downloadList.cgi?session=3537
```

* Now download the tracks that are contained in this list.
    
```
wget -i trackList.txt
```

* Convert the bigbed using the UCSC set of tools. It is available as a CVMFS module. For this example, we will convert and use only one of the files, **24584.Blueprint.ERS255952.H3K27ac.peak_calls.bigBed**.

```
module load mugqic/ucsc/20140212
bigBedToBed 24584.Blueprint.ERS255952.H3K27ac.peak_calls.bigBed 24584.Blueprint.ERS255952.H3K27ac.peak_calls.bed
```

**Note:** If you're under Linux / Mac, you can also install the UCSC tools locally, as they are a useful set of tools to manipulate tracks data, without requiring so much processing power.

* GREAT has a limit on the number of regions to be tested in one execution. Therefore, we need to subsample our file. We can create a BED file subsample this way:
    * Sort BED file in random order with ```sort -R```
    * Take the 20000 first lines in the file with ```head -n20000```

```
sort -R 24584.Blueprint.ERS255952.H3K27ac.peak_calls.bed | head -n 20000 > 24584.Blueprint.ERS255952.H3K27ac.peak_calls.random_short.bed
```

* Download the BED files locally using **scp** / **WinSCP**. Don't forget to run the command on a local terminal session, not on Mammouth.

```
scp lect99@workshop103.ccs.usherbrooke.ca:/home/lect99/module4/great/*.bed .
```

* Load the GREAT website: [http://bejerano.stanford.edu/great/public/html/](http://bejerano.stanford.edu/great/public/html/)

* Provide the following input to the GREAT interface:
    * Assembly: **Human: GRCh37**
    * Test regions: The randomized short version of the BED files you just downloaded.

* Submit the form.

* In the results, for instance, you should obtain something like this for biological processes:

<img src="https://bioinformatics-ca.github.io/2016_workshops/epigenomics/img/module4_GREAT_go_biological_process.png" alt="Region" width="750" />

### Go back to your HOMER results

* Is the job done? If it is completed, you can bring back HOMER results to your laptop for visualiztion. **From your laptop**, use the scp command or WinSCP to bring back the results folder.

```
scp -r lect99@workshop103.ccs.usherbrooke.ca:/home/lect99/module4/homer/output .
```

Then, open the de novo and known motifs HTML files in a browser for visualization. Do the identified motifs fit what we would expect?

<img src="https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/img/module4_2018_HOMER_denovoResult.png" alt="Region" width="750" />

If your job didn't complete yet, you can download the complete results from here instead:

[Homer results](https://bioinformatics-ca.github.io/2016_workshops/epigenomics/homer_output.zip)



### Galaxy

We will now explore and learn how to use the Galaxy interface. In this short exercise, we will load a FASTQ dataset, run FastQC on it, and trim it to improve overall quality of reads.

* Using a web browser, open the following URL: [http://workshop103-galaxy.vzhost34.genap.ca/galaxy/](http://workshop103-galaxy.vzhost34.genap.ca/galaxy/)
 
While you can run Galaxy jobs without creating an account, features and number of jobs that can be executed at once will be limited. We should therefore create an account.

* On the top menu, click on "User" > "Register"

* Fill the email, password and public name boxes, and click on "Submit"

* Click on "Return to the home page."

* You are now logged in as a Galaxy user. For this exercise, we’ll use subsets of data from the Illumina BodyMap 2.0 project, from human adrenal gland tissues. The sampled reads are paired-end 50bp that map mostly to a 500Kb region of chromosome 19, positions 3-3.5 million (chr19:3000000:3500000). (source: https://usegalaxy.org/u/jeremy/p/galaxy-rna-seq-analysis-exercise)

* Import the following two FASTQ files in your user space. To do so:
    * Use Get Data > Upload File from the tool section
    * Go to the ```Paste/Fetch data``` section
    * You can provide both URLs in the same text box
        * [https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/files/adrenal_1.fastq](https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/files/adrenal_1.fastq)
        * [https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/files/adrenal_2.fastq](https://raw.githubusercontent.com/bioinformaticsdotca/Epigenomics_2018/master/files/adrenal_2.fastq)
    * For Genome, specify “Human (Home sapiens): hg19”
    * Click on ```Start```.

* After it finished to upload (green state), rename the two imported files, for better organization.
    * From the history column, click on the ```Pen``` icon for the first imported item, and enter the new name “adrenal_1” in the dialog.
    * Rename the second imported file to “adrenal_2”.
    * Examine results from the history bar using the ```Eye``` icon.

* Run the tool FastQC: Comprehensive QC for adrenal_1.
    * To find it, use the search window at the top of the Tools column (left panel).
    * Execute, then examine results from the history bar using the ```Eye``` icon.
    * Repeat the same operations for adrenal_2. As a shortcut, you can click on the new file name in our history, then click on the ```Run this job again``` icon and simply change the input file to automatically reuse the same parameters.

* Many tools using FASTQ files in Galaxy require them to be “groomed”, meaning they will be standardized. This will ensure more reliability and consistency to those tools output. To groom our FASTQ files, we will use the tool FASTQ Groomer with default parameters.
    * When we don’t know which quality score type to provide, we can extract that information from the FastQC report that we already generated. Can you find the information in the FastQC report? (Answer: It’s in Sanger format)
    * Leave the other options as-is.
    * Run this for both of our paired-end files, adrenal_1 and adrenal_2.

* You will now trim the reads, to improve the quality of the dataset by removing bad quality bases, clipping adapters and so on. Launch the Trimmomatic tool with default parameters, except:
    * Give the groomed adrenal_1 file for direction 1, and groomed adrenal_2 for direction 2.
    * Sliding window size: 4
    * Average quality required: 30

* Run FastQC again on both paired files, and compare results with pre-trimming FastQC output.

### All done!

If you have time remaining, you can try running other types of jobs on Galaxy, or explore further the tools that we covered in this lab, using other types of datasets. For example, does running a GREAT query on another cell type yield the type of annotations that you'd expect?
