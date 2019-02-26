# Useful training links

## Unix, git, python, R
https://software-carpentry.org/lessons/

## Collected bioinformatics tutorials
https://isugenomics.github.io/bioinformatics-workbook/

## Next-gen sequence analysis workshop - ANGUS - UCDavis
https://angus.readthedocs.io/en/2018/#

## Solving biological problems with python
http://pycam.github.io/

## Algorithms
https://www.coursera.org/learn/dna-sequencing
https://www.youtube.com/user/BenLangmead

## Containers for bioinformatics
https://github.com/pawseysc/bio-workshop-18

## Virtual environment

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
```conda create --name mrbayes```
```conda activate mrbayes``

Install a tool (or you can do this outside an environment)
Search here for tools: https://anaconda.org/bioconda/
```conda install mrbayes```

Deactivate the environment
```conda deactivate```




