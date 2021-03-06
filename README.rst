SciKit-GStat
============

Info: scikit-gstat needs Python >= 3.4!

.. image:: https://img.shields.io/badge/pypi%20package-0.2.3-green.svg
    :target: https://pypi.org/project/scikit-gstat/0.2.3/

.. image:: https://img.shields.io/badge/version-0.2.3-green.svg
    :target: https://github.com/mmaelicke/scikit-gstat

.. image:: https://travis-ci.org/mmaelicke/scikit-gstat.svg?branch=master
    :target: https://travis-ci.org/mmaelicke/scikit-gstat
    :alt: Build Status

.. image:: https://api.codacy.com/project/badge/Grade/34022fb8b795435b8eeb5431159fa7c6
   :alt: Codacy Badge
   :target: https://app.codacy.com/app/mmaelicke/scikit-gstat?utm_source=github.com&utm_medium=referral&utm_content=mmaelicke/scikit-gstat&utm_campaign=Badge_Grade_Dashboard

.. image:: https://readthedocs.org/projects/scikit-gstat/badge/?version=latest
    :target: http://scikit-gstat.readthedocs.io/en/latest?badge=latest
    :alt: Documentation Status

.. image:: https://codecov.io/gh/mmaelicke/scikit-gstat/branch/master/graph/badge.svg
    :target: https://codecov.io/gh/mmaelicke/scikit-gstat
    :alt: Codecov

.. image:: https://zenodo.org/badge/98853365.svg
   :target: https://zenodo.org/badge/latestdoi/98853365

How to cite
-----------

In case you use SciKit-GStat in other software or scientific publications,
please reference this module. It is published and has a DOI. It can be cited
as:

  Mälicke, Mirko, & Schneider, Helge David. (2018). mmaelicke/scikit-gstat:
  Geostatistical variogram toolbox (Version v0.2.2). Zenodo.
  http://doi.org/10.5281/zenodo.1345584

Full Documentation
------------------

The full documentation can be found at: https://mmaelicke.github.io/scikit-gstat


New Version 0.2
---------------

Scikit-gstat was rewritten in major parts. Most of the changes are internal,
but the attributes and behaviour of the `Variogram` has also changed
substantially.
A detailed description of of the new versions usage will follow. The last
version of the old Variogram class, 0.1.8, is kept in the `version-0.1.8`
branch on GitHub, but not developed any further. Those two versions are not
compatible.

Description
-----------

SciKit-Gstat is a scipy-styled analysis module for geostatistics. It includes
two base classes :class:`Variogram <skgstat.Variogram>` and
:class:`DirectionalVariogram <skgstat.DirectionalVariogram>`. Both have a
very similar interface and can compute experimental variograms and model
variograms. The module makes use of a rich selection of semi-variance
estimators and variogram model functions, while being extensible at the same
time.
The estimators include:

- matheron
- cressie
- dowd
- genton
- entropy
- two experimental ones: quantiles, minmax

The models include:

- sperical
- exponential
- gaussian
- cubic
- stable
- matérn

with all of them in a nugget and no-nugget variation. All the estimator are
implemented using numba's jit decorator. The usage of numba might be subject
to change in future versions.
At the current stage, the package does not include any kriging. This is planned for a future release.


Installation
~~~~~~~~~~~~

PyPI:

.. code-block:: bash

  pip install scikit-gstat

GIT:

.. code-block:: bash

  git clone https://github.com/mmaelicke/scikit-gstat.git
  cd scikit-gstat
  pip install -r requirements.txt
  pip install -e .

Usage
~~~~~

The `Variogram` class needs at least a list of coordiantes and values. All other attributes are set by default.
You can easily set up an example by generating some random data:

.. code-block:: python

  import numpy as np
  import skgstat as skg

  coordinates = np.random.gamma(0.7, 2, (30,2))
  values = np.random.gamma(2, 2, 30)

  V = skg.Variogram(coordinates=coordinates, values=values)
  print(V)

.. code-block:: bash

  spherical Variogram
  -------------------
  Estimator:    matheron
  Range:        1.64
  Sill:         5.35
  Nugget:       0.00
