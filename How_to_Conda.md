- [how to create conda env](#how-to-create-conda-env)
- [how to remove an environment](#how-to-remove-an-environment)
    - [installing nextlflow](#installing-nextlflow)


### conda install
```
 mkdir miniconda3
ls
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda3/miniconda.sh
bash miniconda3/miniconda.sh -b -u -p miniconda3

miniconda3/bin/conda init bash
miniconda3/bin/conda init zsh
```
## conda settings
from https://bioconda.github.io/
```
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge

conda config --set channel_priority strict
```

# how to create conda env
```
# to check conda envs
conda env list

# create the environment
conda create -n <env>

# activate the env
conda activate <env>

# install packages and libraries
conda install -c <pkg_name>
-c r r-essentials
```
# how to remove an environment
the name is kept
```
conda remove -n R --keep-env --all
```
### installing nextlflow
conda create -n nfcore-rnaseq
  328  conda activate nfcore-rnaseq
  329  conda install bioconda::nextflow
