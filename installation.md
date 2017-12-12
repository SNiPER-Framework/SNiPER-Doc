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

### External Libraries
It's not necessary to use root permission to install these libraries.
We will use a normal user to install them.

Create a directory for the projects:
```
$ mkdir /DEV/sniper-general
```

Create a directory called `ExternalLibs`, which will be used to install the external libraries:
```
$ mkdir /DEV/sniper-general/ExternalLibs
```

Create `Build` under it, to save installation tarballs and caches.
```
$ mkdir /DEV/sniper-general/ExternalLibs/Build
```

#### Python
Let's install python first:
```
$ cd /DEV/sniper-general/ExternalLibs/Build
$ wget http://www.python.org/ftp/python/2.7.14/Python-2.7.14.tgz
$ tar zxvf Python-2.7.14.tgz 
$ cd Python-2.7.14
$ mkdir -p /DEV/sniper-general/ExternalLibs/Python/2.14
$ ./configure --prefix=/DEV/sniper-general/ExternalLibs/Python/2.14 --enable-shared --enable-unicode=ucs4
$ make -j8
$ make install
```

To make python available for us, we create a setup script `bashrc`:
```
$ touch /DEV/sniper-general/ExternalLibs/Python/2.14/bashrc
$ # Please edit this file
$ cat /DEV/sniper-general/ExternalLibs/Python/2.14/bashrc
export PYTHONROOT=/DEV/sniper-general/ExternalLibs/Python/2.14
export PATH=$PYTHONROOT/bin:$PATH
export LD_LIBRARY_PATH=$PYTHONROOT/lib:$LD_LIBRARY_PATH
export PKG_CONFIG_PATH=$PYTHONROOT/lib/pkgconfig:$PKG_CONFIG_PATH
export CPATH=$PYTHONROOT/include:$CPATH
export CMAKE_PREFIX_PATH=$PYTHONROOT:$CMAKE_PREFIX_PATH
export PYTHONPATH=$PYTHONROOT/lib/python2.7/lib-dynload:$PYTHONPATH
```

Then source this bashrc:
```
$ source /DEV/sniper-general/ExternalLibs/Python/2.14/bashrc
$ which python
/DEV/sniper-general/ExternalLibs/Python/2.14/bin/python
```

#### Boost
Now, let's install boost. Before install boost, make sure you source `bashrc` of our own python.
Then, download and install it:
```
$ cd /DEV/sniper-general/ExternalLibs/Build
$ wget http://sourceforge.net/projects/boost/files/boost/1.65.1/boost_1_65_1.tar.gz
$ tar zxvf boost_1_65_1.tar.gz 
$ 
```

## Experiments-specific SNiPER

* For JUNO experiment, there is a tool called `junoenv`.
* For nEXO experiment, there is a tool called `nexoenv`.
