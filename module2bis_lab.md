---
layout: tutorial_page
permalink: /epigenomics_2018_module2b_lab
title: Epigenomics Lab 2
header1: Workshop Pages for Students
header2: Epigenomic Data Analysis 2018 Module 2 Lab
image: /site_images/CBW_Epigenome-data_icon.jpg
home: https://bioinformaticsdotca.github.io/epigenomics_2018
---


CALLING ENRICHMENTS using MACS2

by Misha Bilenky

Set up our variables  
```
source /home/partage/epigenomics/chip-seq/setup.sh
```
Load Python2.7.* and MACS2 modules  
```
module load mugqic/python/2.7.11
module load mugqic/MACS2/2.1.1.20160309
```
The MACS2 tutorial can be found:  

https://github.com/taoliu/MACS  

Check macs2 version (and see that it is properly loaded)  
```
macs2 --version
```


Regular peak calling with macs2:  
```
cd
signal=/home/partage/epigenomics/chip-seq/H1.chr19/H3K4me3.H1.chr19.bam
control=/home/partage/epigenomics/chip-seq/H1.chr19/Input.H1.chr19.bam
macs2 callpeak -t $signal -c $control -f BAM -g hs -n H3K4me3.H1.chr19 -B -q 0.01 --outdir ~/H1.macs2.chr19 
```
Parameters (see https://github.com/taoliu/MACS for more details)  

`-t` treatment  
`-c` control  
`-f` input files format  
`-g`  using human genome  
`-n` name  
`-B` generate output as a bedGraph  
  
  
 That is what we see on the screen:  
 ```
[stud02@workshop103 ~]$ macs2 callpeak -t $signal -c $control -f BAM -g hs -n H3K4me3.H1.chr19 -B -q 0.01 --outdir ~/H1.macs2.chr19 
INFO  @ Tue, 19 Jun 2018 05:51:16: 
# Command line: callpeak -t /home/partage/epigenomics/chip-seq/H1.chr19/H3K4me3.H1.chr19.bam -c /home/partage/epigenomics/chip-seq/H1.chr19/Input.H1.chr19.bam -f BAM -g hs -n H3K4me3.H1.chr19 -B -q 0.01 --outdir /home/stud02/H1.macs2.chr19
# ARGUMENTS LIST:
# name = H3K4me3.H1.chr19
# format = BAM
# ChIP-seq file = ['/home/partage/epigenomics/chip-seq/H1.chr19/H3K4me3.H1.chr19.bam']
# control file = ['/home/partage/epigenomics/chip-seq/H1.chr19/Input.H1.chr19.bam']
# effective genome size = 2.70e+09
# band width = 300
# model fold = [5, 50]
# qvalue cutoff = 1.00e-02
# Larger dataset will be scaled towards smaller dataset.
# Range for calculating regional lambda is: 1000 bps and 10000 bps
# Broad region calling is off
# Paired-End mode is off
 
INFO  @ Tue, 19 Jun 2018 05:51:16: #1 read tag files... 
INFO  @ Tue, 19 Jun 2018 05:51:16: #1 read treatment tags... 
INFO  @ Tue, 19 Jun 2018 05:51:23:  1000000 
INFO  @ Tue, 19 Jun 2018 05:51:27: #1.2 read input tags... 
INFO  @ Tue, 19 Jun 2018 05:51:33:  1000000 
INFO  @ Tue, 19 Jun 2018 05:51:40:  2000000 
INFO  @ Tue, 19 Jun 2018 05:51:43: #1 tag size is determined as 36 bps 
INFO  @ Tue, 19 Jun 2018 05:51:43: #1 tag size = 36 
INFO  @ Tue, 19 Jun 2018 05:51:43: #1  total tags in treatment: 1697605 
INFO  @ Tue, 19 Jun 2018 05:51:43: #1 user defined the maximum tags... 
INFO  @ Tue, 19 Jun 2018 05:51:43: #1 filter out redundant tags at the same location and the same strand by allowing at most 1 tag(s) 
INFO  @ Tue, 19 Jun 2018 05:51:43: #1  tags after filtering in treatment: 1235613 
INFO  @ Tue, 19 Jun 2018 05:51:43: #1  Redundant rate of treatment: 0.27 
INFO  @ Tue, 19 Jun 2018 05:51:43: #1  total tags in control: 2539258 
INFO  @ Tue, 19 Jun 2018 05:51:43: #1 user defined the maximum tags... 
INFO  @ Tue, 19 Jun 2018 05:51:43: #1 filter out redundant tags at the same location and the same strand by allowing at most 1 tag(s) 
INFO  @ Tue, 19 Jun 2018 05:51:43: #1  tags after filtering in control: 2227048 
INFO  @ Tue, 19 Jun 2018 05:51:43: #1  Redundant rate of control: 0.12 
INFO  @ Tue, 19 Jun 2018 05:51:43: #1 finished! 
INFO  @ Tue, 19 Jun 2018 05:51:43: #2 Build Peak Model... 
INFO  @ Tue, 19 Jun 2018 05:51:43: #2 looking for paired plus/minus strand peaks... 
INFO  @ Tue, 19 Jun 2018 05:51:44: #2 number of paired peaks: 13050 
INFO  @ Tue, 19 Jun 2018 05:51:44: start model_add_line... 
INFO  @ Tue, 19 Jun 2018 05:51:44: start X-correlation... 
INFO  @ Tue, 19 Jun 2018 05:51:44: end of X-cor 
INFO  @ Tue, 19 Jun 2018 05:51:44: #2 finished! 
INFO  @ Tue, 19 Jun 2018 05:51:44: #2 predicted fragment length is 297 bps 
INFO  @ Tue, 19 Jun 2018 05:51:44: #2 alternative fragment length(s) may be 297 bps 
INFO  @ Tue, 19 Jun 2018 05:51:44: #2.2 Generate R script for model : /home/stud02/H1.macs2.chr19/H3K4me3.H1.chr19_model.r 
INFO  @ Tue, 19 Jun 2018 05:51:44: #3 Call peaks... 
INFO  @ Tue, 19 Jun 2018 05:51:44: #3 Pre-compute pvalue-qvalue table... 
INFO  @ Tue, 19 Jun 2018 05:51:46: #3 In the peak calling step, the following will be performed simultaneously: 
INFO  @ Tue, 19 Jun 2018 05:51:46: #3   Write bedGraph files for treatment pileup (after scaling if necessary)... H3K4me3.H1.chr19_treat_pileup.bdg 
INFO  @ Tue, 19 Jun 2018 05:51:46: #3   Write bedGraph files for control lambda (after scaling if necessary)... H3K4me3.H1.chr19_control_lambda.bdg 
INFO  @ Tue, 19 Jun 2018 05:51:46: #3   Pileup will be based on sequencing depth in treatment. 
INFO  @ Tue, 19 Jun 2018 05:51:46: #3 Call peaks for each chromosome... 
INFO  @ Tue, 19 Jun 2018 05:51:46: #4 Write output xls file... /home/stud02/H1.macs2.chr19/H3K4me3.H1.chr19_peaks.xls 
INFO  @ Tue, 19 Jun 2018 05:51:46: #4 Write peak in narrowPeak format file... /home/stud02/H1.macs2.chr19/H3K4me3.H1.chr19_peaks.narrowPeak 
INFO  @ Tue, 19 Jun 2018 05:51:46: #4 Write summits bed file... /home/stud02/H1.macs2.chr19/H3K4me3.H1.chr19_summits.bed 
INFO  @ Tue, 19 Jun 2018 05:51:46: Done! 
[stud02@workshop103 ~]$ 
 ```
 
Check the output folder  
```
cd H1.macs2.chr19
ls -l
```
We see following files:  
```
[stud02@workshop103 H1.macs2.chr19]$ ll
total 82468
-rw-r--r-- 1 stud02 stud 157201685 Jun 19 02:12 H3K4me3.H1.chr19_control_lambda.bdg
-rw-r--r-- 1 stud02 stud     77804 Jun 19 02:12 H3K4me3.H1.chr19_model.r
-rw-r--r-- 1 stud02 stud    150042 Jun 19 02:12 H3K4me3.H1.chr19_peaks.narrowPeak
-rw-r--r-- 1 stud02 stud    167335 Jun 19 02:12 H3K4me3.H1.chr19_peaks.xls
-rw-r--r-- 1 stud02 stud    100876 Jun 19 02:12 H3K4me3.H1.chr19_summits.bed
-rw-r--r-- 1 stud02 stud  55449194 Jun 19 02:12 H3K4me3.H1.chr19_treat_pileup.bdg
```
Check how many peaks we called  
```
wc -l H3K4me3.H1.chr19_peaks.narrowPeak
```
1698 H3K4me3.H1.chr19_peaks.narrowPeak  

This was only for chr19 (as an example)  

Running same command for the whole genome took ~1h. Results are located in   
```
ls -l /home/partage/epigenomics/chip-seq/macs2
```  
You see  
```
total 2614211
-rw-r--r-- 1 stud02 stud 5374836445 Jun 19 01:20 H3K4me3.H1_control_lambda.bdg
-rw-r--r-- 1 stud02 stud      78292 Jun 19 00:55 H3K4me3.H1_model.r
-rw-r--r-- 1 stud02 stud    3550063 Jun 19 01:20 H3K4me3.H1_peaks.narrowPeak
-rw-r--r-- 1 stud02 stud    3988586 Jun 19 01:20 H3K4me3.H1_peaks.xls
-rw-r--r-- 1 stud02 stud    2309723 Jun 19 01:20 H3K4me3.H1_summits.bed
-rw-r--r-- 1 stud02 stud 1038752798 Jun 19 01:20 H3K4me3.H1_treat_pileup.bdg
```
Total number of H3K4me3 peaks genome wide is  
```
[stud02@workshop103 macs2]$ wc -l H3K4me3.H1_peaks.narrowPeak 
44679 H3K4me3.H1_peaks.narrowPeak
```

Using 'awk' we can count number of bases in enriched peaks genome wide:  
```
[stud02@workshop103 macs2]$ less H3K4me3.H1_peaks.narrowPeak | awk '{s=s+$3-$2+1} END{print s}'
41872307
```
This is approximatly ~1.6% of mappable genome 41872307/2700000000.  


