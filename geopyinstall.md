>conda create --name geopyenv

Fetching package metadata .............
Solving package specifications:
Package plan for installation in environment C:\Users\shawnm\AppData\Local\ESRI\conda\envs\geopyenv:

Proceed ([y]/n)? y

#
# To activate this environment, use:
# > activate geopyenv
#
# To deactivate an active environment, use:
# > deactivate
#
# * for power-users using bash, you must source
#

>activate geopyenv

>conda install -c conda-forge geopy

Fetching package metadata ...............
Solving package specifications: .

Package plan for installation in environment C:\Users\shawnm\AppData\Local\ESRI\conda\envs\geopyenv:

The following NEW packages will be INSTALLED:

    geographiclib: 1.52-pyhd8ed1ab_0     conda-forge
    geopy:         2.2.0-pyhd8ed1ab_0    conda-forge
    pip:           22.1.1-pyhd8ed1ab_0   conda-forge
    python:        3.7.9-1               esri
    python_abi:    3.7-2_cp37m           conda-forge
    setuptools:    62.3.2-py37h03978a9_0 conda-forge
    wheel:         0.37.1-pyhd8ed1ab_0   conda-forge

Proceed ([y]/n)? y

geographiclib- 100% |###############################| Time: 0:00:03   9.52 kB/s
python_abi-3.7 100% |###############################| Time: 0:00:00   0.00  B/s
wheel-0.37.1-p 100% |###############################| Time: 0:00:00   0.00  B/s
geopy-2.2.0-py 100% |###############################| Time: 0:00:00   2.20 MB/s
setuptools-62. 100% |###############################| Time: 0:00:00   2.97 MB/s
pip-22.1.1-pyh 100% |###############################| Time: 0:00:00   3.09 MB/s


```console 
conda install -n geopyenv ipykernel --update-deps
```

```console 
conda install -c anaconda ipython_genutils
```

```console 
conda install -c anaconda urllib3

```console 
conda install -c anaconda openssl
```

