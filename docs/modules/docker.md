## Containers

* Containers are a collection of tools and their dependencies, packaged into a file.
* You can download and run this file and its software, without directly installing the software itself.
* Types of containers: Docker, Singularity

### The basics

* Download and install Docker Desktop: [https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
* Open docker (e.g.: if it's running, it may show an icon in the top menu bar).
* In the terminal (or equivalent):
```
docker pull busybox   //pulls the image named "busybox" from DockerHub
docker run busybox    //creates the container, then exits if no tasks are running
docker run busybox ls //creates container, lists files, exits
docker image ls       //lists all docker images
docker --help         // docker help
```
### Getting files in and out of containers

* We will make a folder that can get share files with our containers.
* In your home directory (/Users/yourname/):

```
mkdir workspace     
cd workspace
docker run -v /Users/[yourname]/workspace:/data/ busybox touch data/plantfile
```

* <ss>-v</ss> connectes our local "workspace" folder with a "data" folder in the container.
* Around this, we <ss>docker run busybox</ss>
* Finally, we create a file with <ss>touch data/plantfile</ss>

### Example: assemble and annotate a bacterial genome

* Get some sample data files (synthetic bacterial illumina reads):
```
wget https://zenodo.org/record/582600/files/mutant_R1.fastq?download=1
wget https://zenodo.org/record/582600/files/mutant_R2.fastq?download=1
```
* Shorten the names:
```
mv mutant_R1.fastq?download=1 mutant_R1.fastq
mv mutant_R2.fastq?download=1 mutant_R2.fastq
```
* Run the assembly tool (spades) in a container:
```
docker run -v /Users/[yourname]/workspace:/data/ quay.io/biocontainers/spades:3.13.0--0 ./usr/local/bin/spades.py -1 data/mutant_R1.fastq -2 data/mutant_R2.fastq -o data/spades_outdir
```
* <ss>quay.io/biocontainers/spades:3.13.0--0</ss> is the image name
* <ss>./usr/local/bin/spades.py</ss> is the command to run spades
* <ss>-1</ss> specifies the file with forward reads, <fn>data/mutant_R1.fastq<//fn>
* <ss>-2</ss> specifies the file with reverse reads, <fn>data/mutant_R2.fastq<//fn>
* <ss>-o</ss> specifies the output directory, <fn>data/spades_outdir</fn>
```
ls      //to see the output files in your local workspace folder
```
* Move the assembled reads - the contigs file - into the workspace folder:
```
mv spades_outdir/contigs.fasta .
```
* Run the annotation tool (prokka) in a container:
```
docker run -v /Users/[yourname]/workspace:/data/ ummidock/prokka:1.13.3-01 prokka contigs.fasta
```
* <ss>ummidock/prokka:1.13.3-01</ss> is the image name
* <ss>prokka</ss> is the command to run prokka
* the input file is <fn>contigs.fasta</fn>
* this container has been configured to start within the data folder, so "data/" is not needed before the input file
* this container has also been configured to put output in the data folder, so it is not necessary to specify an output directory name
```
ls                        //to see the annotation output
cd PROKKA_outfile_name
less PROKKA_outfile.txt   //summary of annotation
```

### Troubleshooting

How do we know what the command is to run the tool?

* Run the container interactively:
* e.g.`docker run -it ummidock/prokka:1.13.3-01`
* Try the tool name and the help flag: e.g. `prokka -h`

How do we know if the container has a data folder?

* Run the container, print the working directory:
* e.g. `docker run ummidock/prokka:1.13.3-01 pwd`
<!-- alternately: `docker image inspect <container name> --format '{{json .ContainerConfig.WorkingDir}}'` -->
* If the working directory is called "workdir", use that in place of "data"
* e.g. `-v /Users/[yourname]/workspace:/workdir/`

### Links

Docker: [https://docs.docker.com/get-started/](https://docs.docker.com/get-started/)
