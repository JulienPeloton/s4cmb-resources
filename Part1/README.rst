.. contents:: **Part1: Table of Contents**

Requirements
===============
The pipeline is mainly written in python and it has the following dependencies:

* numpy, matplotlib
* astropy, ephem, pyslalib, healpy (astro libs)
* f2py, weave (interfacing with python)

While we use python 2.7, we try to make it compatible with python 3.x.
If you are using python 3.x and you encounter an error, please open an issue or a
pull request so that we fix it asap.

Some parts of the pipeline are written in C (and compiled on-the-fly via the
package weave), and in Fortran (to come). The latter is interfaced with
python using f2py. The compilation is done usually when you install the
package (see setup.py), but we also provide a Makefile for more
customized compilations (see the Makefile in s4cmb).

Installation
===============
You can easily install the package using pip

::

    pip install s4cmb

Instead for the purpose of this tutorial, we rather recommend that you fork the repo from
the github repository and clone it to your machine (to be able to modify the code on your own).
See `here <https://github.com/JulienPeloton/s4cmb/blob/master/CONTRIBUTING.rst>`_ for more information on how to contribute.
Once you have the repo cloned on your machine, use the makefile to compile the source

::

    cd /path/to/s4cmb
    make

Do not forget to update your PYTHONPATH to tell your machine where the code is.
For example, just add at the end of your bashrc:

::

    s4cmbPATH=/path/to/s4cmb
    export PYTHONPATH=$PYTHONPATH:$s4cmbPATH

Then run the test suite and the coverage:

::

    ./coverage_and_test.sh

It should exit with no errors.

Installation using Docker
===============
Alternatively if you do not want install the package on your computer,
we provide a docker image for s4cmb with always the latest version. Install
docker on your computer, and pull the image:

::

    docker pull julienpeloton/s4cmb:latest

Then create a new container and run an interactive session by just running

::

    docker run -i -t julienpeloton/s4cmb:latest bash

Lectures
===============
Day1 is organised the following:

* `Lecture 01 <https://github.com/JulienPeloton/s4cmb-resources/blob/master/Day1/s4cmb_presentation_01.ipynb>`_: presentation of the library.
* `Lecture 02 <https://github.com/JulienPeloton/s4cmb-resources/blob/master/Day1/s4cmb_instrument_02.ipynb>`_: how to generate an instrument.
* `Lecture 03 <https://github.com/JulienPeloton/s4cmb-resources/blob/master/Day1/s4cmb_scanning_strategy_03.ipynb>`_: how to generate a scanning strategy.
* `Lecture 04 <https://github.com/JulienPeloton/s4cmb-resources/blob/master/Day1/s4cmb_tod_04.ipynb>`_: how to generate TOD.
* `Lecture 05 <https://github.com/JulienPeloton/s4cmb-resources/blob/master/Day1/s4cmb_crosstalk_05.ipynb>`_: An example of instrument systematic (crosstalk).

In addition, you will find an end-to-end `example <https://github.com/JulienPeloton/s4cmb-resources/blob/master/Day1/simple_app.py>`_ that can be ran on a laptop

::

    python simple_app.py -inifile simple_parameters.py -tag test

or using 4 processors (change mpirun with your favourite command)

::

    mpirun -n 4 python simple_app.py -inifile simple_parameters.py -tag test
