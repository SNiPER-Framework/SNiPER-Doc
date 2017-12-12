# Installation

In this part, we will introduce how to install SNiPER.

The source code of SNiPER is open-source. The public SNiPER repository can be found in [IHEP gitlab](http://gitlab.ihep.ac.cn/zoujh/sniper). For several experiments using SNiPER, they have their own requirements, so the source code is private and installation is done by their own tools.

## General SNiPER

To build SNiPER, we need several libraries and tools installed:

* CMT, configuration management tools
* Python, python-devel
* Boost, boost.python
* Intel TBB, for parallel computing



## Experiments-specific SNiPER

* For JUNO experiment, there is a tool called `junoenv`.
* For nEXO experiment, there is a tool called `nexoenv`.
