---
layout: tutorial_page
permalink: /EPI_2021_Module1_lab
title: EPI 2021 Module 1 Lab
header1: Workshop Pages for Students
header2: Introduction to ChIP-seq and analysis
image: /site_images/CBW_Epigenome-data_icon.jpg
home: https://bioinformaticsdotca.github.io/EPI_2021
description: Introduction to ChIP-seq and analysis
author: Martin Hirst and Edmund Su

---

# Introduction to ChIP-seq and analysis

*by Martin Hirst and Edmund Su*

# Table of contents:

<font size="5">[Common tools of the trade](#Common-tools-of-the-trade)</font>

<font size="5">[Module 1. Alignment](#Module-1.-BWA-Alignment-+-BAM-post-processing)</font>


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

## <B>Module 1. BWA Alignment + BAM post processing</B>
***

<div><input type="checkbox" name="chk" checked>1. Have a genome reference file ready (DONE)</div>
<div><input type="checkbox" name="uchk" checked>2. Index genome reference file (DONE)</div>
<div><input type="checkbox" name="uchk">3. Run quality Check</div>
<div><input type="checkbox" name="uchk">4. Run alignment</div>
<div><input type="checkbox" name="uchk">5. Coordinate Sort alignment File</div>
<div><input type="checkbox" name="uchk">6. Duplicate marking alignment</div>
<div><input type="checkbox" name="uchk">7. Flagstats</div>
<div><input type="checkbox" name="uchk">7. Clean up</div>


### <B>Setup</B>
```Shell
mkdir ~/workspace/{alignments,fastqc}
```
### <B>1. (DONE) Make a reference directory and download appropriate fasta reference @ https://hgdownload.cse.ucsc.edu/goldenpath/ (https://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/hg38.fa.gz)</B>
##### Code:
<code style="background:black;color:black">
mkdir ~/CourseData/BWA_index
wget https://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/hg38.fa.gz -O ~/CourseData/BWA_index/
gunzip ~/CourseData/EPI_data/Module1/BWA_index/hg38.fa.gz
</code>

### <B>2. (DONE) Index Fasta using BWA </B>
##### Code:
<code style="background:black;color:black">
bwa index ~/CourseData/EPI_data/Module1/BWA_index/chr19.hg38_no_alt.fa
ls ~/CourseData/EPI_data/Module1/BWA_index/ -lth
</code>

##### Output:
```Shell
total 155M
8126488 -rw-rw-r-- 1 ubuntu ubuntu 28M Sep  7 19:22 chr19.hg38_no_alt.fa.sa
8126486 -rw-rw-r-- 1 ubuntu ubuntu 108 Sep  7 19:22 chr19.hg38_no_alt.fa.amb
8126485 -rw-rw-r-- 1 ubuntu ubuntu 153 Sep  7 19:22 chr19.hg38_no_alt.fa.ann
8126484 -rw-rw-r-- 1 ubuntu ubuntu 14M Sep  7 19:22 chr19.hg38_no_alt.fa.pac
8126487 -rw-rw-r-- 1 ubuntu ubuntu 56M Sep  7 19:22 chr19.hg38_no_alt.fa.bwt
8126483 -rw-rw-r-- 1 ubuntu ubuntu 57M Sep  7 18:36 chr19.hg38_no_alt.fa
```

### <B>3. Run quality Check</B>
##### Code:
```Shell
mkdir -p ~/workspace/fastqc
fastq_file_A=~/CourseData/EPI_data/Module1/MCF10A_resources/R1_input.fastq.gz
fastq_file_B=~/CourseData/EPI_data/Module1/MCF10A_resources/R1_h3k27ac.fastq.gz
fastqc ${fastq_file_A} -o ~/workspace/fastqc
fastqc ${fastq_file_B} -o ~/workspace/fastqc
```

##### Output:
```Shell
Started analysis of R1_input.fastq.gz
Approx 5% complete for R1_input.fastq.gz
Approx 10% complete for R1_input.fastq.gz
Approx 15% complete for R1_input.fastq.gz
Approx 20% complete for R1_input.fastq.gz
Approx 25% complete for R1_input.fastq.gz
Approx 30% complete for R1_input.fastq.gz
Approx 35% complete for R1_input.fastq.gz
Approx 40% complete for R1_input.fastq.gz
Approx 45% complete for R1_input.fastq.gz
Approx 50% complete for R1_input.fastq.gz
Approx 55% complete for R1_input.fastq.gz
Approx 60% complete for R1_input.fastq.gz
Approx 65% complete for R1_input.fastq.gz
Approx 70% complete for R1_input.fastq.gz
Approx 75% complete for R1_input.fastq.gz
Approx 80% complete for R1_input.fastq.gz
Approx 85% complete for R1_input.fastq.gz
Approx 90% complete for R1_input.fastq.gz
Approx 95% complete for R1_input.fastq.gz
Analysis complete for R1_input.fastq.gz
```

##### Comment:
```Shell
Check out the HTML file produced!
Note the GC distribution of Input VS H3K27ac
```
##### Input

<img src="https://github.com/bioinformatics-ca/EPI_2021/blob/master/img/moduel1/input.png?raw=true" width= 750 />

##### H3K27ac
<img src="https://github.com/bioinformatics-ca/EPI_2021/blob/master/img/moduel1/h3k27ac.png?raw=true" width= 750 />

### <B>4. Run alignment</B>
##### Code:
```Shell
mkdir -p ~/workspace/alignments
ref=~/CourseData/EPI_data/Module1/BWA_index/chr19.hg38_no_alt.fa
read1=~/CourseData/EPI_data/Module1/MCF10A_resources/R1_input.fastq.gz
read2=~/CourseData/EPI_data/Module1/MCF10A_resources/R2_input.fastq.gz
sample=MCF10A_input_chr19
bwa mem -M -t 2 ${ref} ${read1} ${read2} 2>~/workspace/alignments/alignment.log | samtools view -hbS -o ~/workspace/alignments/${sample}.bam
```
##### Output:
##### <i>Check log</i>
##### Code Breakdown:

```Shell
mkdir -p ~/workspace/alignments # Make working directory
ref=~/CourseData/EPI_data/Module1/BWA_index/chr19.hg38_no_alt.fa # Preset set variables
read1=~/CourseData/EPI_data/Module1/MCF10A_resources/R1_input.fastq.gz
read2=~/CourseData/EPI_data/Module1/MCF10A_resources/R2_input.fastq.gz
sample=MCF10A_input_chr19

bwa mem -M -t 2 ${ref} ${read1} ${read2} 2>~/workspace/alignments/alignment.log # Alignment step {"-t 2":Peform alignment using two threads,"-M":mark short split hits as secondary}
| samtools view -hbS -o ~/workspace/alignments/${sample}.bam # Converts SAM to BAM format {"h":Include Header, "b": output BAM, "S":detect input format}
```
### <B>5. Coordinate Sort alignment File</B>
##### Code:
```Shell
sample=MCF10A_input_chr19
samtools sort  ~/workspace/alignments/${sample}.bam -o ~/workspace/alignments/${sample}.sorted.bam
```
##### Output:
##### <i>N/A</i>
##### Code Breakdown:
```Shell
Coordinate sorts
```
##### Comment:
```Shell
Take a look at the coordinate sorted bam vs original.
```

### <B>6. Duplicate marking alignment</B>
##### Code:
```Shell
sample=MCF10A_input_chr19
java -jar /usr/local/picard/picard.jar MarkDuplicates I=~/workspace/alignments/${sample}.sorted.bam O=~/workspace/alignments/${sample}.dup_marked.sorted.bam M=~/workspace/alignments/${sample}.dup_marked.output.log ASSUME_SORTED=TRUE VALIDATION_STRINGENCY=LENIENT > ~/workspace/alignments/${sample}.dup_marked.error.log
```
##### Code Breakdown:

```Shell
java -jar \ # Requires java to intepret
/usr/local/picard/picard.jar \ #Point to toolkit
MarkDuplicates \  #Specify function from toolkit
I=~/workspace/alignments/${sample}.sorted.bam \ #Input
O=~/workspace/alignments/${sample}.dup_marked.sorted.bam \ #output
M=~/workspace/alignments/${sample}.dup_marked.output.log \ #Work log
ASSUME_SORTED=TRUE \ #B/C we already sorted this will be true
VALIDATION_STRINGENCY=LENIENT \ #Emit warnings but keep going if possible
> ~/workspace/alignments/{sample}.dup_marked.error.log
```
##### Output:
##### <i>See log</i>

### <B>7. Flagstats</B>
##### Code:
```Shell
sample=MCF10A_input_chr19
samtools flagstat ~/workspace/alignments/${sample}.dup_marked.sorted.bam > ~/workspace/alignments/${sample}.dup_marked.sorted.flagstat
```
##### Output:
```Shell
1726243 + 0 in total (QC-passed reads + QC-failed reads)
34545 + 0 secondary
0 + 0 supplementary
64636 + 0 duplicates
1545613 + 0 mapped (89.54% : N/A)
1691698 + 0 paired in sequencing
845849 + 0 read1
845849 + 0 read2
1192976 + 0 properly paired (70.52% : N/A)
1330944 + 0 with itself and mate mapped
180124 + 0 singletons (10.65% : N/A)
0 + 0 with mate mapped to a different chr
0 + 0 with mate mapped to a different chr (mapQ>=5)
```

##### Comment:
```Shell
Run flagstat on MCF10A_input_chr19.sorted.bam. What are the differences?
Try running the alignment with MCF10A_H3K27ac_chr19!
```

### <B>8. Clean up!</B>
##### Code:
```Shell
rm ~/workspace/alignments/${sample}.sorted.bam
rm ~/workspace/alignments/${sample}.bam
```
##### Comment:
```Shell
Good practice to remove redundant files
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
