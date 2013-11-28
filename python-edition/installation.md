---
layout: default
title: Installing ActivePapers
---

## Installing ActivePapers

### Anaconda

The fastest and easiest way to install the ActivePapers framework on
your computer is to start by installing the
[Anaconda Python distribution](https://store.continuum.io/cshop/anaconda/).
Note that you need Anaconda version 1.7 or later. Once you have
Anaconda installed, type the following command into a terminal window:

```
pip install tempdir ActivePapers.Py
```

In case you have multiple Python installations on your machine, make
sure you use the command `pip` from the Anaconda installation.

### Debian and friends

On Debian Linux and derivatives such as Ubuntu, you can in principle
install all the prerequisites using

```
apt-get install python-h5py
```

and then proceed as above with

```
pip install tempdir ActivePapers.Py
```

However, the current stable Debian distribution (7.x, code name "wheezy")
contains a rather old version of h5py which is not sufficient for using
ActivePapers. Until Debian updates h5py to version 2.2, you can use

```
apt-get install python-dev python-pip python-numpy libhdf5-7 libhdf5-dev
```

followed by

```
pip install h5py tempdir ActivePapers.Py
```


### Other Python installations

If you prefer to work with a different Python installation, make sure
you have the following packages installed on your computer:

 * [Python](http://www.python.org/) 2.7, or Python 3.2 or later
 * [HDF5](http://www.hdfgroup.org/) 1.8.9 or later
 * [NumPy](http://www.numpy.org/) 1.6 or later
 * [h5py](http://www.h5py.org/) 2.2 or later
 * [tempdir](https://pypi.python.org/pypi/tempdir/0.6) 0.6 or later

You can then install ActivePapers.Py by following the instructions
given in the source code distribution.

Please note that Python 2.x and Python 3.x are somewhat different
languages and not fully compatible. While the ActivePapers framework
works with both versions, the code in a given ActivePaper may well
require one or the other version specifically. At this time
(autumn 2013), Python 2.x is still more widely used than Python 3.x
in the scientific community.
