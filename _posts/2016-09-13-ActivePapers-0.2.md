---
layout: post
title: New features in ActivePapers 0.2
author: Konrad Hinsen
comments: true
---

The [latest release](https://pypi.python.org/pypi/ActivePapers.Py/0.2) of the ActivePapers Python edition has two new features that deserve some more explanation than is given in the [release notes](https://github.com/activepapers/activepapers-python/blob/3a61045b3f63bcd3cb45136c95b3e4da0a827b2a/doc/RELEASE_NOTES.md).

The first new feature is the possibility to use an ActivePaper from a plain Python script (or a [Jupyter notebook](https://jupyter.org/)) that lives outside of the ActivePapers universe. After opening an ActivePaper, the Python code can access its data and use its Python modules exactly like a calclet or an importlet. The only restriction is that all access is read-only, because an external script or notebook cannot be a dependency of a dataset.

One typical use case for this feature is a presentation of data computed in an ActivePaper in the form of a supplementary Jupyter notebook, as illustrated by [this example](https://github.com/activepapers/activepapers-python/blob/master/examples/Water%20diffusion.ipynb). This is not yet the level of integration I would like to see between ActivePapers and notebooks, but it's a start. You can look at this integration from two points of view. To the ActivePapers user, it provides access to the advanced data exploration and visualization features of Jupyter notebooks. To the Jupyter user, it provides a way to package and publish problem-specific data and code than can then be used in a notebook without any prior installation or explicit download. If you look more closely at the example, you will notice that it opens an ActivePaper through its DOI. This means that the ActivePaper is automatically downloaded from figshare when the notebook is run.

The second new feature is code introspection in calclets. This may sound very technical and a bit obscure at first, so let me explain its utility via two ActivePapers that make use of this feature. The first is a [unit testing framework](https://doi.org/10.5281/zenodo.61693), the second a [support package for literate programming](https://doi.org/10.5281/zenodo.61695).  The unit testing framework locates extracts unit tests from Python modules in an ActivePaper, runs them, and generates a report that is a standard ActivePaper dataset. This means that after any code change, the tests will automatically be re-run when the ActivePaper is updated. Literate programming for ActivePapers is very basic for now: You write comments using Markdown syntax, and the code in the support package turns the code and comments into a readable document that can also include results, including pictures.

If "unit testing framework" makes you think of [nose or py.test](http://pythontesting.net/), you are in for a surprise: the ActivePapers version consists of a single Python module and just 33 lines of code. Of course this does mean that it's much more basic than its bigger brothers. But more importantly, it indicates a very different philosophy. The ActivePapers unit testing framework is not meant to be a black-box tool with tons of features, but a piece of code simple enough that users can read and understand it. If you miss a feature, go add it yourself. If every ActivePaper ends up using its own modification of the code, so be it. In the context of scientific computing, understandable code is what matters most. In the same vein, I have no intentions whatsoever to support or maintain this module. Use it, read it, understand it, modify it, in any way you want, just as I will do myself in the future. The literate programming support is similarly basic: one module, 60 lines of code, and the same comments apply.

The two small packages do come with documentation and examples, however. If you are interested in either one, download the ActivePaper, type
```
aptool checkout
```
and browse through the few files in there.
