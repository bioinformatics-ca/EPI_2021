---
layout: tutorial_page
permalink: /EPI_2021_Module2_lab
title: EPI 2021 Module 2 Lab
header1: Workshop Pages for Students
header2: Epigenomic Analysis 2021
image: /site_images/CBW_Epigenome-data_icon.jpg
home: https://bioinformaticsdotca.github.io/EPI_2021
description: Introduction to ChIP-seq and analysis
author: Martin Hirst and Edmund Su

---

# Introduction to ChIP-seq and analysis

*by Martin Hirst and Edmund Su*

# Table of contents:

<font size="5">[Common tools of the trade](#Common-tools-of-the-trade)</font>

<font size="5">[Module 2. Peak Calling](#Module-2.-Peak-Calling)</font>






## <B>Common tools of the trade</B>
***
### <B>- Explaination of tools</B>
|Tool|Website|Info|
|----|------|-----|
|BWA|http://bio-bwa.sourceforge.net/bwa.shtml| Genomic Sequence Read alignment tool |
|PICARD|https://broadinstitute.github.io/picard/| Toolkit for BAM file manipulation
|SAMTOOLS|http://www.htslib.org/doc/samtools.html| Toolkit for BAM file manipulation |
|BEDTOOLS|https://bedtools.readthedocs.io/en/latest/index.html | Toolkit for BED/BEDGRAPH file manipulation |
|MACS2|https://github.com/macs3-project/MACS | Enriched region identifier for ChIP-seq |
|UCSCtools|http://genome.ucsc.edu/goldenPath/help/bigWig.html| Manipulation of Wigs and Bed/Bedgraph to binary forms|

### <B>- Resource files</B>
|File name | File location| Source
|---|---|--|
|BWA INDEX|~/CourseData/EPI_data/Module1/BWA_index/| |
|Enhancer file.bed|~/CourseData/EPI_data/Module1/QC_resources/|download various state7 and merge https://egg2.wustl.edu/roadmap/data/byFileType/chromhmmSegmentations/ChmmModels/coreMarks/jointModel/final/|
|TSS.bed|~/CourseData/EPI_data/Module1/QC_resources/|Generated by downloading Ensemblv79 GTF convert to Bed +/-2kb of TSS. See https://www.biostars.org/p/56280/|
|HOX regions.bed|~/CourseData/EPI_data/Module1/QC_resources/|Generated by downloading Ensemblv79 GTF convert to Bed then selecting for HOX|
|Hg38 Black list regions|~/CourseData/EPI_data/Module1/QC_resources/|https://www.encodeproject.org/files/ENCFF356LFX/@@download/ENCFF356LFX.bed.gz|

### <B>- Resource files</B>
|File name | File location| Source
|---|---|--|
|CEMT Pooled Breast Basal|~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69069.CEEHRC.CEMT0035.H3K27ac.peak_calls.bigBed
|CEMT Pooled Breast Basal ||https://epigenomesportal.ca/tracks/CEEHRC/hg38/69067.CEEHRC.CEMT0035.H3K27ac.signal_unstranded.bigWig
|CEMT Pooled Breast Basal |~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69063.CEEHRC.CEMT0035.H3K27me3.peak_calls.bigBed
|CEMT Pooled Breast Basal ||https://epigenomesportal.ca/tracks/CEEHRC/hg38/69061.CEEHRC.CEMT0035.H3K27me3.signal_unstranded.bigWig
|CEMT Pooled Breast Basal |~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69054.CEEHRC.CEMT0035.H3K4me1.peak_calls.bigBed
|CEMT Pooled Breast Basal | |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69052.CEEHRC.CEMT0035.H3K4me1.signal_unstranded.bigWig
|CEMT Pooled Breast Basal |~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69057.CEEHRC.CEMT0035.H3K4me3.peak_calls.bigBed
|CEMT Pooled Breast Basal | |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69055.CEEHRC.CEMT0035.H3K4me3.signal_unstranded.bigWig
|CEMT Pooled Breast Basal | |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69070.CEEHRC.CEMT0035.Input.signal_unstranded.bigWig
|CEMT Pooled Breast Stromal|~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69088.CEEHRC.CEMT0036.H3K27ac.peak_calls.bigBed
|CEMT Pooled Breast Stromal| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69086.CEEHRC.CEMT0036.H3K27ac.signal_unstranded.bigWig
|CEMT Pooled Breast Stromal|~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69082.CEEHRC.CEMT0036.H3K27me3.peak_calls.bigBed
|CEMT Pooled Breast Stromal| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69080.CEEHRC.CEMT0036.H3K27me3.signal_unstranded.bigWig
|CEMT Pooled Breast Stromal|~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69073.CEEHRC.CEMT0036.H3K4me1.peak_calls.bigBed
|CEMT Pooled Breast Stromal| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69071.CEEHRC.CEMT0036.H3K4me1.signal_unstranded.bigWig
|CEMT Pooled Breast Stromal|~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69076.CEEHRC.CEMT0036.H3K4me3.peak_calls.bigBed
|CEMT Pooled Breast Stromal| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69074.CEEHRC.CEMT0036.H3K4me3.signal_unstranded.bigWig
|CEMT Pooled Breast Stromal| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69089.CEEHRC.CEMT0036.Input.signal_unstranded.bigWig
|CEMT Pooled Breast Luminal|~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69107.CEEHRC.CEMT0037.H3K27ac.peak_calls.bigBed
|CEMT Pooled Breast Luminal| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69105.CEEHRC.CEMT0037.H3K27ac.signal_unstranded.bigWig
|CEMT Pooled Breast Luminal|~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69101.CEEHRC.CEMT0037.H3K27me3.peak_calls.bigBed
|CEMT Pooled Breast Luminal| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69099.CEEHRC.CEMT0037.H3K27me3.signal_unstranded.bigWig
|CEMT Pooled Breast Luminal|~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69092.CEEHRC.CEMT0037.H3K4me1.peak_calls.bigBed
|CEMT Pooled Breast Luminal| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69090.CEEHRC.CEMT0037.H3K4me1.signal_unstranded.bigWig
|CEMT Pooled Breast Luminal|~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69095.CEEHRC.CEMT0037.H3K4me3.peak_calls.bigBed
|CEMT Pooled Breast Luminal| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69093.CEEHRC.CEMT0037.H3K4me3.signal_unstranded.bigWig
|CEMT Pooled Breast Luminal| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69108.CEEHRC.CEMT0037.Input.signal_unstranded.bigWig
|CEMT Pooled Breast Luminal Progenitor|~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69126.CEEHRC.CEMT0038.H3K27ac.peak_calls.bigBed
|CEMT Pooled Breast Luminal Progenitor| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69124.CEEHRC.CEMT0038.H3K27ac.signal_unstranded.bigWig
|CEMT Pooled Breast Luminal Progenitor|~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69120.CEEHRC.CEMT0038.H3K27me3.peak_calls.bigBed
|CEMT Pooled Breast Luminal Progenitor| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69118.CEEHRC.CEMT0038.H3K27me3.signal_unstranded.bigWig
|CEMT Pooled Breast Luminal Progenitor|~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69111.CEEHRC.CEMT0038.H3K4me1.peak_calls.bigBed
|CEMT Pooled Breast Luminal Progenitor| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69109.CEEHRC.CEMT0038.H3K4me1.signal_unstranded.bigWig
|CEMT Pooled Breast Luminal Progenitor|~/CourseData/EPI_data/Module1/CHEERC_resources|https://epigenomesportal.ca/tracks/CEEHRC/hg38/69114.CEEHRC.CEMT0038.H3K4me3.peak_calls.bigBed
|CEMT Pooled Breast Luminal Progenitor| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69112.CEEHRC.CEMT0038.H3K4me3.signal_unstranded.bigWiig
|CEMT Pooled Breast Luminal Progenitor| |https://epigenomesportal.ca/tracks/CEEHRC/hg38/69127.CEEHRC.CEMT0038.Input.signal_unstranded.bigWig

## <B>Module 2. Peak Calling</B>
***
<div><input type="checkbox" name="chk" checked>1. Dedup BAM file</div>
<div><input type="checkbox" name="chk">2. Running a peak caller</div>
<div><input type="checkbox" name="chk">3. Remove blacklist regions</div>
<div><input type="checkbox" name="chk">4. Visualization</div>


### <B>Setup</B>
<code style="background:white;color:black">mkdir ~/workspace/peaks</code>

<code style="background:black;color:black">samtools index -@4 ~/CourseData/EPI_data/Module1/MCF10A_resources/*.bam</code>

### <B>1. Dedup BAM file</B>
##### Code:
<code style="background:black;color:black">
treatment_bam=~/CourseData/EPI_data/Module1/MCF10A_resources/MCF10A_H3K27ac.bam
treatment_dedup=~/workspace/peaks/MCF10A_H3K27ac.dedup.bam
samtools view -@4 ${treatment_bam} -bh -q10 -F1028 -o ${treatment_dedup}
input_bam=~/CourseData/EPI_data/Module1/MCF10A_resources/MCF10A_Input.bam
input_dedup=~/workspace/peaks/MCF10A_Input.dedup.bam
samtools view -@4 ${treatment_bam} -bh -q10 -F1028 -o ${treatment_dedup}
</code>

##### Code Breakdown:
```Shell
samtools view -@4 ${treatment_bam} -bh -q10 -F1028 chr19# {"-F1028": removes reads that unmapped and duplicated,
"-@4": uses two threads,
"-bh": outputs in binary,
"q10": MAPQ must be >=10

```

##### Comments:
```Shell
This step will take a while, copies have been prepared in resources. Smallest file taking 3 minutes. Longest taking 10.
```

### <B>2. Running a peak caller</B>
##### Code:
```Shell
mkdir -p ~/workspace/peaks
treatment_frag=~/CourseData/EPI_data/Module1/MCF10A_resources/MCF10A_H3K27ac.dedup.bam
input_frag=~/CourseData/EPI_data/Module1/MCF10A_resources/MCF10A_Input.dedup.bam
name=MCF10A_H3K27ac

macs3 callpeak -t ${treatment_frag} -c ${input_frag} -f BAMPE -g hs -n ${name} --keep-dup all --outdir ~/workspace/peaks/ --bdg 1> ~/workspace/peaks/${name}.out.log 2> ~/workspace/peaks/${name}.err.log
```

##### Code Breakdown:
```Shell
macs3 callpeak \ #General purpose peak calling mode
-t ${treatment_frag} \ #Treatment file, can provide more than one to "pool"
-c ${input_frag} \ #Control File/Input
-f BAMPE \ #Instructs MACS2 on what kind of file to expect. Single/Paired-end bed/bam
-g hs \ #Sets appropriate genome size for background sampling hs=human, mm=humouse
-n ${name} \ #name
#-q 0.05 #FDR q value default
#-broad #"broad mode" for broad marks - stitches small peaks together
--outdir ~/workspace/peaks/ \ #where to output files otherwise stores in current working directory
--bdg \ #outputs pileup into bedgraphs
1> ~/workspace/peaks/${name}.out.log \ #output log
2>  ~/workspace/peaks/${name}.err.log #error log
```
##### Comments:
```Shell
List for common marks but is not exhaustive. Best practice would be to observe trends on genome browser and then decide.
Narrow Marks:
H3K27ac
H3K4me3

Broad Marks:
H3K27me3
H3K4me1
H3K36me3
H3K36me2
H3K9me3
```
##### Output:
##### <i>See logs</i>

### <B>2 Black list removal/Inspection </B>
- #### <B>2.1 Black list removal</B>
##### Code:
```Shell
blacklist=~/CourseData/EPI_data/Module1/QC_resources/hg38_blacklist.bed
sample="MCF10A_H3K27ac_peaks"
bedtools intersect -v -a ~/workspace/peaks/${sample}.narrowPeak -b ${blacklist} > ~/workspace/peaks/${sample}.blacklistRemoved.narrowPeak
bedtools intersect -u -a ~/workspace/peaks/${sample}.narrowPeak -b ${blacklist} > ~/workspace/peaks/${sample}.blacklist.narrowPeak
```
##### Output:
##### <i>See log</i>

- #### <B>2.2 NarrowPeak inspection</B>
##### Code:

```Shell
sample="MCF10A_H3K27ac_peaks"
wc -l ~/workspace/peaks/${sample}.blacklistRemoved.narrowPeak
head ~/workspace/peaks/${sample}.blacklistRemoved.narrowPeak -n5
```
##### Output:
```Shell
32384 /home/ubuntu/workspace/peaks/MCF10A_H3K27ac_peaks.blacklistRemoved.narrowPeak
chr1    10003   10467   MCF10A_H3K27ac_peak_1   2160    .       47.2436 221.596 216.028 179
chr1    17283   17514   MCF10A_H3K27ac_peak_2   27      .       3.9983  5.1706  2.76136 82
chr1    180312  180997  MCF10A_H3K27ac_peak_3   803     .       28.8766 85.1306 80.3433 461
chr1    777953  778720  MCF10A_H3K27ac_peak_4   210     .       10.1154 24.4429 21.0334 503
chr1    778984  779223  MCF10A_H3K27ac_peak_5   44      .       4.87285 7.00538 4.45379 69

```
##### Comments:
```Shell
chromosome name
peak start
peak stop
peak name
int(-10*log10pvalue)
N/A
Fold change at peak summit
-log10 P-value at Peak
-log10 Q-value at Peak
Summit position relative to peak
```


- #### <B>2.3 Quality control via % of reads in key genomic areas</B>
##### Code:

```Shell
sample="MCF10A_H3K27ac"
query_bam=~/CourseData/EPI_data/Module1/MCF10A_resources/${sample}.bam
samtools view -@4 -q 10 -F 1028 $query_bam -c
samtools view -@4 -q 10 -F 1028 $query_bam -L ~/CourseData/EPI_data/Module1/QC_resources/encode_enhancers_liftover.bed -c
samtools view -@4 -q 10 -F 1028 $query_bam -L ~/workspace/peaks/${sample}_peaks.blacklistRemoved.narrowPeak -c
```
##### Output:
```Shell
19632094
10752392
2028377

```
##### Comments:

```Shell
samtools view #Viewing entirety or subset of BAM file
-q 10 \ #Parsing for reads with 5>=MAPQ
-F 1028 \ # Remove reads that have the following flags:UNMAP,DUP #https://broadinstitute.github.io/picard/explain-flags.html
$query_bam \ # Bam of interest
-c # Count number of reads instead of displaying
-L # Region of interest. Bed File
```

##### Enrichment at key regions:

| |H3K4me1|H3K27me3|H3K27ac|H3K4me3|
|--|--|--|--|--|
|Reads Count|||||
|Total| 71,545,746 | 55,438,916 | 19,632,094| 26,381,511 |
|Enhancer| 48,466,245 | 25,742,977 | 10,752,392 | 12,302,265 |
|HOX| 13,866 | 13,085 | 4,504 | 28,674 |
|TSS| 7,303,584 | 5,111,631 | 2,702,194 | 18,041,080 |
|In Peaks|27,539,876|25,072,097|2,028,377|20,920,281|
||||||
||||||
||H3K4me1|H3K27me3|H3K27ac|H3K4me3|
|Percent of Total|||||
|Total|100.00|100.00|100.00|100.00|
|Enhancer|67.74|46.43|54.77|46.63|
|HOX|0.02|0.02|0.02|0.11|
|TSS|10.21|9.22|13.76|68.39|
|In Peaks|38.49|45.22|10.33|79.30|

###  <B>3. Visualization </B>

- #### <B>3.1  Visualization (Coverage)</B>
##### Code:
```Shell
mkdir -p ~/workspace/{bigBed,bigWig}
sample="MCF10A_H3K27ac"
input_bedgraph=~/workspace/peaks/${sample}_treat_pileup.bdg
output_bigwig=~/workspace/bigWig/${sample}_treat_pileup.bw
chrom_sizes=~/CourseData/EPI_data/Module1/QC_resources/hg38.chrom.sizes
sort -k1,1 -k2,2n ${input_bedgraph} > ~/workspace/bigWig/tmp
bedGraphToBigWig ~/workspace/bigWig/tmp ${chrom_sizes} ${output_bigwig}
rm ~/workspace/bigWig/tmp
```

```Shell
input_bedgraph=~/workspace/peaks/${sample}_control_lambda.bdg
output_bigwig=~/workspace/bigWig/${sample}_control_lambda.bw
chrom_sizes=~/CourseData/EPI_data/Module1/QC_resources/hg38.chrom.sizes
sort -k1,1 -k2,2n ${input_bedgraph} > ~/workspace/bigWig/tmp
bedGraphToBigWig ~/workspace/bigWig/tmp ${chrom_sizes} ${output_bigwig}
rm ~/workspace/bigWig/tmp
```

##### Output:
##### <i>N/A</i>

##### Code Breakdown:
```Shell
mkdir -p ~/workspace/{bigBed,bigWig}
sample="MCF10A_H3K27ac" # Specify variables
input_bedgraph=~/workspace/peaks/${sample}_treat_pileup.bdg #
output_bigwig=~/workspace/bigWig/${sample}_treat_pileup.bw #
chrom_sizes=~/CourseData/EPI_data/Module1/QC_resources/hg38.chrom.sizes #
sort -k1,1 -k2,2n ${input_bedgraph} > ~/workspace/bigWig/tmp  # Sorts peaks as to match alphabetical order in col 1 and numerical in col 2 #$(chrom_sizes) into a temporary file
bedGraphToBigWig ~/workspace/bigWig/tmp ${chrom_sizes} ${output_bigwig} # Conversion step
rm ~/workspace/bigWig/tmp #remove temporary file
```

- #### <B>3.2  Visualization (Peaks)</B>
##### Code:
```Shell
mkdir -p ~/workspace/{bigBed,bigWig}
sample="MCF10A_H3K27ac"
input_bed=~/workspace/peaks/${sample}_peaks.blacklistRemoved.narrowPeak
output_bigbed=~/workspace/bigBed/${sample}_peaks.blacklistRemoved.bb
chrom_sizes=~/CourseData/EPI_data/Module1/QC_resources/hg38.chrom.sizes
cut -f1-3 ${input_bed} | sort -k1,1 -k2,2n  > ~/workspace/bigBed/tmp
bedToBigBed ~/workspace/bigBed/tmp ${chrom_sizes} ${output_bigbed}
rm ~/workspace/bigBed/tmp
```

##### Output:
##### <i>N/A</i>
##### Code Breakdown:

```Shell
sample="MCF10A_H3K27ac"
input_bed=~/workspace/peaks/${sample}_peaks.blacklistRemoved.narrowPeak
output_bigbed=~/workspace/bigBed/${sample}_peaks.blacklistRemoved.bb
chrom_sizes=~/CourseData/EPI_data/Module1/QC_resources/hg38.chrom.sizes
cut -f1-3 ${input_bed} | sort -k1,1 -k2,2n  > ~/workspace/bigBed/tmp
bedToBigBed ~/workspace/bigBed/tmp ${chrom_sizes} ${output_bigbed} # Largely the same as above, except we trim our narrowPeak file to just 3 columns
rm ~/workspace/bigBed/tmp
```

- ### <B>3.3 Visualization</B>
1. Download tracks via public url
2. Upload onto IGV
3. Explore!
##### Comments:

```Shell
Check out the provided regions!
Filtered out region due to intersect w/ blacklist
chr16:34,145,433-34,160,335
```
<img src="https://github.com/bioinformatics-ca/EPI_2021/blob/master/img/moduel1/blacklist.png?raw=true" width= 750 />

```Shell
Artifact region:
chr16:34514779-34732558
```

<img src="https://github.com/bioinformatics-ca/EPI_2021/blob/master/img/moduel1/artifact.png?raw=true" width= 750 />

```Shell
HOXA region:
chr7:26981738-27365875
```

<img src="https://github.com/bioinformatics-ca/EPI_2021/blob/master/img/moduel1/HOX.png?raw=true" width= 750 />

###  <B>4. Homework </B>
##### Comments:

```Shell
Try Running H3K27me3, H3K4me1 and H3K4me3 on your own! When running H3K27me3 and H3K4me1 note the comments and code breakdown of step 2
```

## <B>Cheat sheet </B>
***


#### <B>Dedup Bams</B>
##### Code:
<code style="background:black;color:black">
mkdir -p ~/workspace/peaks
for mark in H3K27ac H3K4me3 H3K27me3 H3K4me1 Input;
do
    bam=~/CourseData/EPI_data/Module1/MCF10A_resources/MCF10A_${mark}.bam
    dedup=~/workspace/peaks/MCF10A_${mark}.dedup.bam
    samtools view -@4 ${bam} -bh -q10 -F1028 -o ${dedup}
done 
</code>

#### <B>Peak Calling all the marks</B>
##### Code:
<code style="background:black;color:black">
input_frag=~/workspace/peaks/MCF10A_Input.dedup.bam
for narrow_mark in H3K27ac H3K4me3;
do
    treatment_frag=~/workspace/peaks/MCF10A_${narrow_mark}.dedup.bam
    macs3 callpeak -t ${treatment_frag} -c ${input_frag} -f BAMPE -g hs -n MCF10A_${narrow_mark} --keep-dup all --outdir ~/workspace/peaks/ --bdg 1> ~/workspace/peaks/${narrow_mark}.out.log 2> ~/workspace/peaks/${narrow_mark}.err.log 
done
for broad_mark in H3K4me1 H3K27me3;
do
    treatment_frag=~/workspace/peaks/MCF10A_${broad_mark}.dedup.bam
    macs3 callpeak -t ${treatment_frag} -c ${input_frag} -f BAMPE -g hs -n MCF10A_${broad_mark} --keep-dup all --outdir ~/workspace/peaks/ --bdg --broad 1> ~/workspace/peaks/${broad_mark}.out.log 2> ~/workspace/peaks/${broad_mark}.err.log 
done
</code>

#### <B>Blacklist Filtering all Peaks</B>
##### Code:
<code style="background:black;color:black">
blacklist=~/CourseData/EPI_data/Module1/QC_resources/hg38_blacklist.bed
for narrow_mark in H3K27ac H3K4me3;
do
    bedtools intersect -v -a ~/workspace/peaks/MCF10A_${narrow_mark}_peaks.narrowPeak -b ${blacklist} > ~/workspace/peaks/MCF10A_${narrow_mark}_peaks.blacklistRemoved.narrowPeak
    bedtools intersect -u -a ~/workspace/peaks/MCF10A_${narrow_mark}_peaks.narrowPeak -b ${blacklist} > ~/workspace/peaks/MCF10A_${narrow_mark}_peaks.blacklist.narrowPeak
done
for broad_mark in H3K4me1 H3K27me3;
do
    bedtools intersect -v -a ~/workspace/peaks/MCF10A_${broad_mark}_peaks.broadPeak -b ${blacklist} > ~/workspace/peaks/MCF10A_${broad_mark}_peaks.blacklistRemoved.broadPeak
    bedtools intersect -u -a ~/workspace/peaks/MCF10A_${broad_mark}_peaks.broadPeak -b ${blacklist} > ~/workspace/peaks/MCF10A_${broad_mark}_peaks.blacklist.broadPeak
done
</code>

#### <B>BigWig converting all your *treat_pileup.bdg</B>
##### Code:
<code style="background:black;color:black">
mkdir -p ~/workspace/{bigBed,bigWig}
chrom_sizes=~/CourseData/EPI_data/Module1/QC_resources/hg38.chrom.sizes
for mark in H3K27ac H3K4me3 H3K27me3 H3K4me1
do
    input_bedgraph=~/workspace/peaks/MCF10A_${mark}_treat_pileup.bdg
    output_bigwig=~/workspace/bigWig/MCF10A_${mark}_treat_pileup.bw
    sort -k1,1 -k2,2n ${input_bedgraph} > ~/workspace/bigWig/tmp
    bedGraphToBigWig ~/workspace/bigWig/tmp ${chrom_sizes} ${output_bigwig}
    rm ~/workspace/bigWig/tmp
done
</code>

<code style="background:black;color:black">
sample="MCF10A_H3K27ac"
input_bedgraph=~/workspace/peaks/${sample}_control_lambda.bdg
output_bigwig=~/workspace/bigWig/${sample}_control_lambda.bw
chrom_sizes=~/CourseData/EPI_data/Module1/QC_resources/hg38.chrom.sizes
sort -k1,1 -k2,2n ${input_bedgraph} > ~/workspace/bigWig/tmp
bedGraphToBigWig ~/workspace/bigWig/tmp ${chrom_sizes} ${output_bigwig}
rm ~/workspace/bigWig/tmp
</code>


#### <B>BigBed converting all your *Peaks</B>
##### Code:
<code style="background:black;color:black">
mkdir -p ~/workspace/{bigBed,bigWig}
chrom_sizes=~/CourseData/EPI_data/Module1/QC_resources/hg38.chrom.sizes
for narrow_mark in H3K27ac H3K4me3;
do
    input_bed=~/workspace/peaks/MCF10A_${narrow_mark}_peaks.blacklistRemoved.narrowPeak
    output_bigbed=~/workspace/bigBed/MCF10A_${narrow_mark}_peaks.blacklistRemoved.bb
    chrom_sizes=~/CourseData/EPI_data/Module1/QC_resources/hg38.chrom.sizes
    cut -f1-3 ${input_bed} | sort -k1,1 -k2,2n  > ~/workspace/bigBed/tmp
    bedToBigBed ~/workspace/bigBed/tmp ${chrom_sizes} ${output_bigbed}
done
for broad_mark in H3K4me1 H3K27me3;
do
    input_bed=~/workspace/peaks/MCF10A_${broad_mark}_peaks.blacklistRemoved.broadPeak
    output_bigbed=~/workspace/bigBed/MCF10A_${broad_mark}_peaks.blacklistRemoved.bb
    chrom_sizes=~/CourseData/EPI_data/Module1/QC_resources/hg38.chrom.sizes
    cut -f1-3 ${input_bed} | sort -k1,1 -k2,2n  > ~/workspace/bigBed/tmp
    bedToBigBed ~/workspace/bigBed/tmp ${chrom_sizes} ${output_bigbed}
done
</code>

#### <B>Total read counts per BAM</B>
##### Code:
<code style="background:black;color:black">
for narrow_mark in H3K27ac H3K4me3;
do
    bam=~/CourseData/EPI_data/Module1/MCF10A_resources/MCF10A_${narrow_mark}.bam
    peak=~/workspace/peaks/MCF10A_${narrow_mark}_peaks.blacklistRemoved.narrowPeak
    echo total reads in ${narrow_mark} $(samtools view -@4 ${bam} -q10 -F1028 -c )
done
for broad_mark in H3K4me1 H3K27me3;
do
    bam=~/CourseData/EPI_data/Module1/MCF10A_resources/MCF10A_${broad_mark}.bam
    peak=~/workspace/peaks/MCF10A_${broad_mark}_peaks.blacklistRemoved.narrowPeak
    echo total reads in ${broad_mark} $(samtools view -@4 ${bam} -bh -q10 -F1028 -c )
done
</code>

#### <B>Reads in Enriched region per BAM</B>
##### Code:
<code style="background:black;color:black">
for narrow_mark in H3K27ac H3K4me3;
do
    bam=~/CourseData/EPI_data/Module1/MCF10A_resources/MCF10A_${narrow_mark}.bam
    peak=~/workspace/peaks/MCF10A_${narrow_mark}_peaks.blacklistRemoved.narrowPeak
    echo enriched reads in ${narrow_mark} $(samtools view -@4 ${bam} -q10 -F1028 -c -L ${peak})
done
for broad_mark in H3K4me1 H3K27me3;
do
    bam=~/CourseData/EPI_data/Module1/MCF10A_resources/MCF10A_${broad_mark}.bam
    peak=~/workspace/peaks/MCF10A_${broad_mark}_peaks.blacklistRemoved.broadPeak
    echo enriched reads in ${broad_mark} $(samtools view -@4 ${bam} -bh -q10 -F1028 -c -L ${peak})
done
</code>

#### <B>Reads in Domain regions per BAM</B>
##### Code:
<code style="background:black;color:black">
for file in $(ls ~/CourseData/EPI_data/Module1/QC_resources/* | grep bed | grep -v blacklist);
do
    for bam in $(ls ~/CourseData/EPI_data/Module1/MCF10A_resources/*bam );
    do
        echo $(basename ${bam}) $(basename ${file}) $(samtools view -@4 -q 10 -F 1028 ${bam} -L $file -c )
    done
done
</code>

#### <B>Counts total peaks per file</B>
##### Code:
<code style="background:black;color:black">
for file in $(ls ~/workspace/peaks/*.blacklistRemoved.*Peak);
do
    wc -l $file
done
for file in $(ls ~/CourseData/EPI_data/Module1/CEEHRC_resources/*.bed);
do
    wc -l $file
done
</code>

#### <B>Counts total peaks per overlap</B>
##### Code:
<code style="background:black;color:black">
for histone_mark in H3K27ac H3K27me3 H3K4me3 H3K4me1;
do
    for fileA in $(ls ~/workspace/peaks/*${histone_mark}*.blacklistRemoved*Peak);
    do
        for fileB in $(ls ~/CourseData/EPI_data/Module1/CEEHRC_resources/*${histone_mark}*.bed);
        do
            echo $(basename $fileA) $(basename $fileB) AuB $(bedtools intersect -u -a $fileA -b $fileB | wc -l)
            echo $(basename $fileA) $(basename $fileB) A-B $(bedtools intersect -v -a $fileA -b $fileB | wc -l)
            echo $(basename $fileA) $(basename $fileB) B-A $(bedtools intersect -v -b $fileA -a $fileB | wc -l)
        done
    done
done
</code>