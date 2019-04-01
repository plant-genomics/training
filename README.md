# Training

* Training materials and links for plant genomics.
* These tutorials have been developed by the Australian plant genomics community as part of the Genomics for Australian Plants project, by Bioplatforms Australia. https://www.genomicsforaustralianplants.com/
* The tutorials have been deployed here:  https://plant-genomics.github.io/training/
* Tutorials are written in [Markdown](http://en.wikipedia.org/wiki/Markdown) and built with [MkDocs](http://www.mkdocs.org/).

## How to contribute

This section is a guide to contributing edits to the repository.

### Fork and clone this repository

You should do your work in a fork under your own github account:

* Fork this repository in github using the fork button.
* Clone your fork to your local computer.
```
git clone https://github.com/yourname/training.git
```

### Set up your environment and build the documentation

* We are using the Python package [MkDocs](http://www.mkdocs.org/).
* You can install MkDocs into a virtual environment, e.g. with conda.
```
conda create --name mkdocs      //we call our environment "mkdocs"
conda activate mkdocs
conda install pip               
pip install -r requirements.txt  //this file lists the packages required
```

### Edit

* A useful editor is Atom: https://atom.io
* In Atom, open up the folder and edit in here.
* In the terminal, open a new tab and serve the page (i.e. display in a browser tab) by: `mkdocs serve`
* Open your web browser to http://127.0.0.1:8000/ and leave it open.
* This will update automatically as you make changes to the documenation.
* On the web, the contents (displayed in the left hand column) are determined by the mkdocs.yaml file.
* Add or delete topics (and their location) in this file.

### Pull request

* Add, commit and push your changes to your repository.

```
git add .  \\use the dot to mean everything, or name the files
git commit -m ["add commit message here"]
git push
```

* Open your repository (=a fork of the original repository) in github and create a pull request to the original repository.

* If your fork is up to date, you should see "These branches can be automatically merged" while you are creating the pull request. If your fork is *not* up to date you should bring it up to date (sync with upstream) and resolve any merge conflicts before creating the pull request.

* To do this:

```
git remote add upstream https://github.com/plant-genomics/training.git
git fetch upstream
git merge upstream/master
```
### Deploy

* After you, or someone else, accepts your pull request, you can deploy the page (make it available on the internet):

```
git clone https://github.com/plant-genomics/training
cd training
mkdocs gh-deploy
```
* Note: this is a direct copy of the repository, not a clone of your copy of the repository.
* Check that the updated tutorial appears under  https://plant-genomics.github.io/training/
