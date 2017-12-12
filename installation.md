# Installation

In this part, we will introduce how to install SNiPER.

The source code of SNiPER is open-source. The public SNiPER repository can be found in [IHEP gitlab](http://gitlab.ihep.ac.cn/zoujh/sniper). For several experiments using SNiPER, they have their own requirements, so the source code is private and installation is done by their own tools.

## General SNiPER

To build SNiPER, we need several libraries and tools installed:

* CMT, configuration management tools
* git, get the source code of SNiPER
* Python, python-devel
* Boost, boost.python
* Intel TBB, for parallel computing

It's not necessary to use root permission to install these libraries.
Create a directory for the projects:
```
$ mkdir /DEV/sniper-general
```

Create a directory called `ExternalLibs`, which will be used to install the external libraries:
```
$ mkdir /DEV/sniper-general/ExternalLibs
```



## Experiments-specific SNiPER

* For JUNO experiment, there is a tool called `junoenv`.
* For nEXO experiment, there is a tool called `nexoenv`.
