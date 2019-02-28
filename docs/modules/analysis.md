## Set up your computer

A virtual environment is an area to work in that is associated with certain tools and versions.

It is often useful to work on different bioinformatics analyses or tasks in different virtual environments, as they may rely on particular versions of tools.

One way to set this up is to use a package manager called conda.

* Install miniconda

e.g. MacOSX Python 3.7 64bit pkg installer

https://docs.conda.io/en/latest/miniconda.html

* Set up the bioconda channel

More information: https://bioconda.github.io/

```
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```

* Create new environment called mrbayes
```
conda create --name mrbayes
conda activate mrbayes
```

Install a tool (or you can do this outside an environment)
Search here for tools: https://anaconda.org/bioconda/
```
conda install mrbayes
```

Deactivate the environment
```
conda deactivate
```


### How to use HPC

See [HPC analysis](hpc.md)

### How to use web platforms

See [Web platforms](platforms.md)
