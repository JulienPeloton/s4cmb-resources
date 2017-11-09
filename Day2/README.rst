End-to-end examples
===============

We provide two notebooks focusing on

* Simulation of gain drifts.
* Simulation of differential pointing.

Note that on both examples, in addition to scanning pure CMB maps, we also
inject noise directly in time-domain. For the moment, the noise is assumed to
be white, but there is a plan to add correlated noise (see `here <https://github.com/JulienPeloton/s4cmb/projects>_`). If you are interested,
just contact me!

Using s4cmb on a cluster (mpi version)
===============

All examples so far focused on very small instruments, with few bolometers.
Of course, one wants to study current and future experiments with thousands of
detectors. Keep calm, and use a cluster! We provide two ready-to-use Apps and their
batch files for Cori (NERSC). Note that the amount of resource needed usually depends on
what you want to simulate. If your detector timestreams remain uncorrelated, then
you do not need much memory (you would just load a few objects in the memory at once).
But if you need to have access to all timestreams at once (e.g. crosstalk), you may need
a lot of memory. Example, for a SO-like experiment with 7000 detector scanning for 4h at
sampling rate of 15 Hz, just loading the timestreams (Double-precision floating-point format)
requires 7000 * 4 * 3600 * 15 * 8 = 12 GB! And this is just for the timestreams
(you would also need pointing, masks, etc)!

Of course one can always finds clever tricks for particular cases to reduce the memory usage, but
these cases (fully correlated vs fully uncorrelated) roughly define your bounds.

How to contribute to s4cmb?
===============

Feel free to submit issues and enhancement requests!
In general, we appreciate the "fork-and-pull" Git workflow, as explained
`here <https://github.com/JulienPeloton/s4cmb/blob/master/CONTRIBUTING.rst>_`.
