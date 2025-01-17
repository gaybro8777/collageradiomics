![Continuous Delivery](https://github.com/radxtools/collageradiomics/workflows/Continuous%20Delivery/badge.svg) [![Documentation Status](https://readthedocs.org/projects/collageradiomics/badge/?version=latest)](https://collageradiomics.readthedocs.io/en/latest/?badge=latest) [![doi](https://img.shields.io/badge/doi-10.1038/srep37241-brightgreen.svg)](https://doi.org/10.1038/srep37241)

# Co-occurrence of Local Anisotropic Gradient Orientations (CoLlAGe)

# Table of Contents
- [Science](#science)
  - [Overview](#overview)
  - [Features](#features)
  - [References](#references)
- [Code](#code)
  - [Idempotence](#idempotence)
  - [Documentation](#documentation)
  - [Dependencies](#dependencies)
- [Installation & Usage](#installation--usage)
  - [Executive Summary for Experts](#executive-summary-for-experts)
  - [Docker](#docker)
    - [Docker Setup](#docker-setup)
    - [collageradiomics-examples Docker Image](#collageradiomics-examples-docker-image)
    - [collageradiomics-pip Docker Image](#collageradiomics-pip-docker-image)
  - [Pip](#pip)
  - [Python Usage](#python-usage)
    - [Basic Example](#basic-example)
    - [Real Data](#real-data)
- [Other Platforms](#other-platforms)
- [Contact](#contact)

# Science
## Overview
_[Back to **Table of Contents**](#table-of-contents)_

**CoLlAGe** captures subtle anisotropic differences in disease pathologies by measuring entropy of co-occurrences of voxel-level gradient orientations on imaging computed within a local neighborhood.

**CoLlAGe** is based on the hypothesis that disruption in tissue microarchitecture can be quantified on imaging by measuring the disorder in voxel-wise gradient orientations. CoLlAGe involves assigning every image voxel a ‘disorder value’ associated with the co-occurrence matrix of gradient orientations computed around every voxel.

Details on extraction of **CoLlAGe** features are included in [\[1\]](#references). After feature extraction, the subsequent distribution or different statistics such as mean, median, variance etc can be computed and used in conjunction with a machine learning classifier to distinguish similar appearing pathologies. The feasibility of CoLlAGe in distinguishing cancer from treatment confounders/benign conditions and characterizing molecular subtypes of cancers has been demonstrated in the context of multiple challenging clinical problems.

## Features
_[Back to **Table of Contents**](#table-of-contents)_

Each of the 13 **CoLlAGe** correlate to one of the 13 Haralick texture features[\[2\]](#references):
1. _AngularSecondMoment_
2. _Contrast_
3. _Correlation_
4. _SumOfSquareVariance_
5. _SumAverage_
6. _SumVariance_
7. _SumEntropy_
8. _Entropy_
9. _DifferenceVariance_
10. _DifferenceEntropy_
11. _InformationMeasureOfCorrelation1_
12. _InformationMeasureOfCorrelation2_
13. _MaximalCorrelationCoefficient_

## References
_[Back to **Table of Contents**](#table-of-contents)_

<a href="http://bric-lab.com"><img align="right" height=100 src="https://static.wixstatic.com/media/a0e8e5_809a649f13254ff293405c7476004e20~mv2.png/v1/fill/w_248,h_240,al_c,usm_0.66_1.00_0.01/a0e8e5_809a649f13254ff293405c7476004e20~mv2.png"></a>

If you make use of this implementation, please cite the following paper:

[1] Prasanna, P., Tiwari, P., & Madabhushi, A. (2016). "Co-occurrence of Local Anisotropic Gradient Orientations (CoLlAGe): A new radiomics descriptor. Scientific Reports", 6:37241.

[2] R. M. Haralick, K. Shanmugam and I. Dinstein, "Textural Features for Image Classification," in IEEE Transactions on Systems, Man, and Cybernetics, vol. SMC-3, no. 6, pp. 610-621, Nov. 1973, [doi: 10.1109/TSMC.1973.4309314](https://doi.org/10.1109/TSMC.1973.4309314).

# Code

## Idempotence
_[Back to **Table of Contents**](#table-of-contents)_

Our **CoLlAGe** module includes parameter tuning information in the output. It contains the image(s) and mask(s), and the settings applied upon them. This allows multiple fully reproducible runs without having to remember or find the original parameters.

## Documentation
_[Back to **Table of Contents**](#table-of-contents)_

http://collageradiomics.rtfd.io/

## Dependencies:
_[Back to **Table of Contents**](#table-of-contents)_

We thank these generous developers that allowed us to build collageradiomics without reinventing the wheel:
- `matplotlib`
- `numpy`
- `scikit-learn`
- `scikit-build`
- `mahotas`
- `scipy`

_(Note: We are using ```==``` for version numbers of our dependencies as a design choice.)_

# Installation & Usage
These instructions will help set up the **CoLlAGe** core module and examples. They assume you are working out of a terminal such as **Powershell** on Windows or **Konsole** on Linux.

## Executive Summary for Experts
_[Back to **Table of Contents**](#table-of-contents)_

If you are already well-versed in **Docker** and **pip**, here is a quick list of commands for each operating system:

### Linux
```shell
sudo docker pull radxtools/collageradiomics-pip:latest
sudo docker run -it radxtools/collageradiomics-pip

git clone https://github.com/radxtools/collageradiomics.git
sudo docker pull radxtools/collageradiomics-examples:latest
sudo docker run -it -p 8888:8888 -v $PWD:/root radxtools/collageradiomics-examples

pip3 install collageradiomics
```

### Windows
```console
docker pull radxtools/collageradiomics-pip:latest
docker run -it -v ${PWD}:/root radxtools/collageradiomics-pip

git clone https://github.com/radxtools/collageradiomics.git
docker pull radxtools/collageradiomics-examples:latest
docker run -it -p 8888:8888 -v ${PWD}:/root radxtools/collageradiomics-examples

pip install collageradiomics
```

You may wish to jump right to some [**Python** examples](https://github.com/radxtools/tree/master/jupyter/examples).

## Docker
_[Back to **Table of Contents**](#table-of-contents)_

**Docker** is like a stand-alone operating system container that comes pre-installed with all the dependencies already set up properly. It allows you to jump right into coding with **CoLlAGe**. We offer 2 **Docker** images: a basic core image for you to start coding with the **CoLlAGe** features (called _[collageradiomics-pip](#collageradiomics-pip-docker-image)_) and an image that contains a running **Jupyter** notebook with **CoLlAGe** pre-installed and examples ready to run (called _[collageradiomics-examples](#collageradiomics-examples-docker-image)_).

### Docker Setup
_[Back to **Table of Contents**](#table-of-contents)_

#### Linux
* Ubuntu: https://docs.docker.com/engine/install/ubuntu/
* CentOS: https://docs.docker.com/engine/install/centos/
* Debian: https://docs.docker.com/engine/install/debian/ 
* Fedora: https://docs.docker.com/engine/install/fedora/ 
* General Linux: https://docs.docker.com/engine/install/binaries/

#### macOS
Follow instructions here: https://docs.docker.com/docker-for-mac/install/

#### Windows
1. [Click here](https://www.docker.com/get-started) and follow the instructions to install **Docker**.
2. Search for **Docker** in your start manu and run it:  
![Docker Search](https://i.imgur.com/QrhfUj9.png)
3. If it's running you should see an icon:  
![Docker Initializing](https://i.imgur.com/lylVdSc.png)  
![Docker Icon](https://i.imgur.com/NzGJQaO.png)

### collageradiomics-examples Docker Image
_[Back to **Table of Contents**](#table-of-contents)_

This **Docker** image contains a running Jupyter notebook with the **CoLlAGe** module pre-installed. From the cloned repository directory, we will start up a **Docker** image which will run a live web server and host a **Jupyter** notebook at the URL http://localhost:8888 which contains examples of using the code.

_Note: Using this method requires you to pull the code from our repository. If you don't need the **Jupyter** examples and just want to start using **CoLlAGe** right away, you can skip this step and jump to the instructions for **Core** by [clicking here](#collageradiomics-pip-docker-image)._

#### Linux
_Note: This was tested on Ubuntu 19.10 and 20.04_

1. Install git:
```console
user@machine:~$ sudo apt -y install git
Reading package lists... Done
Building dependency tree       
Reading state information... Done
git is already the newest version (1:2.20.1-2ubuntu1.19.10.3).
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
user@machine:~$ 
```
2. Clone the repository:
```console
user@machine:~$ git clone https://github.com/radxtools/collageradiomics.git
Cloning into 'collageradiomics'...
remote: Enumerating objects: 280, done.
remote: Total 280 (delta 0), reused 0 (delta 0), pack-reused 280user
Receiving objects: 100% (280/280), 1.48 MiB | 9.23 MiB/s, done.
Resolving deltas: 100% (125/125), done.
user@machine:~$ cd collageradiomics
user@machine:~/collageradiomics$ ls -l

```
3. Pull the latest **Docker** image:  
```console
user@machine:~/collageradiomics$ sudo docker pull radxtools/collageradiomics-examples:latest
latest: Pulling from radxtools/collageradiomics-examples
Digest: sha256:107a2804e76b156f40d571b8422f822a3712353645c86e5cc2275d2aea85c9be
Status: Image is up to date for radxtools/collageradiomics-examples:latest
docker.io/radxtools/collageradiomics-examples:latest
user@machine:~/collageradiomics$ 
```
4. Run the **Docker** image:  
```console
user@machine:~/collageradiomics$ sudo docker run -it -p 8888:8888 -v $PWD:/root radxtools/collageradiomics-examples
[I 06:35:13.806 NotebookApp] Writing notebook server cookie secret to /tmp/notebook_cookie_secret
[W 06:35:14.030 NotebookApp] All authentication is disabled.  Anyone who can connect to this server will be able to run code.
[I 06:35:14.033 NotebookApp] Serving notebooks from local directory: /root
[I 06:35:14.034 NotebookApp] The Jupyter Notebook is running at:
[I 06:35:14.034 NotebookApp] http://d41cc76f5035:8888/
[I 06:35:14.034 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
```

You can now skip over the _Windows_ installation instructions and jump straight to the [Exploring The Examples](#exploring-the-examples) section.

#### Windows
1. Install **git**. A quick online search for _"git for Windows"_ will provide you with several options for installing the ```git``` command. If it's correctly installed, the following should output your current version of git:  
```console
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\Users\user> git --version
git version 2.26.2.windows.1
PS C:\Users\user>
```
2. Clone the repository:  
```console
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\Users\user> git clone https://github.com/radxtools/collageradiomics.git
Cloning into 'collageradiomics'...
remote: Enumerating objects: 280, done.
Receiving objects:  97% (272/280), 1.24 MiB | 1.02 MiB/sused 280 eceiving objects:  91% (255/280), 1.24 MiB | 1.02 MiB/s
Receiving objects: 100% (280/280), 1.48 MiB | 1.09 MiB/s, done.
Resolving deltas: 100% (125/125), done.
PS C:\Users\user> cd collageradiomics
PS C:\Users\user\collageradiomics> dir


    Directory: C:\Users\user\collageradiomics


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       2020-06-24      3:31                docker
d-----       2020-06-24      3:31                jupyter
d-----       2020-06-24      3:31                module
d-----       2020-06-24      3:31                sample_data
-a----       2020-06-24      3:31            215 .gitignore
-a----       2020-06-24      3:31          35823 LICENSE
-a----       2020-06-24      3:31           4045 README.md
-a----       2020-06-24      3:31            136 start.sh


PS C:\Users\user\collageradiomics>
```
3. Give **Docker** access to your cloned repository:
   1. Right click on the context menu near the clock:  
   ![Docker Context Menu](https://i.imgur.com/CSY0GzK.png)
   2. Select _Dashboard_:  
   ![Docker Dashboard](https://i.imgur.com/zIlGKvb.png)
   3. After you click on _Dashboard_, a window will pop up. Click on the gear icon for _Settings_ and move to _Resources_ :arrow_right: _File Sharing_.  
   ![Docker Filesharing](https://i.imgur.com/JLiVp72.png)
   4. Add your cloned repository folder:  
   ![Docker Add Repo](https://i.imgur.com/lb8RN1O.png)
4. Pull the latest **Docker** image:
```console
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\Users\user\collageradiomics> docker pull radxtools/collageradiomics-examples:latest
latest: Pulling from radxtools/collageradiomics-examples
d51af753c3d3: Already exists
fc878cd0a91c: Already exists
6154df8ff988: Already exists
fee5db0ff82f: Already exists
a6501aa3ed52: Already exists
Digest: sha256:107a2804e76b156f40d571b8422f822a3712353645c86e5cc2275d2aea85c9be
Status: Downloaded newer image for radxtools/collageradiomics-examples:latest
docker.io/radxtools/collageradiomics-examples:latest
PS C:\Users\user\collageradiomics> docker pull radxtools/collageradiomics-examples:latest
latest: Pulling from radxtools/collageradiomics-examples
Digest: sha256:107a2804e76b156f40d571b8422f822a3712353645c86e5cc2275d2aea85c9be
Status: Image is up to date for radxtools/collageradiomics-examples:latest
docker.io/radxtools/collageradiomics-examples:latest
PS C:\Users\user\collageradiomics>
```
5. Run the **Docker** image:
```console
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\Users\user> cd collageradiomics
PS C:\Users\user\collageradiomics> docker run -it -p 8888:8888 -v ${PWD}:/root radxtools/collageradiomics-examples
[I 08:28:36.091 NotebookApp] Writing notebook server cookie secret to /tmp/notebook_cookie_secret
[W 08:28:36.576 NotebookApp] All authentication is disabled.  Anyone who can connect to this server will be able to run code.
[I 08:28:36.585 NotebookApp] Serving notebooks from local directory: /root
[I 08:28:36.585 NotebookApp] The Jupyter Notebook is running at:
[I 08:28:36.585 NotebookApp] http://c5745f91dbee:8888/
[I 08:28:36.585 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
```

#### Exploring The Examples
_[Back to **Table of Contents**](#table-of-contents)_

1. Open up a web browser to http://localhost:8888  
![Jupyter Home](https://i.imgur.com/0XQ8OlT.png)
2. Navigate to the _Jupyter_ :arrow_right: _Examples_ directory.  
![Jupyter Examples](https://i.imgur.com/NjdMlOr.png)
3. Click on one of the example `*.ipynb` files.
4. Run _Cell_ :arrow_right: _Run all_.  
![Jupyter Run Cells](https://i.imgur.com/GaAaNAS.png)
![Jupyter Output](https://i.imgur.com/PapCcsg.png)
5. Feel free to add your own cells and run them to get familiar with the **CoLlAGe** code.
6. To stop the **Jupyter** notebook and exit the **Docker** image, press `Ctrl+C` twice:
```console
[I 07:05:36.271 NotebookApp] The Jupyter Notebook is running at:
[I 07:05:36.271 NotebookApp] http://4f033d68769d:8888/
[I 07:05:36.271 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
^C[I 07:05:37.628 NotebookApp] interrupted
Serving notebooks from local directory: /root
0 active kernels
The Jupyter Notebook is running at:
http://4f033d68769d:8888/
Shutdown this notebook server (y/[n])? ^C[C 07:05:38.744 NotebookApp] received signal 2, stopping
[I 07:05:38.745 NotebookApp] Shutting down 0 kernels
user@machine:~/collageradiomics$ 
```

### collageradiomics-pip Docker Image
_[Back to **Table of Contents**](#table-of-contents)_

This is the most straightforward way to start playing with the code. And it does not require the `git` commands that the **Jupyter** examples require. This is simply a pre-built container that lets you start trying out the module in **Python** immediately.

#### Linux
1. Pull the latest **Docker** image:
```console
user@machine:~$ sudo docker pull radxtools/collageradiomics-pip:latest
latest: Pulling from radxtools/collageradiomics-pip
Digest: sha256:8fc7d61dbe6ad64eeff9c69cfaa788d90c61861bff8aaf8865ed1318c5666250
Status: Image is up to date for radxtools/collageradiomics-pip:latest
docker.io/radxtools/collageradiomics-pip:latest
user@machine:~/collageradiomics$
```
2. Run the **Docker** image:
```console
user@machine:~/collageradiomics$ sudo docker run -it -v $PWD:/root radxtools/collageradiomics-pip
root@12b12d2bff59:/# 
```

#### Windows
1. Pull the latest **Docker** image:
```console
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\Users\user> docker pull radxtools/collageradiomics-pip:latest
latest: Pulling from radxtools/collageradiomics-pip
d51af753c3d3: Already exists
fc878cd0a91c: Already exists
6154df8ff988: Already exists
fee5db0ff82f: Already exists
e4255cf4d4f9: Downloading [=================>                                 ]  62.34MB/178.6MB
14a983cf96b6: Downloading [===========================>                       ]  55.72MB/102.9MB      
14a983cf96b6: Pull complete
Digest: sha256:8fc7d61dbe6ad64eeff9c69cfaa788d90c61861bff8aaf8865ed1318c5666250
Status: Downloaded newer image for radxtools/collageradiomics-pip:latest
docker.io/radxtools/collageradiomics-pip:latest
PS C:\Users\user>
```
2. Run the **Docker** image:
```console
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\Users\user> docker pull radxtools/collageradiomics-pip:latest
PS C:\Users\user> docker run -it radxtools/collageradiomics-pip
root@461c5017ce0e:/#
```

#### Inside The Container
_[Back to **Table of Contents**](#table-of-contents)_

If your terminal prompt changes to `root@[random_string]:/#` then you are now working inside the standardized **Docker** sandbox container environment.

1. Test the python module by making sure the following command outputs `True` to the terminal:  
```console
root@12b12d2bff59:/# python -c 'import numpy as np; import collageradiomics; print(not not len(collageradiomics.__name__) and not not len(collageradiomics.Collage.from_rectangle(np.random.rand(20,20,3), 2, 2, 10, 10).execute()));'
True
root@12b12d2bff59:/# 
```
2. Starting coding with **CoLlAGe** in **Python** [(click here to jump to code examples)](#python-usage):
```console
root@12b12d2bff59:/# python
Python 3.8.2 (default, Apr 27 2020, 15:53:34) 
[GCC 9.3.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import collageradiomics
>>> collageradiomics.__name__
'collageradiomics'
>>> 
```
3. Exit the **Docker** container:
```console
>>> quit()
root@12b12d2bff59:/# exit
exit
```

## Pip
_[Back to **Table of Contents**](#table-of-contents)_

To use this module in your existing **Python** development environment, you can install our **pip** module.

### Linux
1. Install **pip**:
```console
user@machine:~$ sudo apt -y install python3-pip
Reading package lists... Done
Building dependency tree       
Reading state information... Done
python3-pip is already the newest version (18.1-5).
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
user@machine:~$ 
```
2. Install our **CoLlAGe** module:  
```console
user@machine:~$ pip3 install collageradiomics --upgrade
Collecting collageradiomics
  Downloading https://files.pythonhosted.org/packages/58/46/73d6b5a6d0d2b952086a1c9c4ae339087e4678f421044847ab2ea8728adf/collageradiomics-0.0.1a39-py3-none-any.whl
...
(some output omitted for brevity)
...
Successfully installed collageradiomics-...
user@machine:~$ 
```
*(Note: For some operating systems, the command is simply `pip` instead of `pip3`.)*

### Windows
1. Install **Python** using [this link](https://www.python.org/downloads/windows/).
2. Test that **Python** is properly installed in the Powershell:
```console
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\Users\user> python --version
Python 3.8.2
PS C:\Users\user> python
Python 3.8.2 (tags/v3.8.2:7b3ab59, Feb 25 2020, 23:03:10) [MSC v.1916 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> quit()
PS C:\Users\user>
```
3. Install pip by downloading this [get-pip.py file](https://bootstrap.pypa.io/get-pip.py) and running the following command:
```console
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\Users\user> python get-pip.py
Collecting pip
  Downloading pip-20.1.1-py2.py3-none-any.whl (1.5 MB)
     |████████████████████████████████| 1.5 MB 3.2 MB/s
Collecting wheel
  Using cached wheel-0.34.2-py2.py3-none-any.whl (26 kB)
Installing collected packages: pip, wheel
  Attempting uninstall: pip
    Found existing installation: pip 20.0.2
    Uninstalling pip-20.0.2:
      Successfully uninstalled pip-20.0.2
Successfully installed pip-20.1.1 wheel-0.34.2
PS C:\Users\user> pip -V
pip 20.1.1 from c:\users\robto\appdata\local\programs\python\python38\lib\site-packages\pip (python 3.8)
PS C:\Users\user>
```
4. Install our module
```console
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\Users\user> pip install collageradiomics --upgrade
```
5. Verify its installation in **Python**:
```console
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\Users\user> python
>>> import collageradiomics
>>>
```
6. If you get an error like the one below, which can happen for some versions of python, call `import` again:
```console
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Try the new cross-platform PowerShell https://aka.ms/pscore6

PS C:\Users\user> python
>>> import collageradiomics
Could not import submodules (exact error was: DLL load failed while importing _bbox: The specified module could not be found.).

There are many reasons for this error the most common one is that you have
either not built the packages or have built (using `python setup.py build`) or
installed them (using `python setup.py install`) and then proceeded to test
mahotas **without changing the current directory**.

Try installing and then changing to another directory before importing mahotas.
>>> import collageradiomics
>>>
```

## Python Usage
_[Back to **Table of Contents**](#table-of-contents)_

collageradiomics can be implemented in **Python** through the `collageradiomics` pip module. It has a intuitive interface - simply create a `Collage` object and run the `execute()` function.

# Other Platforms
_[Back to **Table of Contents**](#table-of-contents)_

The RadxTools COLLAGE implementation is now available through the Cancer Phenomics Toolkit (CaPTk), developed by the Center for Biomedical Image Computing and Analytics (CBICA) at the University of Pennsylvania. For more information see https://github.com/CBICA/CaPTk


# Contact
_[Back to **Table of Contents**](#table-of-contents)_

Please report any issues or feature requests via the [Issues](https://github.com/radxtools/collageradiomics/issues) tab

Additional information can be found on the [BrIC Lab](http://bric-lab.com) website.
