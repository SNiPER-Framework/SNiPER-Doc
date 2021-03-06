# Installation

In this part, we will introduce how to install SNiPER.

The source code of SNiPER is open-source. The public SNiPER repository can be found in [IHEP gitlab](http://gitlab.ihep.ac.cn/zoujh/sniper). For several experiments using SNiPER, they have their own requirements, so the source code is private and installation is done by their own tools.

## General installation of SNiPER

To build SNiPER, we need several libraries and tools installed:

* CMT, configuration management tools
* git, get the source code of SNiPER
* Python, python-devel
* Boost, boost.python
* Intel TBB, for parallel computing

Note: in following example, Scientific Linux 6.9 with GCC 4.4.7 is used.  
To enable c++11 features, we use [devtoolset](http://linux.web.cern.ch/linux/devtoolset/) so that gcc 4.8 is available for us.

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
$ cd boost_1_65_1
$ mkdir -p /DEV/sniper-general/ExternalLibs/Boost/1.65.1
$ ./bootstrap.sh --prefix=/DEV/sniper-general/ExternalLibs/Boost/1.65.1
$ ./b2 install -j8
$ ./b2 install
```

Then create `bashrc`:

```
$ touch /DEV/sniper-general/ExternalLibs/Boost/1.65.1/bashrc
$ # Please edit this file
$ cat /DEV/sniper-general/ExternalLibs/Boost/1.65.1/bashrc
export BOOSTROOT=/DEV/sniper-general/ExternalLibs/Boost/1.65.1
export LD_LIBRARY_PATH=$BOOSTROOT/lib:$LD_LIBRARY_PATH
export CPATH=$BOOSTROOT/include:$CPATH
export CMAKE_PREFIX_PATH=$BOOSTROOT:$CMAKE_PREFIX_PATH
```

Source this bashrc:

```
$ source /DEV/sniper-general/ExternalLibs/Boost/1.65.1/bashrc
```

#### Intel TBB

Intel TBB is also easy to install:

```
$ cd /DEV/sniper-general/ExternalLibs/Build
$ wget https://github.com/01org/tbb/archive/2018_U2.tar.gz
$ tar zxvf 2018_U2.tar.gz 
$ cd tbb-2018_U2/
$ make
```

A bit different from other libraries, the libraries are created under `build`:

```
$ ls build/
linux_intel64_gcc_cc4.4.7_libc2.12_kernel2.6.32_debug
linux_intel64_gcc_cc4.4.7_libc2.12_kernel2.6.32_release
```

We will install both libraries under `release` and `debug`:

```
$ mkdir -p /DEV/sniper-general/ExternalLibs/tbb/2018
$ prefix=/DEV/sniper-general/ExternalLibs/tbb/2018
$ install -d $prefix/include/serial
$ install -d $prefix/include/serial/tbb
$ install -t $prefix/include/serial/tbb include/serial/tbb/*.h
$ install -d $prefix/include/tbb
$ install -t $prefix/include/tbb include/tbb/*.h
$ install -d $prefix/include/tbb/compat
$ install -t $prefix/include/tbb/compat include/tbb/compat/*
$ install -d $prefix/include/tbb/internal
$ install -t $prefix/include/tbb/internal include/tbb/internal/*
$ install -d $prefix/include/tbb/machine
$ install -t $prefix/include/tbb/machine include/tbb/machine/*.h
$ install -d $prefix/lib
$ install -t $prefix/lib build/linux*/*.so*
```

Then create `bashrc`:

```
$ touch /DEV/sniper-general/ExternalLibs/tbb/2018/bashrc
$ # Please edit this file
$ cat /DEV/sniper-general/ExternalLibs/tbb/2018/bashrc
export TBBROOT=/DEV/sniper-general/ExternalLibs/tbb/2018
export LD_LIBRARY_PATH=$TBBROOT/lib:$LD_LIBRARY_PATH
export CPATH=$TBBROOT/include:$CPATH
export CMAKE_PREFIX_PATH=$TBBROOT:$CMAKE_PREFIX_PATH
```

Source it:

```
$ source /DEV/sniper-general/ExternalLibs/tbb/2018/bashrc
```

#### CMT

Let's install CMT:

```
$ cd /DEV/sniper-general/ExternalLibs/Build
$ wget http://www.cmtsite.net/v1r26/CMTv1r26.tar.gz
$ tar -C /DEV/sniper-general/ExternalLibs -zxvf CMTv1r26.tar.gz
$ cd /DEV/sniper-general/ExternalLibs/CMT/v1r26/mgr/
$ ./INSTALL
$ source setup.sh
$ make
```

### SNiPER

After these external libraries are installed, we can install sniper now.

Get the source code:

```
$ cd DEV/sniper-general
$ git clone http://gitlab.ihep.ac.cn/zoujh/sniper.git
```

In this version, under sniper there are two directories. One is source code. Another is external interface.  
We need to setup an environment variable called `$CMTPROJECTPATH` to let CMT compile SNiPER.

```
$ cd sniper
$ export CMTPROJECTPATH=/DEV/sniper-general/sniper:$CMTPROJECTPATH
```

Setup external interfaces first. To let CMT know our installed libraries, we need to modify several files:

```
$ # edit Externals/Boost/cmt/requirements
$ cat Externals/Boost/cmt/requirements
package Boost

use Python v* Externals

macro_append Boost_linkopts " -L$BOOSTROOT/lib -lboost_python "
include_path none
```

Here, `-L$BOOSTROOT/lib` tells linker where to find `boost_python`.

Then, we could setup external interface:

```
$ cd ExternalInterface/EIRelease/cmt
$ cmt br cmt config
$ source setup.sh
```

Finally, we could build SNiPER:

```
$ cd /DEV/sniper-general/sniper/sniper/SniperRelease/cmt
$ cmt br cmt config
$ source setup.sh
$ cmt br cmt make
```

## Experiments-specific SNiPER

* For JUNO experiment, there is a tool called `junoenv`.
* For nEXO experiment, there is a tool called `nexoenv`.



