#### How to get data

wget or curl:

* `wget [address of file]`
* `curl [address of file]`

SRA toolkit:

* Find some SRR numbers for reads you are interested in (search [NCBI's SRA](https://www.ncbi.nlm.nih.gov/sra))
* `fastq-dump SRR[number goes here]`
* More information:
* [https://ncbi.github.io/sra-tools/install_config.html](https://ncbi.github.io/sra-tools/install_config.html)
* [https://isugenomics.github.io/bioinformatics-workbook/dataAcquisition/fileTransfer/sra.html](https://isugenomics.github.io/bioinformatics-workbook/dataAcquisition/fileTransfer/sra.html)
* Note: the SRR numbers refer to the sequencing run. [https://www.ncbi.nlm.nih.gov/sra/docs/submitmeta/](https://www.ncbi.nlm.nih.gov/sra/docs/submitmeta/)


#### Sample sequencing data

* <ss>PacBio reads</ss> From Canu's quickstart page:`curl -L -o pacbio.fastq http://gembox.cbcb.umd.edu/mhap/raw/ecoli_p6_25x.filtered.fastq`
* <ss>Synthetic PacBio data</ss>: `wget https://zenodo.org/record/1009308/files/pacbio.fq?download=1`
* <ss>Nanopore reads</ss> From Canu's quickstart page; data from the Loman lab: `curl -L -o oxford.fasta http://nanopore.s3.climb.ac.uk/MAP006-PCR-1_2D_pass.fasta`
* <ss>Downsampled nanopore data</ss>: `wget https://zenodo.org/record/842795/files/minion_1.2d_pass.fastq.fastqsanger?download=1`
* <ss>fast5 files</ss> [https://figshare.com/articles/Raw_ONT_reads_-_barcode_1/5353210](https://figshare.com/articles/Raw_ONT_reads_-_barcode_1/5353210)
* <ss>10X (linked) reads</ss> [https://www.10xgenomics.com/resources/datasets/](https://www.10xgenomics.com/resources/datasets/)
