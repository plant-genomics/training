## Set up a vitual environment

* A virtual environment is an area to work in that is associated with certain tools and versions.

* It is often useful to work on different bioinformatics analyses or tasks in different virtual environments, as they may rely on particular versions of tools.

* One way to set this up is to use a package manager called conda.

* Install miniconda: [https://docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html)

* In the terminal (or equivalent), set up the bioconda channel: (More information: [https://bioconda.github.io/](https://bioconda.github.io/))

```
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```
* This example shows how to set up and use an environment:

```
conda create --name mrbayes //create new environment called mrbayes
conda activate mrbayes      //activate this environment
conda install mrbayes       //install the "mrbayes" tool
[amazing analysis]          //run your analysis
conda deactivate            //deactive this environment
```
* Search here for tools: [https://anaconda.org/bioconda/](https://anaconda.org/bioconda/)

## Using conda

```
conda env list              //what environments have you set up?
conda list -n mrbayes       // what's installed in the mrbayes environment
```
