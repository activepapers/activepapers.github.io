---
layout: default
title: ActivePapers tutorial
---

# ActivePapers tutorial

This short tutorial shows how to

 - inspect the contents of an ActivePaper
 - extract code and documentation (including plots)
 - modify parameters of the computation
 - modify the code
 - re-run computations
 - creating an ActivePaper from scratch

The example file for this tutorial can be
[downloaded](http://files.figshare.com/1216312/lysozyme_diffusion.ap)
from Figshare.  It's also a good idea to look at the
[description](http://figshare.com/articles/Model_free_simulation_approach_to_molecular_diffusion_tensors_Lysozyme/808594)
on the Figshare site. You do not need to understand what it does or
why, but if you are interested, feel free to look at the
[paper](https://www.researchgate.net/publication/257940340_Model-free_simulation_approach_to_molecular_diffusion_tensors)
describing the work, which is about computing the translational and
rotational diffusion tensors for a protein in solution from a
Molecular Dynamics trajectory.

Please copy the downloaded ActivePaper file to an empty directory.
Open a shell window, and go to that directory. When you type

    ls -l

you should see something like

    -rw-r--r--  1 hinsen  staff  148133188 Sep 26 16:21 lysozyme_diffusion.ap

## Inspecting the contents

    aptool ls

produces a long list of datasets, starting with

    code/correlation_functions
    code/diffusion_tensor
    code/identify_trajectories
    code/plots
    code/python-packages/fitting
    code/python-packages/molecular_structure
    code/python-packages/mosaic
    code/python-packages/quaternion
    code/python-packages/time_series
    code/python-packages/units
    code/thermal_averages
    code/trajectory_processing
    data/coordinate_trajectories/rotation_laboratory_frame_1
    data/coordinate_trajectories/rotation_laboratory_frame_10
    data/coordinate_trajectories/rotation_laboratory_frame_2

But how does `aptool` know which ActivePaper file you want to look at?
Well, if there is only one file with the `.ap` extension in the
current directory, that's the one it takes. And that's why it's a good
idea to use a separate directory for each ActivePaper project.
If for whatever reason you do not want to do this, you can pass the
ActivePaper filename explicitly:

    aptool ls -p lysozyme_diffusion.ap


You can get more information using

    aptool ls -l

yielding

    2013-06-07/09:13:05  calclet    code/correlation_functions
    2013-06-07/09:19:48  calclet    code/diffusion_tensor
    2013-06-07/10:02:29  calclet    code/identify_trajectories
    2013-06-12/08:03:48  calclet    code/plots
    2013-06-04/15:42:02  module     code/python-packages/fitting
    2013-05-02/15:11:53  module     code/python-packages/molecular_structure
    2013-06-14/15:46:18  reference  code/python-packages/mosaic
    2013-05-23/11:42:31  module     code/python-packages/quaternion
    2013-05-27/04:13:09  module     code/python-packages/time_series
    2013-05-02/15:12:07  module     code/python-packages/units

plus lots of more lines like that. The first column shows the date and
time of the last modification for each dataset. The second column
shows the type of the dataset. The above list contains two of the
types for executable code, `calclet` and `module`. There is a third
one not occuring in this list, `importlet`.

A module is just what you would expect as a Python programmer: a
Python source code file to be imported by other Python code. Calclets
and importlets are the two variants of scripts provided by
ActivePapers.  The most common type is the calclet, which is a Python
script with restricted rights: it cannot do any I/O outside of the
ActivePaper file it is contained in, meaning that it can access
neither files nor network resources. These restrictions ensure
reproducibility (all input data is guaranteed to be in the
ActivePaper) and protect the user agains bugs and malicious code.  But
they also mean that calclets cannot be used to import data into the
ActivePaper. That's where importlets come into play: they can use any
Python feature and access any resource. That also means that you
should not run somebody else's importlets without first looking at
them. The [[Calclets]] page tells you how to write calclets and
importlets.

There is one more dataset type in the list above: the reference, which
serves to refer to datasets in other ActivePaper files. A reference
consists of two parts: a reference to the file, and the name of the
dataset within that file. The file reference can be a DOI, for a
published file, or a local filename. Obviously local filenames don't
make sense on anybody else's computer, so local references are a bit
like importlets: they document where data comes from, but don't make
it available.

Let's look at the references in our ActivePaper:

    aptool refs

We find one DOI and ten local references:

    doi:10.6084/m9.figshare.705829
    local:lysozyme_spce_rbt_1
    local:lysozyme_spce_rbt_10
    local:lysozyme_spce_rbt_2
    local:lysozyme_spce_rbt_3
    local:lysozyme_spce_rbt_4
    local:lysozyme_spce_rbt_5
    local:lysozyme_spce_rbt_6
    local:lysozyme_spce_rbt_7
    local:lysozyme_spce_rbt_8
    local:lysozyme_spce_rbt_9

The DOI is for the pyMosaic library, version 0.1.1, as deposited on
Figshare. The local files are the simulation trajectories that are
analyzed in the ActivePaper. Lets get some more information about
these references:

    aptool refs -v

    doi:10.6084/m9.figshare.705829
      links:
        code/python-packages/mosaic
    local:lysozyme_spce_rbt_1
      copies:
        data/center_of_mass
        data/orientation
        data/reference_structure
        data/time

and so on for the nine other input files. This shows that the DOI is
used in a link to the destination file's dataset
`code/python-packages/mosaic`, whereas the local files were used as
the source for data copied into the ActivePaper itself. A copy
reference thus serves just for documentation, there is no need to have
a copy of the referenced file.

Back to dataset types. There are a few more of those, which didn't
show up in the first lines of `aptool ls -l`, so let's look at a few
of the remaining lines:

    2013-07-03/12:24:26  text       documentation/README
    2013-06-14/15:55:08  file       documentation/c_rr_diagonals.pdf
    2013-06-14/15:55:00  data       data/correlation_function_integration_limit
    2013-06-14/15:46:47  dummy      data/coordinate_trajectories/rotation_laboratory_frame_1

You can probably guess what `text` means. And `file` is just what a
file is in the Unix world: a sequence of bytes, with no particular
intepretation attached to them. You will see later how such a file can
be extracted. The meaning of `data` is perhaps less obvious, in
particular how it differs from a file. The answer is that `data` is an
arbitrary HDF5 dataset, characterized by a data space, and a data
type. Think of it as an array if you want, it's in fact quite close.

That leaves `dummy`, which is a non-existant dataset. More precisely,
a no longer existing dataset. It's a dataset that was generated by a
calclet, and then removed explicitly (using `aptool dummy ...`) in
order to reduce the size of the file. If you want to inspect it, or
run any of the calclets that read it in, you have to re-generate it first
by re-running the calclet.

So let's do this:

    aptool update -v

This updates everything in the ActivePaper that needs updating: dummy
datasets, but also stale datasets, i.e. datasets that are older than
the current version of the calclet that produced them. The `-v`
options makes it verbose, it tells you which calclets are run and
why. Be prepapred to wait a while; on my machine, the operation takes
about eight minutes on my machine. We can see that the file size has
increased significantly:

    ls -l

    -rw-r--r--  1 hinsen  staff  540352636 Oct 23 14:54 lysozyme_diffusion.ap

Moreover, the formerly dummy datasets are now real ones:

    aptool ls -l data/coordinate_trajectories/rotation_laboratory_frame_1

    2013-10-23/14:45:29  data       data/coordinate_trajectories/rotation_laboratory_frame_1


## Extracting the plots

If you look at the full output of `aptool ls -l`, you will notice a
couple of PDF files under `documentation`. To look at them, extract
them to real files:

    aptool checkout documentation

This will also get you the `README`, as it extracts everything in the
HDF5 group `documentation` to a local directory called, you guessed
it, `documentation`. The `documentation` group in an ActivePaper is
for data intended for humans, it is in general not used as input to
computations.

Note that you can of course check out individual files, e.g.

    aptool checkout documentation/README.txt

The `checkout` command extracts only those datasets that are newer
than the corresponding file on disk, if it already exists. You can
thus edit extracted files without having them overwritten. We will see
this in action immediately when working with the code.


## Extracting and modifying the code

Next, let's have a look at all the code in the ActivePaper:

    aptool checkout code

This will produce a warning,

    Skipping /code/python-packages/mosaic: data type reference not extractable

but everything else is in the directory `code`:

    ls -lR code

    total 72
    -rw-r--r--  1 hinsen  staff  4537 Jun  7 09:13 correlation_functions.py
    -rw-r--r--  1 hinsen  staff  1586 Jun  7 09:19 diffusion_tensor.py
    -rw-r--r--  1 hinsen  staff   266 Jun  7 10:02 identify_trajectories.py
    -rw-r--r--  1 hinsen  staff  9246 Jun 12 08:03 plots.py
    drwxr-xr-x  8 hinsen  staff   272 Oct 23 15:02 python-packages
    -rw-r--r--  1 hinsen  staff  2024 Jun  7 09:57 thermal_averages.py
    -rw-r--r--  1 hinsen  staff  2987 Jun 14 15:46 trajectory_processing.py
    
    code/python-packages:
    total 40
    -rw-r--r--  1 hinsen  staff   273 Jun  4 15:42 fitting.py
    -rw-r--r--  1 hinsen  staff   655 May  2 15:11 molecular_structure.py
    -rw-r--r--  1 hinsen  staff     0 Oct 23 15:02 mosaic
    -rw-r--r--  1 hinsen  staff  2741 May 23 11:42 quaternion.py
    -rw-r--r--  1 hinsen  staff  3234 May 27 04:13 time_series.py
    -rw-r--r--  1 hinsen  staff  3772 May  2 15:12 units.py

The dates are the ones stored in the ActivePaper. Let's now make a
change to a file. A good candidate is `plots.py`, because it's cheap
to re-run (nothing depends on the generated plots). To avoid breaking
anything, don't make any real change, but just a comment line
somewhere. You should see a current time stamp:

    ls -l code/plots.py

    -rw-r--r--  1 hinsen  staff  9253 Oct 23 15:15 code/plots.py

Now we update the copy in the ActivePaper:

    aptool checkin code

and verify that it has the same time stamp:

    aptool ls -l code/plots

    2013-10-23/15:15:54  calclet    code/plots

All the plots should now be marked as stale, which `aptool ls -l`
indicates by a star before the filename. Let's check:

    aptool ls -l | grep \*

    2013-10-23/14:54:15  file      *documentation/c_rr_diagonals.pdf
    2013-10-23/14:54:16  file      *documentation/c_rr_off_diagonal.pdf
    2013-10-23/14:54:14  file      *documentation/c_tt_diagonal.pdf
    2013-10-23/14:54:15  file      *documentation/c_tt_off_diagonal.pdf
    2013-10-23/14:54:18  file      *documentation/c_vr.pdf
    2013-10-23/14:54:20  file      *documentation/msd_rr_diagonal.pdf
    2013-10-23/14:54:20  file      *documentation/msd_rr_off_diagonal.pdf
    2013-10-23/14:54:19  file      *documentation/msd_tt_diagonal.pdf
    2013-10-23/14:54:19  file      *documentation/msd_tt_off_diagonal.pdf
    2013-10-23/14:54:21  file      *documentation/msd_vr.pdf

Now we can update them again:

    aptool update -v

which says

    Dataset /documentation/msd_vr.pdf is stale or dummy, running /code/plots

There is just that one line, because running `code/plots` updates all
the plots, so after the execution there are no stale files left.

## Inspecting and modifying parameters

The example file contains four parameters that were set manually:

    data/correlation_function_integration_limit
    data/correlation_function_plot_range
    data/msd_fit_range
    data/msd_plot_range

The plot ranges are the intervals on the x-axis in the plots you have
extracted above. The integration limits are used in the computations,
but are also shown in the plots, as grey boxes. This means you can see
the effect of modifying these values just by looking at the plots.
Changing the plot ranges is cheaper because nothing but the plots
needs to be recomputed. So let's change `data/msd_plot_range`.

Before changing it, it would be nice to know what the current value is.
There are no data formatting commands in `aptool` (yet), but since an
ActivePaper is just an HDF5 file, you can use the generic `h5dump`:

    h5dump -d data/msd_plot_range lysozyme_diffusion.ap

This tells you way more than you need to know:

    HDF5 "lysozyme_diffusion.ap" {
    DATASET "data/msd_plot_range" {
       DATATYPE  H5T_IEEE_F64LE
       DATASPACE  SIMPLE { ( 2 ) / ( 2 ) }
       DATA {
       (0): 0, 100
       }
       ATTRIBUTE "ACTIVE_PAPER_DATATYPE" {
          DATATYPE  H5T_STRING {
             STRSIZE H5T_VARIABLE;
             STRPAD H5T_STR_NULLTERM;
             CSET H5T_CSET_ASCII;
             CTYPE H5T_C_S1;
          }
          DATASPACE  SCALAR
          DATA {
          (0): "data"
          }
       }
       ATTRIBUTE "ACTIVE_PAPER_TIMESTAMP" {
          DATATYPE  H5T_STD_I64LE
          DATASPACE  SCALAR
          DATA {
          (0): 1371218101290
          }
       }
    }
    }

This tells you that the plot range is a two-element float array whose
value is `[0, 100]`. Let's set it to `[0, 200]`:

    aptool set msd_plot_range 'array([0.,200.])'

Since all data must be under `data`, we just give `msd_plot_range` as
the dataset name. The value can be any Python expression, but it
must evaluate to something that [h5py](http://www.h5py.org/) accepts
for assigning to a dataset.

We should now have a few stale datasets again:

    aptool ls -l | grep \*

    2013-10-23/15:21:15  file      *documentation/msd_rr_diagonal.pdf
    2013-10-23/15:21:15  file      *documentation/msd_rr_off_diagonal.pdf
    2013-10-23/15:21:14  file      *documentation/msd_tt_diagonal.pdf
    2013-10-23/15:21:14  file      *documentation/msd_tt_off_diagonal.pdf
    2013-10-23/15:21:16  file      *documentation/msd_vr.pdf

Updating the ActivePaper will do exactly the same as last time: run
`code/plots`. But this time, the plots really change (remember we
changed the plot range), so it's worth extracting them again to
verify:

    aptool update
    aptool checkout documentation


## Creating an ActivePaper from scratch

We have come to the end of this tutorial, but as a final goodie I will
show you the shell script that I used to generate this ActivePaper.
You can't run it on your machine, because you don't have all the input
data (remember those `local:` references?), but it can serve as a guide
for making your own.

    # This is the only time we need to give the filename.
    # After -d, we list external dependencies, i.e. Python modules
    # that are required but not available as ActivePapers.
    aptool -p lysozyme_diffusion.ap create -d matplotlib
    
    # Add README.txt and all the Python modules and calclets
    aptool checkin -t text documentation/README.txt
    aptool checkin -t module code/python-packages/*.py
    aptool checkin -t calclet code/*.py
    
    # Add a link to pyMosaic, as published on Figshare
    aptool ln doi:10.6084/m9.figshare.705829: code/python-packages/mosaic
    
    # Create two groups to which calclets will later add datasets
    aptool group data/reference_structures
    aptool group data/trajectory
    
    # Copy data from ActivePapers stored locally
    aptool cp local:lysozyme_spce_rbt_1:data/time data/trajectory/time
    for N in 1 2 3 4 5 6 7 8 9 10
    do
      aptool cp local:lysozyme_spce_rbt_$N:data/reference_structure data/reference_structures/reference_structure_$N
      aptool cp local:lysozyme_spce_rbt_$N:data/center_of_mass data/trajectory/center_of_mass_$N
      aptool cp local:lysozyme_spce_rbt_$N:data/orientation data/trajectory/orientation_$N
    done
    
    # Set the temperature parameter
    aptool set temperature 300.
    
    # Run the first calclets
    aptool run identify_trajectories
    aptool run thermal_averages
    aptool run trajectory_processing
    aptool run correlation_functions
    
    # Set the integration limits and plot ranges
    aptool set correlation_function_integration_limit 20.
    aptool set correlation_function_plot_range 'array([0.,30.])'
    aptool set msd_plot_range 'array([0.,100.])'
    aptool set msd_fit_range 'array([20.,40.])'
    
    # Generate the plots and the output datasets (diffusion tensors)
    aptool run plots
    aptool run diffusion_tensor
