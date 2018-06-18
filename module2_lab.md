---
layout: tutorial_page
permalink: /epigenomics_2018_module2_lab
title: Epigenomics Lab 2
header1: Workshop Pages for Students
header2: Epigenomic Data Analysis 2018 Module 2 Lab
image: /site_images/CBW_Epigenome-data_icon.jpg
home: https://bioinformaticsdotca.github.io/epigenomics_2018
---

# Module 2 Lab: ChIP-Seq Alignment, Peak Calling (Enrichment Regions Detection), and Visualisation

By Misha Bilenky

1. Set up some useful variables etc...
```
source /home/partage/epigenomics/chip-seq/setup.sh
```
You will see on the screen: 
```
**** setting useful stuff
```
you can see what variables we defined by
```
less /home/partage/epigenomics/chip-seq/setup.sh
```
2. Create your personal working directory;
For example, I create my own working space:

```
out=/home/partage/epigenomics/chip-seq/H1test
mkdir -p $out
cd $out
```
We will perform alignment of small fastq file (H1 cells, H3K27ac ChIP-seq) to the human reference hg19

Fastq file is located in `/home/partage/epigenomics/chip-seq/H1/data/H3K27ac`  
```
echo "$H1data"
ls -l $H1data/H3K27ac/H3K27ac.H1.fastq.gz
```
It is a very small region of genome on chr3
~50K reads.

```
less $H1data/H3K27ac/H3K27ac.H1.fastq.gz | head -40
```

3. Human genome is stored in the variable
```
echo $hg19
ls -l $hg19
```
```
less $hg19/Homo_sapiens.hg19.fa | head -1
```
we see first chromosome.
To see what are sequence names (line starting with ">") you can use, e.g. command:

`less $hg19/Homo_sapiens.hg19.fa | awk '/>/' `

To see the human genome sequence:
```
less $hg19/Homo_sapiens.hg19.fa | head -250
```
Sequence starts with a stretch of'NNN..' at the begining and then DNA letters in lower (masked) and upper case.

4. BWA: alignment.
Lets check that we have bwa installed
```
which bwa
bwa
```

Run first step, "bwa aln"
```
bwa aln $hg19/Homo_sapiens.hg19.fa $H1data/H3K27ac/H3K27ac.H1.fastq.gz > H3K27ac.H1.sai
```

small delay at the start as genome was beeing loaded...
We should see a .sai file
```
ls -l
```
The .sai file is an intermediate file containing the suffix array indexes. Such file is afterwards translated into a SAM file.

NOTE: if we align data from pair-end experiment we need to do alignment of both read1 and read2

bwa aln <genome> read1.fastq > read1.sai
bwa aln <genome> read1.fastq > read2.sai

5. BWA: translation of suffix index file into SAM
```
bwa samse -f H3K27ac.H1.sam $hg19/Homo_sapiens.hg19.fa H3K27ac.H1.sai $H1data/H3K27ac/H3K27ac.H1.fastq.gz
```
See that sam file is there
```
ls -l
more H3K27ac.H1.sam | head -200
```

6. Now using "samtools" to manipulate SAM file

First see that you can easily get samtools help:
```
samtools
samtools view
```

Convert into binary BAM file:
```
samtools view -Sb H3K27ac.H1.sam > H3K27ac.H1.bam
```
Position sort:
```
samtools sort H3K27ac.H1.bam H3K27ac.H1.sorted
```
NOTE: if we use option '-n' in "samtools sort" file will be name sorted. Useful for pair-end data; then two reads from the pair are next to each other in the file.

Check:
``` 
ls -lh
```
You will see on the screen something like
```
-rw-r--r-- 1 stud02 abcd 2.1M Jun 17 20:43 H3K27ac.H1.bam
-rw-r--r-- 1 stud02 abcd 1.8M Jun 17 20:05 H3K27ac.H1.sai
-rw-r--r-- 1 stud02 abcd 7.1M Jun 17 20:06 H3K27ac.H1.sam
-rw-r--r-- 1 stud02 abcd 2.1M Jun 17 20:43 H3K27ac.H1.sorted.bam
```
You see that "BAM" file is ~4-5 times smaller than "SAM"

7. Lets look into alignment file:
File has a header (use "-H" flag)
```
samtools view -H H3K27ac.H1.sorted.bam | more
```
and the aliggned/unuligned reads information
```
samtools view H3K27ac.H1.sorted.bam | head
```
[all fields we discussed]

8. Using BAM file we can obtain useful informtion just using "samtools" and counting number of lines:
```
samtools view H3K27ac.H1.sorted.bam | wc -l
```
49990

Filtering unaligned reads:
```
samtools view -F 4 H3K27ac.H1.sorted.bam | wc -l
```
31555

Now filtering on mapping quality:
```
samtools view -F 4 -q 5 H3K27ac.H1.sorted.bam | wc -l
```
27735
Aligned and filtered reads containing "TATA" sequence:
```
samtools view -F 4 -q 5 H3K27ac.H1.sorted.bam | cut -f10 | grep TATA | wc -l
```
2178
Longer "TATAA" sequence:
```
samtools view -F 4 -q 5 H3K27ac.H1.sorted.bam | cut -f10 | grep TATAA | wc -l
```
718

9. Marking duplicated reads

```
echo "$picard"

java -jar $picard/MarkDuplicates.jar I=H3K27ac.H1.sorted.bam O=H3K27ac.H1.sorted.dupsMarked.bam M=dups AS=true VALIDATION_STRINGENCY=LENIENT QUIET=true
```

You should have H3K27ac.H1.sorted.dupsMarked.bam file in your directory.

```
samtools view -F 1028 -q 5 H3K27ac.H1.sorted.dupsMarked.bam | wc -l
```
25902

Useful "samtools" option (showing flag in the user friendly format) [ also remeber useful website:
https://broadinstitute.github.io/picard/explain-flags.html]
```
samtools view -X  H3K27ac.H1.sorted.dupsMarked.bam | more
```
shows second field ("SAM flag") in a human readable format.

10. Lets count reads aligned to (+) and (-) strands. Reverse strand flag is '16': 
"-f 16" - accept (-) only
"-F 16" - exclude (-) strand  [accept (+) strand only]
```
samtools view -X -F 20 H3K27ac.H1.sorted.dupsMarked.bam | wc -l
```
15995
```
samtools view -X -f16 H3K27ac.H1.sorted.dupsMarked.bam | wc -l
```
15560

Looks very reasonable: counts of (+) and (-) reads are very close

11. BAM file statistics:
```
samtools flagstat H3K27ac.H1.sorted.dupsMarked.bam > H3K27ac.H1.sorted.dupsMarked.bam.flagstat
```
check the output
```
more H3K27ac.H1.sorted.dupsMarked.bam.flagstat
```
you should see alignments file details:
```
[lect02@workshop103 H1test]$ less H3K27ac.H1.sorted.dupsMarked.bam.flagstat | more
49990 + 0 in total (QC-passed reads + QC-failed reads)
1854 + 0 duplicates
31555 + 0 mapped (63.12%:-nan%)
0 + 0 paired in sequencing
0 + 0 read1
0 + 0 read2
0 + 0 properly paired (-nan%:-nan%)
0 + 0 with itself and mate mapped
0 + 0 singletons (-nan%:-nan%)
0 + 0 with mate mapped to a different chr
0 + 0 with mate mapped to a different chr (mapQ>=5)
```

Lest do the same with "sambamba". Type
```
sambamba flagstat
```
to see help.
```
sambamba flagstat H3K27ac.H1.sorted.dupsMarked.bam 

49990 + 0 in total (QC-passed reads + QC-failed reads)
0 + 0 secondary
0 + 0 supplementary
1854 + 0 duplicates
31555 + 0 mapped (63.12%:N/A)
0 + 0 paired in sequencing
0 + 0 read1
0 + 0 read2
0 + 0 properly paired (N/A:N/A)
0 + 0 with itself and mate mapped
0 + 0 singletons (N/A:N/A)
0 + 0 with mate mapped to a different chr
0 + 0 with mate mapped to a different chr (mapQ>=5)
```
Gives the same info as samtools. In "sambamba" we can use multi-threading by adding "-t <n-threads>" flag which is significantly speeds up the execution.

12. Indenxing BAM file
```
samtools index H3K27ac.H1.sorted.dupsMarked.bam
```
(or "sambamba index")

Now we ask some interesting questions:

How may H3K27ac reads fall into promoter of a gene? (TSS+/-2Kb)

"TCAIM" gene  (T_cell_activation_inhibitor_mitochondrial), location chr3:44,379,611-44,401,294, (+) strand

TSS+/-2Kb (take start coordinate +2000 and -2000 region)

chr3:44377611-44381611
```
samtools view -q 5 -F 1028 H3K27ac.H1.sorted.dupsMarked.bam chr3:44377611-44381611 | wc -l
```
431

We just attached region's coordinates at the end of the "samtools view"command.
There is definetely some ChIP-seq signal.

Another gene just upstream 

TOPAZ1, location chr3:44,283,378-44,373,590 

TSS+/-2Kb:

chr3:44281378-44285378
```
samtools view -q 5 -F 1028 H3K27ac.H1.sorted.dupsMarked.bam chr3:44281378-44285378 | wc -l
```
30

Much less reads in the promoter of this gene...

... and some random 4Kb regions
```
samtools view -q 5 -F 1028 H3K27ac.H1.sorted.dupsMarked.bam chr3:44271378-44275378 | wc -l
```
10
```
samtools view -q 5 -F 1028 H3K27ac.H1.sorted.dupsMarked.bam chr3:44261378-44265378 | wc -l
```
26

Thus we can conclude that we see two genes - one has a strong H3K27ac signal and another does not.

We can define a file containing locations (e.g. regions)

chr3:44377611-44381611

chr3:44281378-44285378

chr3:44271378-44275378

chr3:44261378-44265378

and see number of reads falling into all those regions

13. Visualization @ UCSC, generating WIG file.  
Filtering:  
1. accepting only reads qith mapping quality >5 "-q 5"  
2. collapsing duplicated reads (flag 1024) and rejecting unmapped reads (flag 4) -F 1024+4 -->"-F 1028"   
3. Using CiP-seq single end option of BAM2WIG with directionl read extension by 150bp: "-cs -x 150"  

```
samtools=/cvmfs/soft.mugqic/CentOS6/software/samtools/samtools-0.1.19/samtools
java -jar -Xmx2G $bin/BAM2WIG.jar -bamFile H3K27ac.H1.sorted.dupsMarked.bam -out $out -q 5 -F 1028 -cs -x 150 -samtools $samtools
```

what you see on the screen:

```
[lect02@workshop103 H1test]$ java -jar -Xmx2G $bin/BAM2WIG.jar -bamFile H3K27ac.H1.sorted.dupsMarked.bam -out /home/partage/epigenomics/chip-seq/H1test -q 5 -F 1028 -cs -x 150 -samtools /cvmfs/soft.mugqic/CentOS6/software/samtools/samtools-0.1.19/samtools
**** v. 0.9.8
$Id: BAM2WIG.java 120350 2016-06-04 01:27:29Z mbilenky $
Reading BAM file: H3K27ac.H1.sorted.dupsMarked.bam
Output WIG file into: /home/partage/epigenomics/chip-seq/H1test
Reading the header...
/cvmfs/soft.mugqic/CentOS6/software/samtools/samtools-0.1.19/samtools view -H -q 5 -F 1028 H3K27ac.H1.sorted.dupsMarked.bam
Read lengths for 93 chromosomes
ChIP-seq, SET, read extension xset=150
Start analysis...

Parsing H3K27ac.H1.sorted.dupsMarked.bam
/cvmfs/soft.mugqic/CentOS6/software/samtools/samtools-0.1.19/samtools view -X -q 5 -F 1028 H3K27ac.H1.sorted.dupsMarked.bam
.
Reads: total=25902
```

14. Check the WIG file

```
less H3K27ac.H1.sorted.dupsMarked.q5.F1028.SET_150.wig.gz
```







