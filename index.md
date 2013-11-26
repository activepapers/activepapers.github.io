---
layout: default
title: ActivePapers
---

## ActivePapers - computational science made reproducible and publishable

ActivePapers is a research and development project whose aim is to
make computational science more open and more reliable, by making
comutational reproducible and publishable.


### The ActivePapers design criteria

An ActivePaper is a file combining datasets and programs working on
these datasets in a single package, which also contains a detailed
history of which data was produced when, by running which code, and on
which machine. It is a complete record of the state of a computational
research project that can be shared among collaborators and in the end
published as supplementary material to a journal article.

The development of ActivePapers was guided by the following principles:

##### 1. Data is more important than software

Computational scientists usually first choose the software for doing
their work, and then let the software decide how to store the data
they work on. But data is both more fundamental and more long-lived
than software. A protein structure or a temperature field will make as
much sense in fifty years as it does today, but the software used to
produce it will probably be obsolete by then. Data should be stored in
well documented and software-independent formats.

##### 2. Code is data

We tend to think of code as the "active" part of computation and
consider data the "passive" one: computation works on input data and
generates output data. But code is really just yet another form of
data: a set of instructions that define a computation. And since code
is just data, why not store it along with the data it works on?

##### 3. Workflows are code

A workflow is nothing but the outermost layer of the algorithm that
defines a computational research project. It's code, and thus data,
and should be stored with the other data of the project.

##### 4. One project, one file

The typical setup in computational science consists of a directory per
project containing all the data, scattered over many files, some of
the code, the rest being "installed" elsewhere on the computer.
Workflow information is sometimes stored in the scientist's brain
(interactive shell commands, actions in a graphical user interfaces)
rather than explicitly in the computer. For any non-trivial project,
this quickly turns into a mess. Which data files are up to date?
Which version of the program A was installed when script B was run?
On which computer was file X produced? Who changed script C yesterday?
All this confusion can be eliminated by storing all project
information in a single file, with the consistency of the contents
verified by the computer. This single file can be copied between
machines, shared among collaborators, and in the end published
for consultation and reuse by fellow scientists around the world.

##### 5. Re-use is a form of citation

Scientists have always built on other scientists' work. In
computational science, this means re-using other scientists' datasets
and software. This works smoothly only through precise
machine-readable references, such as DOIs (Digital Object Identifiers).
Another advantage of machine-readable references is the integration
of data and code references into bibliometry, creating the missing
incentive for scientists to actually publish data and code.

##### 6. Security matters.

Reproducible research invites scientists to download their peers'
computational code and run it. But running downloaded code without a
careful inspection is risky: the code might destroy information on the
computer it runs on, or transfer sensitive information to someone
else. While malicious code is at this time not a major concern in the
scientific community, defective code is not uncommon. ActivePapers
provide a closed universe, isolated from other data on a user's
computer and from the Internet, in which defective and malicious code
can do no harm.

##### 7. Research moves at a slower pace than computing

In the natural sciences, researchers typically consult original
journal publications that are up to about thirty years old, whereas
they turn to textbooks and review articles for older work.
Published computational science must therefore remain useable
for a few decades. Computing environments evolve at a much
faster pace, which is why software requires maintenance
to remain useable for more than a few years. Computational
science therefore requires a [stable computing platform]
(http://khinsen.wordpress.com/2013/08/14/platforms-for-reproducible-research/).


### ActivePapers in practice

There are currently two implementations of the ActivePapers
concept: the [Python edition](./python-edition/) and the
[JVM edition](./jvm-edition). The Python edition is the more
immediately useful one for most computational scientists, but
the JVM edition is a more complete implementation of the
principles listed above.

Both ActivePapers implementations use
[HDF5](http://www.hdfgroup.org/HDF5/) as the underlying storage
format. An ActivePaper is thus an HDF5 file. Datasets in an
ActivePaper can be inspected using many generic HDF5 tools, in
particular [HDFView](http://www.hdfgroup.org/hdf-java-html/hdfview/).
HDF5 has the advantage of providing compact binary storage for large
datasets and efficient access to them. This makes ActivePapers
suitable for working with Big Data.
