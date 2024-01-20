# python_tutorial
Python tutorial including dependency management.

**Please feel free to create an issue for better ways to managing deps and compats**.

Python is not my main programming language,
and I don't still know the best way to manage the deps and compats.
I think [poetry](https://python-poetry.org/) is promising but
it was often unstable to use daily from my experiences.



## Dependency management via Miniconda
Here, we will consider Miniconda for beginners of Python.

### Install Miniconda
Here, we are gonna use [miniconda](https://docs.conda.io/projects/miniconda/en/latest/), which is a smaller version of [Anaconda](https://www.anaconda.com/).
- Visit the miniconda official website (e.g., [Latest Miniconda installer links by Python version](https://docs.conda.io/projects/miniconda/en/latest/miniconda-other-installer-links.html)) and follow the instruction to download the installer (for your OS) and to install miniconda.

### Create a new environment
Execute the following command to create a new environment with its name of `{env_name}` and the python version of `{py_version}`.
```
conda create -n {env_name} python={py_version}
```

For example,
```
conda create -n my_env python=3.10
```
will create a new environment `my_env` with python version `3.10`.


### Activate and deactivate a conda environment
```
#
# To activate this environment, use
#
#     $ conda activate my_env
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

In case you use `zsh`, you can see if a conda env is activated or not as follows,
```
➜  ~ conda activate my_env
(my_env) ➜  ~ conda deactivate
➜  ~
```

### Add dependencies (deps)
The simplest way to add deps is to use `pip install`.
For example,
```
➜  ~ conda activate my_env
(my_env) ➜  ~ pip install numpy
Collecting numpy
  Downloading numpy-1.26.3-cp310-cp310-macosx_10_9_x86_64.whl.metadata (61 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 61.2/61.2 kB 2.8 MB/s eta 0:00:00
Downloading numpy-1.26.3-cp310-cp310-macosx_10_9_x86_64.whl (20.6 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 20.6/20.6 MB 36.7 MB/s eta 0:00:00
Installing collected packages: numpy
Successfully installed numpy-1.26.3
(my_env) ➜  ~ python
Python 3.10.13 (main, Sep 11 2023, 08:39:02) [Clang 14.0.6 ] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import numpy
>>>
(my_env) ➜  ~ conda list
# packages in environment at /Users/jinrae/miniconda3/envs/my_env:
#
# Name                    Version                   Build  Channel
bzip2                     1.0.8                h1de35cc_0
ca-certificates           2023.12.12           hecd8cb5_0
libffi                    3.4.4                hecd8cb5_0
ncurses                   6.4                  hcec6c5f_0
numpy                     1.26.3                   pypi_0    pypi
openssl                   3.0.12               hca72f7f_0
pip                       23.3.1          py310hecd8cb5_0
python                    3.10.13              h5ee71fb_0
readline                  8.2                  hca72f7f_0
setuptools                68.2.2          py310hecd8cb5_0
sqlite                    3.41.2               h6c40b1e_0
tk                        8.6.12               h5d9f67b_0
tzdata                    2023d                h04d1e81_0
wheel                     0.41.2          py310hecd8cb5_0
xz                        5.4.5                h6c40b1e_0
zlib                      1.2.13               h4dc903c_0
(my_env) ➜  ~ conda list | grep numpy
numpy                     1.26.3                   pypi_0    pypi
```

### How to make it reproducible?
After installing `matplotlib` in the conda env `my_env`
and creating a new conda env `my_env2` with the same Python version,
```
(my_env) ➜  ~ pip freeze > requirements.txt
(my_env) ➜  ~ cat requirements.txt
contourpy==1.2.0
cycler==0.12.1
fonttools==4.47.2
kiwisolver==1.4.5
matplotlib==3.8.2
numpy==1.26.3
packaging==23.2
pillow==10.2.0
pyparsing==3.1.1
python-dateutil==2.8.2
six==1.16.0
(my_env) ➜  ~ conda deactivate
➜  ~ conda activate my_env2
(my_env2) ➜  ~ pip freeze
(my_env2) ➜  ~ pip install -r requirements.txt

...


(my_env2) ➜  ~ pip freeze
contourpy==1.2.0
cycler==0.12.1
fonttools==4.47.2
kiwisolver==1.4.5
matplotlib==3.8.2
numpy==1.26.3
packaging==23.2
pillow==10.2.0
pyparsing==3.1.1
python-dateutil==2.8.2
six==1.16.0
```
