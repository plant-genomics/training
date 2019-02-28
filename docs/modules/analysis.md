# Analysis


## Set up your computer





## Virtual environments

Install miniconda
e.g. MacOSX Python 3.7 64bit pkg installer
https://docs.conda.io/en/latest/miniconda.html

Set up the bioconda channel
More information: https://bioconda.github.io/

```
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```

Create new environment called mrbayes
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
