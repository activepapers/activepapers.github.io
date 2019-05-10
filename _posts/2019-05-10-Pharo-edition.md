---
layout: post
title: The ActivePapers Pharo edition
author: Konrad Hinsen
comments: true
---

The ActivePapers family has a new member: the [ActivePaper Pharo
edition](http://www.activepapers.org/pharo-edition/). In contrast to
the [Python](http://www.activepapers.org/python-edition/) and
[JVM](http://www.activepapers.org/jvm-edition/) editions, which
implement mostly the same ideas and concepts on two different
platforms, the Pharo edition pursues a different goal: exploring
the human-computer interface of reproducible, understandable, and
verifiable computer-aided research.

One of the most frequent questions I received concerning the Python
edition of ActivePapers was: "Does this work with Jupyter notebooks?"
Initially my answer was "Not yet, but I am working on it." And I did.
However, that work never led to a satisfying result. One reason was
technical obstacles. I had tried to include Jupyter notebooks inside
an ActivePaper, but that turned out to be impossible because Jupyter's
two-process design (the kernel and the notebook editor are separate
processes connected by a communication protocol) was not compatible
with the HDF5 library's restriction that only one process can write to
a file at any time. And that means you cannot store a notebook and the
results it computes into the same HDF5 file.

However, the more I thought about integrating ActivePapers and
Jupyter, the more I realized that its linear notebooks (a sequence of
code, documentation, and result cells) are not really adapted to the
task of documenting a scientific computation, except for simple cases.
If you look at the various published ActivePapers, they invariably
contain multiple scripts plus a few library modules. Superficially, it
may seem that notebooks can replace the scripts and thereby provide
documentation. However, a good documentation must document the whole,
not some its parts. It must tie together multiple scripts and code
from the library modules. Usually computational methods are
implemented in the library modules, and the scripts apply them to
datasets. If the documentation is done script by script, how do you
document the methods?

Today there are plenty of published Jupyter notebooks, so how do they
deal with this? I didn't look at all of them, of course, but so far my
impression is that there are two cases. The most frequent case is
notebooks documenting data analyses based on standard well-known
methods implemented in well-known libraries. Readers of the notebook
are expected to be familiar with the methods, or to learn about them
elsewhere. The other case is notebooks including the full method
implementation. In addition to being limited to simple methods, this
approach has the big advantage that the method implementation is not
reusable.

Since my own research mainly focuses on developing and evaluating new
computational methods, I concluded that notebooks are not a good fit
for my work. In fact, I had come to that same conclusion by trying.
Whenever I started a new project as a notebook, I quickly switched to
old-style modules and scripts, with documentation in separate text
files. I found this to be a perfectly good enough technique for my
personal use, but a bunch of files, even well-organized, does not make
for something another scientist, even a collaborator, is eager to dig
into.

When I started to look at [Pharo](http://pharo.org/) a few months ago,
largely by accident (I signed up to the [Pharo
MOOC](http://mooc.pharo.org/) to get some MOOC experience from the
learner's point of view, before taking the role of an instructor in
the [Reproducible Research
MOOC](https://www.fun-mooc.fr/courses/course-v1:inria+41016+session02/info)),
I discovered a very different kind of interactive computing
environment. The Smalltalk family, of which Pharo is one of the
younger members, has a long history of valuing explorability and
understandability (see [this blog
post](https://blog.khinsen.net/posts/2018/12/19/exploring-pharo/) for
more details). Then I quickly discovered the [Glamorous Toolkit](https://gtoolkit.com/), a new interactive environment building on Pharo and aiming for an even higher
level of explorability through moldable development tools, the idea being that developers should be able to extend the environment with domain-specific inspection tools. The intellectual background of these ideas have been nicely summarized in a [blog post](https://osoco.es/thoughts/2019/05/designing-media-for-thought-with-moldable-development/) by Rafael Luque.

Compared to the current and future environments of the Pharo universe,
computational notebooks feel very limited and constraining. Which
isn't really surprising considering their origins. Today's Jupyter and
RMarkdown are minor variations on the notebook idea introduced in the
early 1980s by [Mathematica](https://www.wolfram.com/mathematica/).
Mathematica in turn, like most other computer algebra systems, built
on the heritage of Lisp, which in the 1950s introduced many
revolutionary features into computing, among which interactivity via
the Read-Eval-Print Loop (REPL) that was a natural way to implement
interaction within the constraints of the user interface hardware of
the time: a line-oriented terminal. Smalltalk, on the other hand,
started out in the 1970s with graphical displays and pointing devices
right from the start, at the price of depending on hardware that at
the time very few people had access to. As Marshall McLuhan taught us,
first we shape our tools and then our tools shape us. The
line-oriented terminals of the 1950s have imprinted a way of thinking
on computer users that even today's computational notebooks have
retained, in spite of superior approaches having been around for
decades. And that superior technology is not merely Smalltalk, which
has always remained a niche system. Non-linear GUIs is what we all use
for working with images or sound files. Those tasks are almost
impossible to do in a line-by-line way, so they didn't really happen
before GUIs. For computations, GUIs probably came too late: linear
thinking had already become a cultural norm.

The Pharo edition of ActivePapers aims at molding the GToolkit
environment into an environment for doing computing-aided research,
rather than software development.  These two activities are distinct
but share many common features. The main difference is that science
focuses on data and on models, with software being only a means to an
end. However, it's such an important means that everything else is
structured around it. Moreover, software development also deals with
data (about software) and models (as specifications). In the end, the
differences are gradual rather than fundamental. This journey has just
begun, and I don't really know where it will lead. Stay tuned for
updates! In the meantime, you can watch [this demo video](https://peervideo.net/videos/watch/4022a2cf-2b22-4a1c-935e-bf80724d3970).

