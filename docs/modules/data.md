# Data

When running bioinformatics analyses on the command-line, you may wish to use publicly-available data for testing or for analysis. Some examples of how to do this are given here, along with sample datasets.

## Get data with wget or curl
At the command line, type:

* `wget [address of file]`   or
* `curl -o [give the file a name][address of file]`

More about wget: [https://en.wikipedia.org/wiki/Wget](https://en.wikipedia.org/wiki/Wget)

More about curl: [https://en.wikipedia.org/wiki/CURL](https://en.wikipedia.org/wiki/CURL)

## SRA Toolkit

* Find some SRR numbers for reads you are interested in (search [NCBI's SRA](https://www.ncbi.nlm.nih.gov/sra))
* At the command line, type `fastq-dump SRR[number goes here]`
* Note: the SRR numbers refer to the sequencing run. [https://www.ncbi.nlm.nih.gov/sra/docs/submitmeta/](https://www.ncbi.nlm.nih.gov/sra/docs/submitmeta/)
* Note: `fasterq-dump` is now also supported and `fastq-dump` may be deprecated in the future.
* More about the SRA Toolkit: [https://github.com/ncbi/sra-tools/wiki](https://github.com/ncbi/sra-tools/wiki)

## Sample sequencing data

<ss>PacBio reads</ss> From Canu's quickstart page:

* `curl -L -o pacbio.fastq \
http://gembox.cbcb.umd.edu/mhap/raw/ecoli_p6_25x.filtered.fastq`

<ss>Synthetic PacBio data</ss>

* `wget https://zenodo.org/record/1009308/files/pacbio.fq?download=1`

<ss>Nanopore reads</ss> From Canu's quickstart page; data from the Loman lab:

* `curl -L -o oxford.fasta \
http://nanopore.s3.climb.ac.uk/MAP006-PCR-1_2D_pass.fasta`


<ss>Downsampled nanopore data</ss>

* `wget \
https://zenodo.org/record/842795/files/minion_1.2d_pass.fastq.fastqsanger?download=1`

<ss>fast5 files</ss>

* [https://figshare.com/articles/Raw_ONT_reads_-_barcode_1/5353210](https://figshare.com/articles/Raw_ONT_reads_-_barcode_1/5353210)

<ss>10X (linked) reads</ss>

* [https://www.10xgenomics.com/resources/datasets/](https://www.10xgenomics.com/resources/datasets/)
