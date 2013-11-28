---
layout: default
title: ActivePapers Python edition
---

## The ActivePapers Python edition

The Python edition is the most practically useful implementation of
the ActivePapers concept, because it can build on the very well
developed ecosystem for scientific computing in the Python language,
which offers libraries for many scientific application domains.
However, the Python platform also imposes a few limitations:

 1. The restrictions on calclet execution cannot be strictly
    enforced. Circumventing the rules is possible, but unlikely
    to happen by accident. Users should inspect the code in a
    downloaded ActivePaper before executing it, or run ActivePapers
    in a virtual machine where malicious code cannot do any harm.
    
 2. Reproducibility is limited, as the same Python code can produce
    different results with different versions of Python or one of the
    libraries on which ActivePapers depends (NumPy, HDF5, h5py and
    their respective dependencies). The Python platform has no
    formal specification and a history of regular minor incompatible
    changes. ActivePapers records the versions of all dependencies,
    but re-creating an identical environment a few years later may
    become a challenge.
 
 3. Many popular libraries for scientific computing contain extension
    modules and can therefore not be packaged as ActivePapers. They
    can be used as external dependencies, but this increases the
    number of dependencies that every user must install before being
    able to use an ActivePaper, and it reduces reproducibility.

For a first impression of ActivePapers, see the [tutorial](tutorial.html).
Following the tutorial requires a working ActivePapers installation,
which you will get by following the [installation notes](installation.html).

The development of the ActivePapers Python edition is
[hosted on Github](http://github.com/activepapers/activepapers-python).

### Compatibility and dependencies

ActivePapers supports both Python 2.7 and the Python 3.x series
starting with 3.2. Since Python 2 and Python 3 are not fully compatible
languages, a given ActivePaper may work with only one of them.

ActivePapers depends on [NumPy](http://numpy.scipy.org/) (tested
with 1.6 and 1.7) and [h5py](http://www.h5py.org) (at least 2.2,
tested with 2.2). The current release also requires tempdir (tested
with 0.6), but this is a non-essential dependency that may disappear
in the future.
