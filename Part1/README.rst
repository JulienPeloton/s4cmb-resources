.. contents:: **Part1: Table of Contents**

Requirements
===============
The pipeline is mainly written in python and it has the following dependencies (see requirements.txt):

* numpy, matplotlib
* astropy, ephem, pyslalib, healpy (astro libs)
* f2py (interfacing with python)

While we use python 2.7, we try to make it compatible with python 3.5 and 3.6.
If you are using python 3.x and you encounter an error, please open an issue or a
pull request so that we fix it asap.

Some parts of the pipeline are written in Fortran which is interfaced with
python using f2py. The compilation is done usually when you install the
package (see setup.py), but we also provide a Makefile for more
customized compilations (see the Makefile in s4cmb).

Installation
===============
The type of installation depends on what you want to do with the code:
just using it or also developing it?

**I just want to use the code:**

You can easily install the package using pip

::

    pip install s4cmb

**In addition to use the code, I want to be a developer:**

For the purpose of this tutorial, we rather recommend that you fork the repo from
the s4cmb github repository to your account and clone it to your machine (to be able to modify the code on your own).
See `here <https://github.com/JulienPeloton/s4cmb/blob/master/CONTRIBUTING.rst>`_ for more information on how to contribute.
Once you have the repo cloned on your machine, use the makefile to compile the source

::

    cd /path/to/s4cmb
    pip install -r requirements.txt
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

Installation and usage at NERSC
===============

Again, you can easily install the package using pip

::

    pip install s4cmb --user

Alternatively, if you want to do dev at NERSC and do a manual installation, it's better to keep most of your packages under Anaconda.
I recommend to have a look first at the `NERSC page <https://www.nersc.gov/users/data-analytics/data-analytics-2/python/anaconda-python/>`_ describing how to use it.

The installation of s4cmb can be done in few steps:

* Clone the repo somewhere in your $HOME
* Install dependencies (see requirements.txt) using Anaconda
* Compile the source (using make in /path/s4cmb)

**Use of notebooks at NERSC (not so recommended)**

If you want to run jupyter notebooks, see `here <http://www.nersc.gov/users/data-analytics/data-analytics-2/jupyter-and-rstudio/>`_.
Note that jupyter.nersc.gov doesn't source your bashrc (so you won't have by default access to your modules). For a more advanced use,
log on to jupyter-dev.nersc.gov (however, frequent errors occur... Especially conflict with your $PYTHONPATH and $JUPYTER_PATH).
In addition, to display images you probably need to add

::

    %matplotlib inline

at the beginning of each notebook.

**If you cannot connect to jupyter-dev (failure to spawn)**

When you try to connect to jupyter-dev, it will read your JUPYTER_PATH.
If for some reasons, there are packages in your path in conflict with the default
paths of jupyter-dev, you will not be able to connect. If you encounter such problem, here is a solution:

* Edit your .bashrc.ext (or whatever file where you declare your paths) and reorganise it the following:

::

    export NERSC_HOST=`/usr/common/usg/bin/nersc_host`
    if [ ${NERSC_HOST} == "cori19" ]; then
        export NERSC_HOST="toto"
    fi

    if [ ${NERSC_HOST} == "cori" ]; then
        <all your declarations and module loads>
    fi

* By doing so, if you connect to jupyter-dev (cori19), you won't load all your custom packages. However, if you connect to cori, you will load everything as usual.
* Then clone the package `Ipython_Kernel_NERSC <https://github.com/JulienPeloton/Ipython_Kernel_NERSC>`_ and create a kernel with all your paths.
* Connect to https://jupyter-dev.nersc.gov/hub/login and create a notebook with the kernel you just created (which contains all your favourite paths).

Working with Docker
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
Part 1 is organised the following:

* `Lecture 01 <https://github.com/JulienPeloton/s4cmb-resources/blob/master/Part1/s4cmb_presentation_01.ipynb>`_: presentation of the library.
* `Lecture 02 <https://github.com/JulienPeloton/s4cmb-resources/blob/master/Part1/s4cmb_instrument_02.ipynb>`_: how to generate an instrument.
* `Lecture 03 <https://github.com/JulienPeloton/s4cmb-resources/blob/master/Part1/s4cmb_scanning_strategy_03.ipynb>`_: how to generate a scanning strategy.
* `Lecture 04 <https://github.com/JulienPeloton/s4cmb-resources/blob/master/Part1/s4cmb_tod_04.ipynb>`_: how to generate TOD.
* `Lecture 05 <https://github.com/JulienPeloton/s4cmb-resources/blob/master/Part1/s4cmb_crosstalk_05.ipynb>`_: An example of instrument systematic (crosstalk).

In addition, you will find an end-to-end `example <https://github.com/JulienPeloton/s4cmb-resources/blob/master/Part1/simple_app.py>`_ that can be ran on a laptop

::

    python simple_app.py -inifile simple_parameters.py -tag test

or using 4 processors (change mpirun with your favourite command)

::

    mpirun -n 4 python simple_app.py -inifile simple_parameters.py -tag test

The script should exit with a message: All OK! Greetings from processor X/Y!
and you have a folder out/ containing maps and masks.
