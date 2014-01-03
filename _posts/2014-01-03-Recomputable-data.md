---
layout: post
title: Storing recomputable data
author: Konrad Hinsen
comments: true
---

A frequent question I get asked when presenting ActivePapers is
"What's the point of storing results of computations? If you keep the
code, you can just re-run it. All you need to store is code and input
data." The short answer to this is that it is true in theory but a bit
less true in practice. For the long answer, read on. You will also
learn how ActivePapers can help you both with storing and non-storing
recomputable data.

First, let's get the obvious reason for storing recomputable data out
of the way: the computation may be too costly to be run
repeatedly. That's a classical case of a tradeoff between
(re-)computation time and use of disk storage. In many cases, a good
compromise is to keep the resulting data for a while, in order to be
able to do a quick analysis on it if you have a new idea, but not
archive it for long-time storage.

Next, a less obvious reason, and moreover a reason we don't really
like to be reminded of: the computation may not be as reproducible as
it should be. Programs that produce slightly different results
depending on the platform they are run on (OS, compiler version, ...)
are actually quite common. Programs that use floating-point arithmetic
almost inevitably fall into this category. It gets particularly bad
when the differences between two runs of the program are so different
that the conclusions drawn from the results change. Yes,
[this happens](http://scitation.aip.org/content/aip/journal/cise/14/1/10.1109/MCSE.2011.21).

Finally, there is a very frequent situation in which storing the
output data of a computation is not important, but storing the
associated metadata is. And that's where ActivePapers really shines.
That situation occurs when your recomputable output is really
*intermediate* data in your complete workflow. For example, you run
some simulation that produces some lengthy trajectory, then you run
some analysis on the trajectory, from which you generate a plot.  The
plot is your final result, so you want to keep it. The trajectory and
the raw analysis are intermediate results, which you do not have to
store unless it falls into one of the two categories explained above.
But you do want to store the fact that your plot was generated from
your raw analysis which in turn was generated from the simulation
trajectory. With that information, you, and anyone else looking at
your work later, can easily verify that the plot actually corresponds
to the latest version of your simulation and analysis code.

ActivePapers provides "dummy datasets" for dealing with this
situation.  A dummy dataset contains no actual data, but it does have
all the metadata that ActivePapers generates during the execution of
codelets. In the current state of ActivePapers, the only way to
generate such a dummy dataset is to first generate a real dataset,
then run all the calclets that use it as input, and in the end
replace the real dataset by a dummy dataset using `aptool dummy ...`.
The [tutorial](http://www.activepapers.org/python-edition/tutorial.html)
also mentions dummy datasets and shows how to recompute the original data.

There is plenty of room for future improvements of the user interface
to dummy datasets. For example, the calclet that creates a dataset
could mark it as a dummy immediately, and then it would never be
written to the file but passed to client calclets in memory. If you
have any ideas for this, please open an issue on the
[Github issue tracker](https://github.com/activepapers/activepapers-python/issues).

