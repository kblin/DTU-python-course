---
layout: page
title: "Setup"
permalink: /setup/
---

## Installing Python Using Anaconda

[Python](https://python.org) is a popular language for scientific computing, and great for
general-purpose programming as well. Installing all of its scientific packages
individually can be a bit difficult, however, so we recommend the all-in-one
installer [Anaconda](https://www.continuum.io/anaconda).

Regardless of how you choose to install it, please make sure you install Python
version 3.x (e.g., 3.4 is fine). Also, please set up your python environment at 
least a day in advance of the workshop.  If you encounter problems with the 
installation procedure, ask your workshop organizers via e-mail for assistance so
you are ready to go as soon as the workshop begins.

### Windows - [Video tutorial](https://www.youtube.com/watch?v=xxQ0mzZ8UvA)

1. Open [https://www.anaconda.com/products/individual](https://www.anaconda.com/products/individual) 
    with your web browser.

2. Download the graphical installer for Windows.

3. Double-click the executable and install Python using _MOST_ of the
    default settings. The only exception is to check the 
    **Make Anaconda the default Python** option (in case that opion exists).

### Mac OS X - [Video tutorial](https://www.youtube.com/watch?v=TcSAln46u9U)

1. Open [https://www.anaconda.com/products/individual](https://www.anaconda.com/products/individual) 
    with your web browser.

2. Download the graphicsl installer for OS X at the botoom.

3. Install Python 3 using all of the defaults for installation.

### Linux
Note that the following installation steps require you to work from the shell. 
If you run into any difficulties, please request help before the workshop begins.

1.  Open [https://www.anaconda.com/products/individual](https://www.anaconda.com/products/individual)
     with your web browser.

2.  Download a suitable installer for Linux.

3.  Install Python 3 using all of the defaults for installation.

    a.  Open a terminal window.

    b.  Navigate to the folder where you downloaded the installer

    c.  Type

    ~~~
    $ bash Anaconda3-
    ~~~
    {: .source}

    and press tab.  The name of the file you just downloaded should appear.

    d.  Press enter.

    e.  Follow the text-only prompts.  When the license agreement appears (a colon
        will be present at the bottom of the screen) hold the down arrow until the 
        bottom of the text. Type `yes` and press enter to approve the license. Press 
        enter again to approve the default location for the files. Type `yes` and 
        press enter to prepend Anaconda to your `PATH` (this makes the Anaconda 
        distribution the default Python).

## Getting the Data

This lesson comes with a number of pre-made notebooks and some practice data.
The data we will be using for the pandas lesson is taken from the [gapminder](http://gapminder.org) dataset.
To obtain it, download and unzip the file 
[python-novice-biopython-data.zip][data-zip].
In order to follow the presented material, you should launch a Jupyter 
notebook in the "notebooks" directory (see [Starting Python](#Starting-Python)).

Solutions for the exercises are in
[notebooks_solved.zip][data-solved-zip].

## Starting Python

We will teach Python using the [Jupyter notebook](http://jupyter.org/), a 
programming environment that runs in a web browser. Jupyter requires a reasonably 
up-to-date browser, preferably a current version of Chrome, Safari, or Firefox 
(note that Internet Explorer version 9 and below are *not* supported). If you 
installed Python using Anaconda, Jupyter should already be on your system. If 
you did not use Anaconda, use the Python package manager pip.
([See the Jupyter website for details](http://jupyter.readthedocs.io/en/latest/
install.html#optional-for-experienced-python-developers-installing-jupyter-with-pip))

To start the notebook, open a terminal or git bash and type the command:

~~~
$ jupyter notebook
~~~
{: .source}

To start the Python interpreter without the notebook, open a terminal 
or git bash and type the command:

~~~
$ python
~~~
{: .source}

[data-zip]: {{site.github.repository_url}}/blob/gh-pages/files/python-novice-biopython-data.zip?raw=true
[data-solved-zip]: {{site.github.repository_url}}/blob/gh-pages/files/notebooks_solved.zip?raw=true
