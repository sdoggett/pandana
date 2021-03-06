Installation
============

Pandana is a Python package that includes a C/C++ extension. Pandana is tested on Mac, Linux, and Windows with Python 2.7, 3.6, and 3.7.

The easiest way to install Pandana is using the `Anaconda`_ package manager. Pandana's Anaconda distributions are pre-compiled and include multi-threading support on all platforms.

If you install Pandana from Pip or from the source code on GitHub, you'll need to compile the C/C++ extension locally. This is automatic, but won't work unless the right build tools are present. See full instructions below.


Anaconda (recommended)
----------------------

Pandana is hosted on Conda Forge::

    conda install pandana --channel conda-forge


.. _pip:

Pip (requires local compilation)
--------------------------------

Pandana is also hosted on PyPI::

    pip install pandana

Pandana's C/C++ extension will compile automatically if the right tools are present. See below for troubleshooting.

Pip can have trouble installing Pandana's requirements in Windows Python 2.7; try Conda instead.


.. _github:

GitHub source code
------------------

If you'll be modifying the code, you can install Pandana from the `GitHub source <https://github.com/udst/pandana>`_::

    git clone https://github.com/udst/pandana.git
    cd pandana
    python setup.py develop

You'll need to have Cython and NumPy installed before running :code:`setup.py`. 

Pandana's C/C++ extension will compile automatically if the right tools are present. See below for troubleshooting.


Compiling locally
-----------------

Building Pandana from source requires C/C++ compilers. On Linux and Mac these are usually already present, but read on for more information.

Compiling Pandana in Linux
~~~~~~~~~~~~~~~~~~~~~~~~~~

Pandana's setup script expects a version of the GCC compiler with support for OpenMP. This appears to be GCC 4.8+, but we haven't done extensive testing. If you run into problems, try doing a fresh install of the core build tools::

    sudo apt-get install --reinstall build-essential

Compiling Pandana in Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Compilation is automatic but requires that `Microsoft Visual C++ Build Tools <https://visualstudio.microsoft.com/visual-cpp-build-tools/>`_ are installed.

Certain older machines may need the `Microsoft Visual C++ 2008 SP1 Redistributable Package (x64) <https://www.microsoft.com/en-us/download/details.aspx?id=2092>`_ or something similar in order to use Pandana. This provides runtime components of the Visual C++ libraries.

Compiling Pandana in OS X
~~~~~~~~~~~~~~~~~~~~~~~~~

The default OS X compilers don't support OpenMP, which Pandana uses for multi-threading.

To allow multi-threading, use these commands to confirm that Xcode Command Line Tools are present and to install some newer compilers from Anaconda::

    xcode-select --install
    conda install llvm-openmp clang

Then follow the :ref:`Pip <pip>` or :ref:`GitHub source code <github>` instructions above.

If you get a compilation error like ``'wchar.h' file not found``, you can resolve it in macOS 10.14 by installing some additional header files::

    open /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg

After installing Pandana, running :code:`examples/simple_example.py` will display the number of threads that Pandana is using.  

.. _Anaconda: https://www.anaconda.com/distribution/
