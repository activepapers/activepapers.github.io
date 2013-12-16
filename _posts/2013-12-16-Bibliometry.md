---
layout: post
title: ActivePapers in bibliometry
author: Konrad Hinsen
comments: true
---

An often overlooked feature of ActivePapers is the possibility to use
the references in an ActivePaper in bibliometry. Before going into the
details, I need to make one point clear: Like many scientists, I have
a strong dislike for how bibliometry is done and used today, in
particular when it is used as a substitute for evaluating the quality
of scientific work. But (1) there are many ways to improve bibliometry
and (2) for some purposes it is actually a very reasonable approach.

One problem with today's bibliometry is that ignores everything that's
not a paper. In particular, it ignores published datasets and
published scientific software. This problem is currently being solved
by archiving sites that store such products and hand out
[DOI](http://en.wikipedia.org/wiki/Digital_object_identifier)s for
them. Examples of such sites are [figshare](http://figshare.com/),
[Zenodo](http://zenodo.org/), or [Dryad](http://datadryad.org/).

However, that's only a partial integration of software and data into
the bibliographic citation network. A paper cites other papers, for
example papers that it builds on. In the same spirit, software should
cite other software that it builds on (more commonly known as
"libraries"), and datasets that are derived from other datasets
(i.e. everything that's not raw observations) should cite the data
from which they were computed, and also the software used for the
computation. Unfortunately that's technically difficult to do, because
the common formats for storing datasets and software do not provide
metadata storage that could be used for citations.

ActivePapers stores a complete dependency graph for everything,
software and data. This dependency graph is needed for recomputing
data and for downloading external dependencies. The technical term
"external dependency" means exactly "earlier work that I build on",
and it covers both datasets and software libraries, since both can be
published as ActivePapers. These references to external dependencies
are thus exactly what is required for fully integrating scientific
software and data into the citation network.

What motivated me to write this post is Daniel S. Katz' paper on
[Citation and Attribution of Digital Products](http://dx.doi.org/10.6084/m9.figshare.791606),
presented at the recent
[WSSSPE workshop](http://wssspe.researchcomputing.org.uk/wssspe1/).
Dan argues that digital products (data and software) need to become
part of the citation and attribution system of the scientific
community in order to provide an incentive for scientists to publish
them in the first place. This is very much in line with the
ActivePapers philosophy. Dan adds the interesting idea of "fractional
credit": every scientific publication (paper, data, software) should
contain a statement which fraction of the total credit for the work
should go to each of the listed authors and to each of the cited
material. For example, a computational study could attribute 30% of
the total credit to each of the two authors and 40% to the software
that was used. The software could then attribute 80% of the credit for
itself to its author (assuming a single one) and 20% to a library that
it builds on. This system would ensure the attribution of credit in
particular for infrastructure software (mostly libraries) that
scientists use indirectly, sometimes without even being aware of it.

This fractional credit system sounds like an interesting idea, which
would be very easy to implement in the ActivePapers system. Consider it
placed on the ActivePapers to-do list.
