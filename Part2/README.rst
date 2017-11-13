.. contents:: **Part2: Table of Contents**

End-to-end examples
===============

We provide two notebooks focusing on

* `Simulation of gain drifts. <https://github.com/JulienPeloton/s4cmb-resources/blob/master/Part2/s4cmb_gain_drifts.ipynb>`_
* `Simulation of differential pointing. <https://github.com/JulienPeloton/s4cmb-resources/blob/master/Part2/s4cmb_differential_pointing.ipynb>`_

Note that on both examples, in addition to scanning pure CMB maps, we also
inject noise directly in time-domain. For the moment, the noise is assumed to
be white, but there is a plan to add correlated noise
(see `here <https://github.com/JulienPeloton/s4cmb/projects>`_).
If you are interested, just contact me!

Using s4cmb on a cluster/supercomputer (mpi version)
===============

**Why going to a supercomputer?**

All examples so far focused on very small instruments, with few bolometers.
Of course, one wants to study current and future experiments with thousands of
detectors, and make MC simulations. Keep calm, and use a cluster!
We provide two ready-to-use Apps and their batch files for Cori (NERSC).
Note that the amount of resource needed usually depends on
what you want to simulate. If your detector timestreams remain uncorrelated, then
you do not need much memory (you would just load a few objects in the memory at once).
But if you need to have access to all timestreams at once (e.g. crosstalk), you may need
a lot of memory. Example, for a SO-like experiment with 7000 detector scanning for 4h at
sampling rate of 15 Hz, just loading the timestreams (Double-precision floating-point format)
requires 7000 * 4 * 3600 * 15 * 8 = 12 GB! And this is just for the timestreams
(you would also need pointing, masks, etc)!

Of course one can always finds clever tricks for particular cases to reduce the memory usage, but
these cases (fully correlated vs fully uncorrelated) roughly define your bounds.
Note that the parallelisation happens at the level of CES, that is we send different scans
to different CPU (or group of CPU). One could benefit from openmp in fortran routines (i.e. hybrid MPI/openmp),
but I disabled that for the moment. Contact me if you are interested in restoring that.

**Submit your first job**

Say you want to launch the simulation for gain drifts. First, connect to Cori, and copy
MC_lowmemory_gain_drifts_launcher.batch, so_MC_gain_drift.py and so_parameters.py to
a folder in your $SCRATCH. Make sure you have installed s4cmb at NERSC as well.
Then from the folder where all files are, just submit a job

::

    sbatch MC_lowmemory_gain_drifts_launcher.batch

it should take roughly 20 minutes to complete the full 10 MC simulations.

How to contribute to s4cmb?
===============

Feel free to submit issues and enhancement requests!
In general, we appreciate the "fork-and-pull" Git workflow, as explained
`here <https://github.com/JulienPeloton/s4cmb/blob/master/CONTRIBUTING.rst>`_.
