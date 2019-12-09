#### Assemble and annotate a chloroplast genome

##### What is genome assembly?

* Genome assembly is the process of joining together DNA sequencing fragments into longer pieces, ideally up to chromosome lengths.
* The DNA fragments are produced by DNA sequencing machines, and are called "reads". These are in lengths of about 150 base pairs, to up to a million (or more) base pairs, depending on the sequencing technology used. Currently, most reads are from Illumina (short), PacBio (long) or Oxford Nanopore (long and extra-long).
* It is difficult to assemble plant genomes as they are often large (for example, 3,000,000,000 base pairs), have many repeat regions (such as transposons), and may be polyploid.
* This tutorial shows genome assembly for a smaller data set - the plant chloroplast genome - a circular chromosome about 160,000 base pairs long.
* The process shown here is applicable to assembling plant nuclear genomes but there would be extra steps (and much more time) involved. For example, additional sequencing would usually be run on 10X, BioNano or HiC to produce information to link up longer nuclear chromosome pieces and to separate out the maternal and paternal haplotypes.

##### Tutorial overview

* The chloroplast genome of the sweet potato has been sequenced.
* This has produced many sequencing reads - DNA fragments.
* We will try to join these reads together to make the whole chloroplast genome sequence.
* We will use the Galaxy Australia platform (a web page) to run our analysis.
* This tutorial assumes some familiarity with Galaxy and bioinformatics - if you are new to either of these, we recommend the [Galaxy Australia Training](https://galaxy-au-training.github.io/tutorials/) tutorials *Get started, Learn key tasks, Quality control, Genome assembly, *and* Genome annotation*.

##### Import the data

* Log in to [Galaxy Australia](https://usegalaxy.org.au/) and create a new history.
* The data is from this paper: [Zhou C, Duarte T, Silvestre R et al. 2018](https://doi.org/10.12688/gatesopenres.12856.1), hosted at EBI ENA.
<!--How I got these files: see text at end of this document -->
* Original FASTQ reads: Illumina (SRR6828568) and Nanopore (SRR6828567).
* These data sets have been highly reduced in size for this tutorial.
* In a new browser tab, go to this webpage [at this link](http://doi.org/10.5281/zenodo.3567224).
* Find the file called <fn>sweet-potato-chloroplast-illumina-reduced.fastq</fn>
* Right click on file name: select "copy link address"
* In Galaxy, go to <ss>Get Data</ss> and then <ss>Upload File</ss>
* Click <ss>Paste/Fetch data</ss>
* A box will appear: paste in link address
* Click <ss>Start</ss>; click <ss>Close</ss>
* The file will now appear in the top of your history panel.
* Repeat for the Nanopore reads <fn>sweet-potato-chloroplast-nanopore-reduced.fastq</fn>.
* We now have two FASTQ read files in our history.
* Click on the eye icon next to one of the FASTQ sequence files.
* View the file in the centre Galaxy panel.

##### Look at the read quality [to do]

* In the tool panel, search for Nanoplot
* [to do - run details] [to do - results] what does it mean, see sweet potato nanoplot - why is weighted histogram of read lengths have some that are in negative?/ eg NanoStats / average read length = 7000 / av quality = 10 / 2000 reads / 13 million bases

##### Assemble the nanopore reads

* In the tool panel, search for "flye", and click on "Assembly of long and error-prone reads".
* For <ss>Input reads</ss> select <fn>sweet-potato-chloroplast-nanopore-reduced.fastq</fn>
* Leave other settings as default, except for <ss>estimated genome size</ss> add <fn>160000</fn>
* Click <ss>Execute</ss>

##### View assembly outputs

* There are five output files.
* View the <fn>log</fn> file and scroll to the end. How many contigs were assembled? What is the length of the assembly?
* View the <fn>assembly_info</fn> file. What are the contig names? What does the "graph_path" show? <!-- that contig 2 has inverted repeats -->
* The assembly sequence is in the <fn>scaffolds</fn>. Re-name this <fn>flye-assembly.fasta</fn>
* Optional: Download the <fn>Graphical Fragment Assembly</fn>
* Open the Bandage program (add link).
* Go to <ss>File: load graph</ss> then <ss>Draw graph</ss>
* What is your interpretation of this assembly graph?
<!--
It looks like the LSC and SSC fragments are joined by a collapsed repeat (the inverted repeat)
-->
![assembly graph](images/flye-assembly-graph.png)
[to do - check the lengths of these graph contigs match the lengths in the flye output files]
[to do - check the contig naming - note that it is changed in bandage?]

##### Map short reads to the aseembly

* Short illumina reads are more accurate the nanopore reads. We will use them to correct errors in the nanopore assembly.
* The first step is to map the reads to the assembly.
* In the tool panel, search for "bwa mem", and click on "Map with BWA-MEM"
* For <ss>Will you select a reference genome from your history</ss> select <fn>Use a genome from history</fn>
* For <ss>Use the following dataset as the reference sequence</ss> select <fn>flye-assembly.fasta</fn>
* For <ss>Algorithm for constructing the BWT index</ss> select <fn>Auto. Let BWA decide</fn>
* For <ss>Single or Paired-end reads</ss> select <fn>Single</fn>
* For <ss>Select fastq dataset</ss> select <fn>sweet-potato-chloroplast-illumina-reduced.fastq</fn>
* For <ss>Set read groups information?</ss> select <fn>Do not set</fn>
* For <ss>Select analysis mode</ss> select <fn>1. Simple Illumina mode</ss>
* Click <ss>Execute</ss>
* This maps the short reads to the assembly, and creates an alignment file.
* Re-name this file <fn>illumina.bam</fn>

##### Polish the assembly

* In the tool panel, search for "pilon", and click on "pilon"
* For <ss>Source for reference genome used for BAM alignments</ss> select <fn>Use a genome from history</fn>
* For <ss>Select a reference genome</ss> select <fn>flye-assembly.fasta</fn>
* For <ss>Type automatically determined by pilon</ss> click <fn>Yes</fn>
* For <ss>Input BAM file</ss> select <fn>illumina.bam</fn>
* For <ss>Variant calling mode</ss> select <fn>No</fn>
* For <ss>Create changes file</ss> select <fn>Yes</fn>
* Click <ss>Execute</ss>
* This compares the short reads to the assembly, and creates a polished (corrected) assembly file.
<!-- option: run a second round of polishing. keep track of file naming, and will need to generate a new bam [map illumina reads to polished.fasta] -->
* Re-name the fasta output file <fn>polished.fasta</fn>
* Find and run the tool called "Fasta statistics" on this file.
* How does it compare to the unpolished <fn>flye-assembly.fasta</fn>?
<!-- length 161333 compared to unpolished 160340; about 1k bases have been added back in; nanopore can have a lot of homopolymer deletions; the changes file shows lots of cases with a deletion changing to a base, there are also stretches of bases replaced-->


##### View read alignments

Get cutdown nano and illumina reads for viewing in bams

View all histories: see History: chloroplast-tutorial-data - drag sweet-potato-nanopore-tiny.fastq and sweet-potato-illumina-tiny.fastq
click Analyze Data

Map tiny nano to polished.fasta with bwa-mem

bwa mem
single reads
analysis: nano mode
=> bam
re-name as nanopore-tiny.bam

map tiny illumina to polished.fasta with bwa-mem

bwa mem
single reads
analysis: illumina mode
=> bam
re-name as illumina-tiny.bam

JBrowse on polished.fasta and nano-bam and illumina-bam

ref = polished.fasta
genetic code = 11

Insert Track Group

Insert Annotation Track
Track type: BAM pileups
BAM track data: nanopore-tiny.bam

Insert Annotation Track
Track type: BAM pileups
BAM track data: illumina-tiny.bam

=> JBrowse. re-name: e.g. view flye.fasta and seq reads

Two contigs in drop down.
zoom all the way out
zoom all the way in
change ref seq display.
see diffs bn long error nano reads and short low-error illumina reads

note that the coverage is quite uneven, but that these reads could have bias as they are those that mapped to a certain set of cp genomes. If this new genome has new bits, these may be in the long-read assembly but missing in short reads.

Why would the polished assembly (the ref track) be different to the reads - wouldn't these snps correct these places? maybe would need another round+ of polishing.


##### Annotate

* Annotation is ....

download the polished.fasta
https://chlorobox.mpimp-golm.mpg.de/geseq.html
web: geseq: upload the fasta file.
linear
options: generate codon-based alignments
Blat - default
hmmer - tick emrbyophyta
argaron tick
tRNAscan - tick
accept disclaimer
submit: (5 mins): tutorial break

contigA: gff3: click on it: click download at the bottom
contigB: repeat

click on ogdraw to look
[Note: can see the repeated 16sRNA and 23sRNA -- although one of sets only has fragments? not full length? -- also, where does the Inverted Repeat start - is is ycf2?]

upload geseq.gff3 to galaxy

Get data
choose local file x2, start, close

JBrowse: geseq.gff3 and polished.fasta

two contigs

re-name view polished.fasta annotations

[note: two gff tracks displayed under each but one will be empty under each.]

annotation: a constantly-improving process as more info for matching to seq string, seq structure, etc.
can be multiple annotations under each feature depending on the database matched.

[option: repeat jbrowse, add the barrnap gff track to compare where that mapped the rRNAs - can see that the geseq annotation is slightly different]

** Extension exercise: assemble the snow gum chloroplast genome **


##### See this history in Galaxy

If you want to see this Galaxy history without performing the steps above:

* Log in to Galaxy Australia: [https://usegalaxy.org.au/](https://usegalaxy.org.au/)
* Go to <ss>Shared Data</ss>
* Click <ss>Histories</ss>
* Click <fn>Completed-assembly-analysis</fn>
* Click <ss>Import</ss> (at the top right corner)
* The analysis should now be showing as your current history.

##### See this workflow in Galaxy



##### What's next?

You can find more tutorials at

Galaxy Australia Training

and

the Galaxy Training Network:

* [http://galaxyproject.github.io/training-material/](http://galaxyproject.github.io/training-material/)




<!-- File prep:

Created history: sweet potato chloroplast tutorial data

Nanopore data
Galaxy: Get data: EBI SRA:
enter in search box: SRR6828567
click on the link under run
under FASTQ files (Galaxy) click on File 1
will upload into current history

repeat for Illumina data: SRR6828568
note this data says paired but there is only one file.
these don't look paired, I uncompressed and looked at the last reads in the file and they are numbered xxx/1
probably ok to use though as just using for correction

Renamed.
Uncompressed (don't know what this tool is or how to find it in tools).
Reduced.
Very reduced (for a bam example).

the paper used slightly diff assembly method, which included correcting nanopore reads with illumina reads, trimming low qual, assembling nano with canu, then polish with pilon and illumina.

=> illumina file
[I found this by ncbi - looking at the Tanzania sample (see paper supp table S1) that gave the nanopore file (which is easy to find bc only one nanopore file in the set, but lots of illumina) - then searched for all reads under under this, and found the accompanying illumina file.

I've cut down the size of these datasets and hosted the data on Zenodo (with permission from author Lachlan Coin) at http://doi.org/10.5281/zenodo.3567224
-->
