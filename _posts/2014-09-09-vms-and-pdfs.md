---
layout: post
title: Virtual Machines and PDFs: future relics of the past
author: Konrad Hinsen
comments: true
---

A recent tweet by Greg Wilson hits the nail on the head:

<blockquote class="twitter-tweet" lang="en"><p>VM images are just PDFs you can run. If we use &#39;em for reproducibility today, ppl will have to hack tools to mine their content tomorrow.</p>&mdash; Greg Wilson (@gvwilson) <a href="https://twitter.com/gvwilson/status/508402669825060864">September 6, 2014</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

In fact, both virtual machines and PDFs were designed for a very
specific purpose, but that purpose is not scientific publishing. PDFs
were designed for capturing the exact contents of printed paper pages
in a computer file. There are very good reasons for doing this, of
course, and that's why PDFs became popular. Virtual machines were
designed to make a complete software stack, from operating system to
application software, transportable from one physical computer to
another. There are very good reasons for doing this as well, which is
why virtual machines became popular.

Both PDFs and virtual machines were adopted for scientific publishing
out of convenience: they were well-established technologies that
seemed to correspond to an immediate need. PDFs replaced printed paper
as the publishing medium for science in what was a minimal transition
to electronic publishing: only the medium was replaced. But electronic
publishing would allow much better: raw data and computational methods
could be machine-readable and thus reusable by others. Virtual
machines provide a low-effort way of archiving and publishing
computations in a minimal way, requiring no change to the software and
file formats we use today. But again a big chance is missed to do
better, and make data and code accessible and reusable.

ActivePapers was specifically designed to address these issues, and it
is perhaps the first file format designed with the needs of scientific
publishing as its top priority. An ActivePaper combines datasets and
the code that works on it, in a way that permits reusing one or the
other (or both, of course) in a fully tracable way. For doing science
not only reproducibly, but also openly, that's very important.


