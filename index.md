---
layout: default
title: ActivePapers
---

## ActivePapers - computational science made reproducible and understandable

ActivePapers is a research project about the future of science communication
in the context of the ever increasing importance of computing in scientific
research. The central question that ActivePapers wishes to answer is:

> **How should we package and publish the outcomes of
> computer-aided research in order to make them maximally useful
> to the scientific community?**

An *ActivePaper* is such a publishable package, which in general
contains documentation, code, and data.

The desirable properties for an ActivePaper are:

 - **Understandability** is primordial for communication. Readers
   should be able to understand, with as little effort as possible,
   what exactly was done and why. This includes in particular the
   computational models and methods that have been applied.

 - **Reproducibility** is a fundamental aspect of scientific quality
   control. Readers should be able to convince themselves, with as
   little effort as possible, that the computations in an ActivePaper
   are reproducible.

 - **Reusability** ensures that the outcomes of a research project
   can become the basis for future work. Readers should be able to
   use, with as little effort as possible, any item in an ActivePaper
   in their own work, referencing that ActivePaper to ensure both
   traceability and attribution of credit to its authors.

Exploring this research question involves designing, implementing, and
applying infrastructure software for computer-aided research. This
software is openly available, and everybody is welcome to use it in
whatever way. However, please be aware that these software packages
are research prototypes, not products.  Don't expect technical support
or long-term maintenance. We will do our best to help with potential
problems, but in the spirit of collaborative research rather than
customer support.

For keeping up to date with ActivePapers development,
follow [@ActivePapers](https://twitter.com/ActivePapers) on Twitter
and read [our blog](http://www.activepapers.org/blog.html).

### Scientific publications related to the ActivePapers project

 - "A data and code model for reproducible research and executable papers",
   [Procedia Computer Science 2011, 4:579](https://doi.org/10.1016%2Fj.procs.2011.04.061)

 - "ActivePapers: a platform for publishing and archiving computer-aided research",
    [F1000Research 2015, 3:289](https://doi.org/10.12688/f1000research.5773.3)

 - "Verifiability in computer-aided research: the role of digital scientific
   notations at the human-computer interface",
   [PeerJ Computer Science 2018, 4:e158](https://doi.org/10.7717/peerj-cs.158)

### ActivePapers in practice

The best platforms for publishing ActivePapers are currently
[Zenodo](http://zenodo.org) and [figshare](http://figshare.com/). You
can consult the list of ActivePapers available
[on Zenodo](https://zenodo.org/search?f=keyword&p="ActivePapers")
and
[on figshare](http://figshare.com/search?q=ActivePapers).

### ActivePapers infrastructure software

There are currently two implementations of the ActivePapers
concept: the [Python edition](./python-edition/) and the
[JVM edition](./jvm-edition). The Python edition is the more
immediately useful one for most computational scientists, but
the JVM edition is a more complete implementation of the
design goals outlined in the [first paper on ActivePapers](https://doi.org/10.1016%2Fj.procs.2011.04.061).

Both ActivePapers implementations use
[HDF5](http://www.hdfgroup.org/HDF5/) as the underlying storage
format. An ActivePaper is thus an HDF5 file. Datasets in an
ActivePaper can be inspected using many generic HDF5 tools, in
particular [HDFView](http://www.hdfgroup.org/hdf-java-html/hdfview/).
HDF5 has the advantage of providing compact binary storage for large
datasets and efficient access to them.

### Core ideas and concepts of ActivePapers

##### Reproducibility by construction

Today's most common approach to ensuring computational reproducibility
is to do a computation and then check if its results are reproducible.
Such a check requires significant competence and effort, and as a
consequence it is rarely done, in particular for long-running
computations. The best evidence is that reviewers for scientific
journals are not expected to check for reproducibility. ActivePapers
pursues a different approach: the infrastructure software guarantees
the reproducibility of the results stored in an ActivePaper. This
requires authors to adopt a new tool for their work, but removes the
need to check reproducibility.

##### Data is more important than software

Computational scientists usually first choose the software for doing
their work, and then let the software decide how to store the data
they work on. But data is both more fundamental and more long-lived
than software. A protein structure or a temperature field will make as
much sense in fifty years as it does today, but the software used to
produce it will probably be obsolete by then. Data should be stored in
well documented and software-independent formats.

##### Code is essential documentation for data

Good data formats go a long way to document the meaning of a dataset,
but they cannot provide the context in which a particular dataset was
produced. For computational results, the ultimate documentation is the
code that produced the dataset. This code should thus be easily
accessible from the dataset itself.

##### The code-data dichotomy is not fundamental

The distinction between code as a tool and data as the virtual matter
manipulated by that tool is little more than an historical accident of
computing technology. What matters more for science is the distinction
between the different kinds of scientific information:

 - human input: scientific models and methods,
   including parameter choices
 - observational data
 - results of computations

Today we often neglect the distinction between observational data and
computed results, calling both "data". We also sometimes put parameter
choices into the "data" category, and bury small datasets in software
source code for practical convenience.

##### Re-use is a form of citation

Scientists have always built on other scientists' work. In
computational science, this means re-using other scientists' datasets
and software. This works smoothly only through precise
machine-readable references, such as DOIs (Digital Object Identifiers)
or, better yet, intrinsic identifiers based on the concepts of
content-addressable storage. Such machine-readable references can also
be used to integrate data and code references into bibliometry,
creating the missing incentive for scientists to actually publish data
and code.

##### Research often moves at a slower pace than computing

In the natural sciences, researchers typically consult original
journal publications that are up to about thirty years old, whereas
they turn to textbooks and review articles for older work.
Published computational science must therefore remain usable
for a few decades. Computing environments evolve at a much
faster pace, which is why software requires maintenance
to remain usable for more than a few years. Computational
science therefore requires [stable computing platforms]
(http://khinsen.wordpress.com/2013/08/14/platforms-for-reproducible-research/).
