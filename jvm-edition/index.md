---
layout: default
title: ActivePapers JVM edition
---

## The ActivePapers JVM edition

The JVM (Java Virtual Machine) edition of ActivePapers comes closest
to the ideals of the ActivePapers project in terms of reproducibility
and secure execution of downloaded code. The only restriction concerns
reproducibility. The JVM specification does not fully specify the
semantics of floating-point operations, in order to permit the
efficient use of floating-point hardware.  Programs containing
floating-point operations may therefore produce different results on
different machines. Note, however, that this restriction currently
applies to all practically usable programming languages.

An important advantage of the JVM edition is its support for a wide
range of programming languages. Its main inconvenience is the lack of
popularity of the JVM for scientific computing. There is an
insufficient choice of existing libraries in most application domains.

The development of the ActivePapers JVM edition is
[hosted on Bitbucket](https://bitbucket.org/khinsen/active_papers).

### Compatibility and dependencies

ActivePapers depends on the Java Virtual Machine, requiring at least
version 1.6 (sometimes also called "Java 6"), and on
[JHDF5](http://wiki-bsse.ethz.ch/display/JHDF5) (at least version 11).
