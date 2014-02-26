---
layout: post
title: Software maintenance in research
author: Konrad Hinsen
comments: true
---

Software maintenance is one of the difficulties that developers of
scientific software face regularly. It's an important activity, but it
can take a lot of time and it's hardly rewarded by today's evaluation
procedures. And if you are manging a big software project, getting
funding for maintenance is usually difficult.

Given that software maintenance is difficult and not intrinsically
of scientific interest, we should ask ourselves the question of
why it is necessary, and if we can do something to reduce the need
for maintenance.

First of all, what is software maintenance?
[Merriam-Webster](http://www.merriam-webster.com/dictionary/maintain)
defines the verb "maintain" as

> to keep (something) in good condition by making repairs,
> correcting problems, etc.

This makes sense for technical equipment that deteriorates over time
due to mechanical wear etc. Software doesn't deteriorate, so
maintenance must mean something different when applied to software.  I
am not aware of any concensus definition, so what I give here is my
own: Software maintenance consists of modifying software for one of
two reasons:

  1. Fixing bugs.
  2. Keeping the software usable in evolving computing environments.

Some people would add functional enhancements to this list, but those
are not really maintenance in any sense, but improvements. In
particular in the case of scientific software, where new functionality
often means new science.

First, bugs. As with any software, we want bugs in scientific software
fixed in order to get better results in the future. However, we also
want to keep the buggy version around if any published scientific
study has used it. This is simply a question of honesty and
preservation of the scientific record: if there's a chance that the
outcome of a study is influenced by a bug in the software, people
looking at the study should be able to find this out. They should have
access to the exact same software that was used originally, not just
to today's improved successor. For this reason, it is actually more
important to preserve the code that was used in a study than to fix
bugs. ActivePapers was designed with this goal in mind: any computed
data item in an ActivePaper is linked to the software that produced
it. Moreover, this link is strictly unmodifiable after publication,
since ActivePapers are published just like electronic copies of
articles and referenced through DOIs. You _can_ cheat before
publication, by modifying an ActivePaper with the specific intention
of committing fraud. ActivePapers doesn't support such actions, but
doesn't make any effort to prevent fraud either. Such features could
be added by protecting provenance information with hashes, but I hope
this won't be necessary.

The second problem, evolving computing environments, is a more subtle
one. It's a fact of life that everything in the computer world
(computers, operating systems, compilers, language definitions,
libraries, ...) changes at a fast pace, with the result that a given
piece of source code is unlikely to work as-is a few years later. This
happens because of two reasons: (1) technical progress permits ever
better computers and software, which is what people want, and (2)
nobody has a vested interest in the stability of computing platforms
**and** the power to make it happen.  For hardware vendors and
suppliers of commercial software, rapid change is the best way to
ensure that customers buy new machines and update their licenses
regularly.

There is, of course, at least one community that has a vested interest
in the stability of computing platforms: the computational science
community. If we could run our software 20 years later, without
modification, and get the same results, we'd be happy. We don't want
to do software maintenance, and most of us cannot reasonably maintain
the software they develop for their own research beyond their
immediate personal needs. It's even less reasonable to expect anyone
to maintain somebody else's software, for example the software left by
the graduate student who now works in industry. In practice, only
widely used community software gets maintained over sufficiently long
periods. But even research projects using widely used and maintained
packages usually also require some project-specific software, at the
very least a couple of shell scripts. And that's one reason why the
reproducibility of computational studies is so bad.

Could the scientific community do something about this? I believe it
can, but I am not optimistic that it will take action in the near
future. It is probable that scientists will continue to use commodity
hardware for scientific computing, meaning that they will have to
accept the evolution of hardware and the associated systems software,
which is out of their control. However, they can build a stable
platform on top of these ever evolving ones, at least for the purely
computational part of their work. At a fundamental level, all
Turing-complete notations for software are equivalent and can be
converted into each other. In practice, performance considerations
impose a limit to code conversion, but it is still possible to define
a code representations that can be translated efficiently to all kinds
of underlying hardware and systems software and thus remain
stable. Two real-life examples are
[JVM](http://en.wikipedia.org/wiki/Java_virtual_machine)
[bytecode](http://en.wikipedia.org/wiki/Bytecode) and
[LLVM](http://llvm.org/)'s
[intermediate form](https://en.wikipedia.org/wiki/Intermediate_form).
JVM bytecode has been around for 20 years and has proven to be
extremely stable. LLVM's intermediate form is not meant to be stable,
but that's because LLVM's developers don't want to limit their future
options by committing to a stable representation.  Google's
[PNaCl](http://www.chromium.org/nativeclient/pnacl) project tries to
ignore this warning and use LLVM code in a way that makes sense only
if it remains stable. Time will tell how this will work out.

The scientific community could define its own intermediate code
representation, building on the experience with existing approaches,
and optimizing their platform for scientific applications. But, as I
said above, I am not optimistic that this will happen. Two
requirements would be a long-time commitment by several large research
and funding organizations to maintain this platform over many
decades. I am convinced that this would be economically reasonable,
because I am certain that maintaining one platform is cheaper than
maintaining lots of scientific software packages, and constantly
rewriting those that weren't maintained. But it would require a level
of agreement and commitment that is rare in science; it has only
happened for a few huge installations such as
[CERN](http://home.web.cern.ch/).

The important advantage provided by a stable platform is the reason why the
[first ActivePapers edition](http://www.activepapers.org/jvm-edition/)
was designed around the JVM. Unfortunately, the JVM is not very
popular in scientific computing. This is often explained by a lack of
performance, although that argument is no longer as valid as it used
to be. There are also a few design problems, in particular concerning
floating-point operations, but then the same can be said about popular
languages like C or C++, which hasn't kept scientists from using them.

The practically more useful
[Python edition of ActivePapers](http://www.activepapers.org/python-edition/)
is built on a platform defined by the Scientific Python ecosystem (in
particular Python, NumPy, and h5py). This platform has proven to be
moderately stable in the past, with the transition to Python 3 being
the major event of instability. The time scale over which scientific
Python code can be used without maintenance is probably a few years.
That's not good enough in my opinion, and I hope that the community
will take stability more seriously in the future.
