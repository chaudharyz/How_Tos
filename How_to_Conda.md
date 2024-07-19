- [1. Install conda](#1-install-conda)
  - [1.1. Intial settings conda](#11-intial-settings-conda)
- [2. Conda environments](#2-conda-environments)
  - [2.1. create the environment](#21-create-the-environment)
  - [2.2. activate the environment](#22-activate-the-environment)
  - [2.3. Check conda environments](#23-check-conda-environments)
  - [2.4. Cloning an environment](#24-cloning-an-environment)
  - [2.5. Export an environment](#25-export-an-environment)
  - [2.6. Install environment from an environment.yml file](#26-install-environment-from-an-environmentyml-file)
  - [2.7. Restoring an environment](#27-restoring-an-environment)
  - [2.8. Remove an environment](#28-remove-an-environment)
- [3. Install packages and libraries](#3-install-packages-and-libraries)
- [4. Installing nextlflow environment](#4-installing-nextlflow-environment)


# 1. Install conda

```
# make miniconda3 directory in your home directory
mkdir miniconda3

# download the miniconda.sh from here
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda3/miniconda.sh

# run it with bash and initialise for both bash and zsh
bash miniconda3/miniconda.sh -b -u -p miniconda3

miniconda3/bin/conda init bash
miniconda3/bin/conda init zsh
```

To verify, check `conda --version`

## 1.1. Intial settings conda
from https://bioconda.github.io/

Then perform a one-time set up of Bioconda with the following commands. This will modify your ~/.condarc file:

```
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge

conda config --set channel_priority strict

```
If you have used Bioconda in the past, note that the recommended configuration has changed over the years. You should run the above commands to ensure your settings follow the current recommendations.


One can also disable channel priority as below:
```
conda config --set channel_priority false

# check channel priority
conda config --show channel_priority
```
I cannot remember why channel priority is disabled at the moment. There was some package problem at one point.

# 2. Conda environments
The beauty of conda is because of its [environments](https://docs.conda.io/projects/conda/en/latest/user-guide/concepts/environments.html).

An environment is a directory that contains a specific collection of packages that you have installed. For example, you may have one environment with NumPy 1.7 and its dependencies, and another environment with NumPy 1.6 for legacy testing. If you change one environment, your other environments are not affected. You can easily activate or deactivate environments, which is how you switch between them. You can also share your environment with someone by giving them a copy of your `environment.yaml` file. For more information, see [Managing environments](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#).

These environments work as containers in which one can contain versions of a tool or a set of tools which can be independent from other versions  


## 2.1. create the environment
```
conda create -n <env>

# to create with specific version of python
conda create -n myenv python=3.9
```
## 2.2. activate the environment
```
conda activate <env>

# to deactivate
conda deactivate <env>
```

## 2.3. Check conda environments
```
conda env list

#or

conda info --envs
```

## 2.4. Cloning an environment
```
conda create --name <new_env> --clone <orig_env>
```

## 2.5. Export an environment
```
conda activate <env>
conda env export > environment.yml
```
This file itself is enable to replicate the environment.

## 2.6. Install environment from an environment.yml file
```
conda env create -f environment.yml
```

## 2.7. Restoring an environment
Conda keeps a history of all the changes made to your environment, so you can easily "roll back" to a previous version. To list the history of each change to the current environment:
```
conda list --revisions
```

To restore environment to a previous revision: 
```
conda install --revision=REVNUM 

# or 

conda install --rev REVNUM
```

## 2.8. Remove an environment

```
conda remove -n <env> --all

# or
conda env remove --name myenv

# to keep name 
conda remove -n <env> --keep-env --all
```

# 3. Install packages and libraries
I usually install packages after activating the environment and then installing within the environment. But it is not a must and one can also install from the base env.
```
conda install -c <pkg_name>

# or 

conda create -n <env> <pkg_name>
conda install -n <env> <pkg_name>

# Example
conda install -c r r-essentials

# to install specific version of a package
conda install -c <pkg_name>=<pkg_version>
```


# 4. Installing nextlflow environment
```
conda create -n nfcore-rnaseq

conda activate nfcore-rnaseq
conda install bioconda::nextflow
```