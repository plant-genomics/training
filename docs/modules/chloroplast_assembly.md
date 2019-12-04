#### Assemble and annotate a chloroplast genome

** What is genome assembly? **

* Genome assembly is the process of joining together DNA sequencing fragments into longer pieces, ideally up to chromosome lengths.
* The DNA fragments are produced by DNA sequencing machines, and are called "reads". These are in lengths of about 150 base pairs, to up to a million (or more) base pairs, depending on the sequencing technology used. Currently, most reads are from Illumina (short), PacBio (long) or Oxford Nanopore (long and extra-long) machines.
* It is difficult to assemble plant genomes as they are often large (for example, 3,000,000,000 base pairs), have many repeat regions (such as transposons), and may be polyploid.
* This tutorial shows genome assembly for a smaller data set - the plant chloroplast genome - a circular chromosome about 160,000 base pairs long.
* The process shown here is applicable to assembling plant nuclear genomes but there would be extra steps (and much more time) involved. For example, additional sequencing would usually be run on 10X, BioNano or HiC to produce information to link up longer nuclear chromosome pieces.
* We will use the Galaxy Australia platform (a web page) to run our analysis.

<fn>**New to Galaxy?** Go to [Galaxy Australian Training](https://galaxy-au-training.github.io/tutorials/) and try the first two tutorials "Get started" and "Learn key tasks"</fn>

** Tutorial overview **

* The chloroplast genome of the sweet potato has been sequenced.
* This has produced many sequencing reads - DNA fragments.
* We will try to join these reads together to make the whole chloroplast genome sequence.
* The data is from this paper: [Zhou C, Duarte T, Silvestre R et al. 2018](https://doi.org/10.12688/gatesopenres.12856.1)








** Get the data **

* Log in to Galaxy Australia at [usegalaxy.org.au](https://usegalaxy.org.au/).
*



** Where is the data from? **
