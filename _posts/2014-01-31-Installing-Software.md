---
layout: post
title: Does installing software have to be like playing Tetris?
author: Konrad Hinsen
comments: true
---

One of the eternal headaches of computer users is the installation of
software. This is particularly true in computational science, where
ready-to-run software distributions for the major computing platforms
are rare, and unusual computing platforms abound. The typical
scientific software package is distributed as source code that needs
to be compiled and installed. The compilation and installation
procedure must frequently be hand-tuned for a specific computing
platform.  To make things worse, each software package comes with a
list of dependencies, which are other software packages that must be
installed first. It is not uncommon to spend an entire day with the
installation of a non-trivial software package, and it is not uncommon
either to give up after a series of failures.

To see why software installation is so hard, and how it can be
improved, it helps to have a close look at the two main world views
about how application software (the software that solves your problem)
interacts with systems software (the software that comes with your
computer). I will call them the "Tetris model" and the
"platform-content" model.

## The Tetris model

In the [Tetris](http://www.tetris.com/) model, every piece of
software, i.e. every library or application program, is like a piece
in a Tetris game: it has a very specific shape and thus fits only into
a very specific place in a landscape. The landscape is defined by the
computer hardware and all the software already installed on the
system. A software package's installation instructions describe the
landscape that it expects: the dependencies that must be preinstalled,
the system tools that must be present, etc. Minor mismatches can be
eliminated manually with a chisel, meaning by editing configuration
files. Major mismatches may prevent installation altogether, unless
modifications are made to the software which are beyond the average
user's competence.

In the Tetris model, there is no fundamental difference between
systems software and application software. Systems software is just
the part of the installation that the manufacturer has already
provided. Application software is considered a systems extension.

The Unix family of operating systems is the archetype of the Tetris
model. Each hardware platform and each Unix dialect defines a
particular landscape for the systems software, and each specific
collection of installed systems software defines a particular
landscape for application software.

The Windows operating system presents a more uniform landscape, but
still has a large variety of landscapes due to differences in Windows
versions and device drivers. If software installation is overall
simpler under Windows than under Unix, that's mostly due to a
difference in culture. The typical Windows user buys and installs
large preassembled units of software, and expects the vendor to do the
adaptation work to the different landscapes.  The typical Unix user
downloads free software from small producers, and accepts to do the
adaptation work himself. But both systems are based on the Tetris
model and suffer from its fundamental messiness.


## The platform-content model

The platform-content model is named after the principle of operation
of media players. To play music from an MP3 file, you need an MP3
player.  To read a PDF file, you need a PDF reader. In both cases,
there is a clear contract (the file format) that defines the tasks of
the platform (the MP3 or PDF software) and how the content (MP3 or PDF
file) must be constructed to obtain the desired result (music or page
of text) from playing the content on the platform.

In the computing world, it's the systems software that defines the
platform and the applications software that represents the content.
A clear contract defines the responsibilities of each part. Users
just copy the application to their computer and run it.

The first implementation of the platform-content model that I am aware
of is the Java Virtual Machine (JVM). "Write once, run anywhere" was
the slogan that Sun used to describe its new multiplatform programming
system nearly 20 years ago. The "anywhere" part required a very strict
platform definition. An application for the JVM takes the form of a
[jar file](http://en.wikipedia.org/wiki/Jar_file), which can be run on
any computer with a JVM installation.

More recent implementations of the platform-content model can be found
in MacOS X (application bundles) and on the mobile computing platforms
such as iOS or Android. The crucial difference between these systems
and Windows, which I have assigned to the Tetris category, is that
applications in the platform-content model are completely isolated
from each other. Windows applications have files in various public
locations, meaning that different applications, and in particular
different versions of the same applications, can be in conflict
because they want to put different information into the same file.

## Two extremes with a lot of middle ground

For clarity, I have painted a black-and-white picture above that
contrasts the two extreme approaches to software management.  Most
systems are somewhere in the middle, and even the difference between
the two extremes is not as big as it may seem initially.

Systems adopting the platform-content model effectively hide their
internal Tetris landscape from their users by packaging software in
shiny boxes. Application developers who produce Jar files or Mac
application bundles for their clients have to fight with much the same
problems as the systems administrators of Unix machines. Still, the
difference is important: the existence of a well-defined platform
limits the pain to a much smaller number of people.

The JVM running on Linux illustrates that it is possible to build a
platform-content model on top of a Tetris universe, but this
represents a major effort. In general, defining a good general-purpose
platform is a highly non-trivial job, and until now none has succeeded
completely. The problem is that a general-purpose platform is by
necessity rather complex. It's easy to overlook something, or write
down a slightly ambiguous specification. Sooner or later, someone will
exploit such weak spots, and application will be not work under some
conditions. There is also the temptation to permit application
developers to work around the platform's limitations in a
system-specific way, in order to gain in performance or functionality.
This is what has happened to the JVM platform and has given rise
to the parody "Write once, debug everywhere".

## Programming languages

Programming languages whose calling conventions differ from the
underlying operating systems (in particular, interpreted languages
that manage libraries in source code form) tend to have their own
library management systems that follow the same principles as
system-wide software management. The Python language, for example, is
a representative of the Tetris model.  Tools like
[virtualenv](https://pypi.python.org/pypi/virtualenv) have been
invented to work around some of the inconveniences of the Tetris
approach. What virtualenv does is set up "clean" standardized Tetris
landscapes that are independent of each other. Such a virtual
environment can be seen as a platform (defined by a specific version
of Python and its standard library), but it's not quite the
platform-content model because there is no straightforward way to
package and distribute content.

Languages based on a "system image" approach (most famously Smalltalk,
but many Lisps work the same way) come closest to the platform-content
model: the sytem image is the content, the runtime system is the
platform. However, system images are in practice not used for software
distribution, they are seen as an implementation detail.

The only languages I am aware of that adopt the platform-content model
are languages designed for the JVM and its younger cousin, Microsoft's
[CLR](http://en.wikipedia.org/wiki/Common_Language_Runtime), which
is better known under its commercial name .NET.

## What's the link with ActivePapers?

One of the roles of ActivePapers is publishing and archiving
scientific software, along with data. ActivePapers can accomodate both
scripts and libraries. It is therefore a platform for software
management, adopting the platform-content model. ActivePapers even
goes further than other platforms in proposing zero-installation
software assembly: dependencies are downloaded automatically when
needed.

In light of what I said above, this may seem like an overly ambitious
goal. However, I am confident that ActivePapers can keep its promises,
because it doesn't try to be a general-purpose platform, but a
domain-specific platform for scientific computing.

One important feature of ActivePapers is that the content is limited
to computations. Code in an ActivePaper has intentionally very limited
access to the computer it runs on: it sees only what it in the
ActivePapers universe. An ActivePaper cannot implement graphical user
interfaces, Web servers, or device drivers. This removes much of the
complexity of a general-purpose computing environment.

Moreover, ActivePapers is specifically designed for scientific
publications, and can therefore profit from the infrastructure of the
scientific community, in particular scientific repositories such as
[figshare](http://figshare.com) and [Zenodo](http://zenodo.org) and
the permanent references through DOIs that they provide.  This is how
ActivePapers achieves zero-installation deployment.

All is not perfect though, because the ActivePapers platforms has a
few leaks, which it inherits from the Python language it is built on.
While ActivePapers does what it can to prevent access to resources
outside of its universe, it cannot do enough, because Python provides
insufficient access control mechanisms. Another limitation is that
neither the Python language nor the two libraries that ActivePapers
depends on (NumPy and h5py) have formal specifications. They are quite
stable, but they do evolve over time. It is therefore possible that an
ActivePaper that works today stops working in the future because some
code in NumPy has changed. One possible solution is to define a unique
"ActivePapers platform" which consists of specific versions of the
underlying software packages. However, such a platform will survive
only as long as its constituents are maintained by its respective
authors.
