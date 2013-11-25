---
layout: default
title: ActivePapers
---

## ActivePapers - computational science made reproducible and publishable

ActivePapers is a research and development project whose aim is to
make computational science more reliable.

### The ActivePapers principles

#### 1. Data is more important than software

Computational scientists usually first choose the software for doing
their work, and then let the software decide how to store the data
they work on. But data is both more fundamental and more long-lived
than software. A protein structure or a temperature field will make as
much sense in fifty years as it does today, but the software used to
produce it will probably be obsolete by then. Data should be stored in
well documented and software-independent formats.

#### 2. Code is data

We tend to think of code as the "active" part of computation and
consider data the "passive" one: computation works on input data and
generates output data. But code is really just yet another form of
data: a set of instructions that define a computation. And since code
is just data, why not store it along with the data it works on?

#### 3. Workflows are code

A workflow is nothing but the outermost layer of the algorithm that
defines a computational research project. It's code, and thus data,
and should be stored with the other data of the project.

#### 4. One project, one file

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
