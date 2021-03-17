*******
WireViz
*******


.. image:: https://img.shields.io/pypi/v/wireviz.svg?colorB=blue
  :alt: PyPI - Version
  :target: https://pypi.org/project/wireviz/

.. image:: https://img.shields.io/pypi/pyversions/wireviz.svg?
  :alt: PyPI - Python Version
  :target: https://pypi.org/project/wireviz/

.. image:: https://img.shields.io/pypi/dm/wireviz
  :alt: PyPI - Downloads
  :target: https://pypi.org/project/wireviz/


Summary
=======

WireViz is a tool for easily documenting cables, wiring harnesses and connector pinouts. It takes plain text, YAML-formatted files as input and produces beautiful graphical output (SVG, PNG, ...) thanks to [GraphViz](https://www.graphviz.org/). It handles automatic BOM (Bill of Materials) creation and has a lot of extra features.


Features
========

* WireViz input files are fully text based

  * No special editor required
  * Human readable
  * Easy version control
  * YAML syntax
  * UTF-8 input and output files for special character support

* Understands and uses color abbreviations as per `IEC 60757 <https://en.wikipedia.org/wiki/Electronic_color_code#Color_band_system>`__ (black=BK, red=RD, ...)
* Auto-generates standard wire color schemes and allows custom ones if needed

  * `DIN 47100 <https://en.wikipedia.org/wiki/DIN_47100>`__ (WT/BN/GN/YE/GY/PK/BU/RD/BK/VT/...)
  * `IEC 60757 <https://en.wikipedia.org/wiki/Electronic_color_code#Color_band_system>`__   (BN/RD/OR/YE/GN/BU/VT/GY/WT/BK/...)
  * `25 Pair Color Code <https://en.wikipedia.org/wiki/25-pair_color_code#Color_coding>`__ (BUWH/WHBU/OGWH/WHOG/GNWH/WHGN/BNWH/...)
  * `TIA/EIA 568 A/B <https://en.wikipedia.org/wiki/TIA/EIA-568#Wiring>`__  (Subset of 25-Pair, used in CAT-5/6/...)

* Understands wire gauge in mm² or AWG

  * Optionally auto-calculates equivalent gauge between mm² and AWG

* Is suitable for both very simple cables, and more complex harnesses.
* Allows for easy-autorouting for 1-to-1 wiring
* Generates BOM (Bill of Materials)

.. note:: WireViz is not designed to represent the complete wiring of a system. Its main aim is to document the construction of individual wires and harnesses.

Examples
========

Demo 01
-------

.. code-block:: yaml

  connectors:
    X1:
      type: D-Sub
      subtype: female
      pinlabels: [DCD, RX, TX, DTR, GND, DSR, RTS, CTS, RI]
    X2:
      type: Molex KK 254
      subtype: female
      pinlabels: [GND, RX, TX]

  cables:
    W1:
      gauge: 0.25 mm2
      length: 0.2
      color_code: DIN
      wirecount: 3
      shield: true

  connections:
    -
      - X1: [5,2,3]
      - W1: [1,2,3]
      - X2: [1,3,2]
    -
      - X1: 5
      - W1: s

Output file:

.. image:: ./examples/demo01.png
  :alt: Sample output diagram

`Source <./examples/demo01.yml>`__ - `Bill of Materials <examples/demo01.bom.tsv>`__ (auto-generated)

Demo 02
-------

.. image:: ./examples/demo02.png
  :alt: Wireviz output for demo02

`Source <examples/demo02.yml>`__ - `Bill of Materials <examples/demo02.bom.tsv>`__

Tutorial and example gallery
----------------------------

See the `tutorial page <tutorial/readme.md>`__ for sample code,
as well as the `example gallery <examples/readme.md>`__ to see more of what WireViz can do.

Usage
=====

Installation
------------

Requirements
^^^^^^^^^^^^

WireViz requires Python 3.7 or later.

WireWiz requires GraphViz to be installed in order to work. See the `GraphViz download page <https://graphviz.org/download/>`__ for OS-specific instructions.

.. note:: Ubuntu 18.04 LTS users in particular may need to separately install Python 3.7 or above, as that comes with Python 3.6 as the included system Python install.

Installing the latest release
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The latest WireViz release can be downloaded from `PyPI <https://pypi.org/project/wireviz/>`__ with the following command:

.. code::

  pip3 install wireviz

Installing the development version
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Access to the current state of the development branch can be gained by cloning the repo and installing manually:

.. code::

  git clone <repo url>
  cd <working copy>
  git checkout dev
  pip3 install -e .


If you would like to contribute to this project, make sure you read the `contribution guidelines <CONTRIBUTING.md>`__!

How to run
----------

.. code::

  wireviz ~/path/to/file/mywire.yml

This will output the following files ::

  mywire.gv         GraphViz output
  mywire.svg        Wiring diagram as vector image
  mywire.png        Wiring diagram as raster image
  mywire.bom.tsv    BOM (bill of materials) as tab-separated text file
  mywire.html       HTML page with wiring diagram and BOM embedded


Command line options
^^^^^^^^^^^^^^^^^^^^

- ``--prepend-file <FILE>`` to prepend an additional YAML file. Useful for part libraries and templates shared among multiple cables/harnesses.
- ``-o <OUTPUT>`` or ``--output_file <OUTPUT>`` to generate output files with a name different from the input file.
- ``-V`` or ``--version`` to display the WireViz version.
- ``-h`` or ``--help`` to see a summary of the usage help text.

Syntax description
------------------

A description of the WireViz YAML input syntax can be found `here <syntax.md>`__.


(Re-)Building the example projects
----------------------------------

Please see the `documentation <buildscript.md>`__ of the ``build_examples.py`` script for info on building the demos, examples and tutorial.

Changelog
=========

See `CHANGELOG.md <CHANGELOG.md>`__.

Status
======

This is very much a work in progress. Source code, API, syntax and functionality may change wildly at any time.


License
=======

`GPL-3.0 <LICENSE>`__
