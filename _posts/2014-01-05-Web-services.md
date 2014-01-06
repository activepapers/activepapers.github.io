---
layout: post
title: Reproducible research with Web services
author: Konrad Hinsen
comments: true
---

Web services are becoming more and more popular in scientific
computing.  There are already lots of Web sites where you can upload
some data, push a button to run a computation, and download the
results. Sometimes a computational Web service is integrated with a
database, so you don't even have to upload any data. You type in some
search, push a button, and get your data. The computation is done
somewhere in the cloud.

Web services are becoming popular because of their convenience. For
the user, there is no software to install. For the software developer,
there is no distribution or packaging, and no more trouble with users
refusing to upgrade to the latest version. Moreover, convenience for
users means more users and thus more citations for the software. On
the development side, there is a price to pay, of course, because the
Web layer needs to be developed in addition to the computational
software. But a good desktop user interface is a lot of work as well,
so in the end the Web service may well be the easier option.

So in the end, everybody wins, which is why Web services are becoming
so popular. And they all lived happily ever after...

Well, not quite. There is one big problem with Web services for
scientific computing: in terms of reproducibility, they are a
disaster. The statement "the results in table 1 were obtained from the
Web service at http://..." in a scientific publication is almost as
informative as "table 1 was dictated by the Oracle of Delphi". Well,
almost, there are two important differences. First, a reference to the
Oracle of Delphi would lead to certain rejection of the paper by any
serious journal, whereas a reference to a Web service is considered
normal.  Second, Web services usually do come with a citable
publication that explains what they do and provide a summary of the
algorithms used. Still, Web services are the ultimate black boxes of
scientific computing: you get a result but neither a version number
nor an archivable copy of the current source code. A colleague trying
to reproduce your work a month later may well get different results
from the same input, without any explanation.

However, there is absolutely no *technical* reason why computations
through Web services should not be reproducible. They are not because
their clients don't ask for reproducibility. As soon as scientific
journals start rejecting submissions that are not fully reproducible,
we will have Web services providing reproducible results. Trust me,
it's [Pythia](https://en.wikipedia.org/wiki/Pythia) herself who told
me.

After all, a Web service is just a Web-based user interface to
computational software. If software on your personal computer or on
your computing cluster can deliver reproducible results, so can a Web
service. Nothing prevents Web service providers from putting their
source code on [Github](http://github.com/) and the commit number for
the exact version that was used into every result file offered to the
user for download.

That's still not quite the end of the story. Imagine a near future
with lots of computational Web services, and users (or scripts they
write, or meta-services) feeding the results from one Web service into
the next Web service. This leads to exactly the same problem of
workflow logging and provenance tracking that we have today when using
a chain of traditional software on a desktop computer. Users or their
workflow management software will have to figure out which result was
produced from which input using which Web service, and figure out
everyone's version numbers. Wouldn't life be easier if this happened
automatically? If every file passed around between Web services
contained a complete trace of its origins, including references to the
software that was used?

That's where ActivePapers enters the stage. Imagine the following
scenario. You prepare your input data in Excel 2020 and select
"publish on figshare in ActivePapers format" from the menu. A DOI pops
up, which you paste into your first Web service. The Web service does
its computation on the data, using its computational software that is
also published as an ActivePaper. What it sends back to you (or
directly to your figshare account) is an ActivePaper as well, with
references to your input data and to the software that was used.
Ready to be fed into the next Web service. Provenance tracking is
integrated into the workflow itself, and stored along with the data.

Now, finally, everybody wins. Scientists run computations without
installing software and without worrying about data management.
Software developers do exactly what they do now: develop computational
software plus Web interfaces. They don't have to worry about data
management either because the decentralized ActivePapers infrastructure
takes care of that. And science was reproducible ever after.
