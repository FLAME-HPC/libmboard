# libmboard: the Message Board Library
        
The Message Board Library is a data management and communication library
developed  for  multi-agent  simulations  generated using the FLAME framework.

As agents only interact with its environment (and each other) via messages,
the Message Board library serves as a means of achieving parallelisation.
Agents can be farmed out across multiple processors and simulated concurrently,
while a coherent simulation is maintained through a unified view of the
distributed Message Boards.

Synchronisation of the message boards are non-blocking as they are performed on
a separate communication  thread, allowing much of the communication time to be
overlapped with computation.

Copyright (c) 2007-2012 STFC Rutherford Appleton Laboratory

## Getting help

If you have any problems or enquiries, you should 
[raise a GitHub issue](https://github.com/FLAME-HPC/libmboard/issues).
      
## Requirements

You will need the following:

  * a **C compiler**, e.g. GCC 
  * GNU **Make**
  * **libtool**

If you are building on Linux then you will likely already have those installed.

If you want to build libmboard from a **clone of the libmboard Git repository** (very likely)
then you will also need:

  * GNU **Autoconf** (version >= 2.56)
  * GNU **Automake** (version >= 1.8)

Again, if you are building on Linux then you will likely already have those installed.

To compile the **parallel version** of the library, you will also need:

  * An **MPI** implementation, e.g. [MPICH](http://www.mcs.anl.gov/research/projects/mpich2/) or [OpenMPI](https://www.open-mpi.org)
  * Support for [**pthreads**](http://en.wikipedia.org/wiki/POSIX_Threads)

To generate the **documentation**, you will also need:

  * [**Doxygen**](http://www.doxygen.org)

To compile the **unit tests**, you will also need:

  * [**CUnit**](http://cunit.sourceforge.net/)

### Installation

1. (Only) if you are trying to build libmboard from a clone of the libmboard Git repository,
   you first need to run:

       $ ./autogen.sh
  
2. Configure the source using the `./configure` script. 
   This will prepare the source code and check that all pre-requisites are met.
   
       $ ./configure
   
   **Changing installation directory:**
   By default, the library will be configure for installation within your
   system (typically in `/usr/local` for Linux systems). This will allow users
   to link to the library without having to specify the library location.  This
   however would require you to have administrator privileges (root).
   
   If you wish to change the installation destination (this may be necessary if
   you do not have root access, of if you wish to maintain multiple versions of
   the library), you can use the `--prefix` option to specify an alternative
   installation location. 
   
       $ ./configure --prefix=/home/lsc/build/libmboard
   
   **Disabling some components:**
   You can disable the inclusion of unit tests (if you do not have CUnit)
   by appending `--disable-tests` to the list of arguments to `./configure`.
   
   You can also disable the compilation of parallel libraries (if you do not
   have pthreads and MPI support) by appending the `--disable-parallel`
   argument to `./configure`.
   
   **More options:**
   For more configuration options, run 
   
       $ ./configure --help
   
2. Once the configuration is successful, you can compile and install the 
   library.
   
       $ make 
       $ make install
   
For more details on installation, see the [INSTALL](INSTALL) file.

## Using the library

For information on how to use the library, view the User Manual. 
The manual can be generated by running:

    $ make doc

You can then view the user documentation using:

    $ firefox doc/user/html/index.html

And view the developer documentation using:

    $ firefox doc/develop/serial/html/index.html

and 

    $ firefox doc/develop/parallel/html/index.html

You can also [browse the User Manual online](http://www.softeng.rl.ac.uk/st/projects/libmboard/) 
although note that this may not correspond exactly to the version of libmboard you have installed.

## Running unit tests

Compile the tests using 

    $ make test
    
Four tests binaries will be produced, each testing different aspects of the
library.

  * `./tests/run_test_utils`           : Test utility code used by both serial and parallel modules
  * `./tests/run_test_serial`          : Test serial libmboard API
  * `./tests/run_test_parallel_utils`  : Test utility code used only by the parallel modules
  * `./tests/run_test_parallel`        : Test parallel libmboard API 
 
You will need to run the parallel tests using your standard MPI job launcher (e.g. `mpirun` or `mpiexec`).
 
## Performing Test Coverage analysis
 
Configure the package using `--enable-coverage`, and compile the code using 
 the `coverage` target:
    
    $ ./configure --enable-coverage
    $ make coverage
    
If the code compiles and the tests run successfully, 
the coverage report will be available in the `./coverage_html` directory. 
Load the `index.html` file in your favourite browser to view the report e.g.
 
    $ firefox ./coverage_html/index.html

When done, you can clean up your source directives by running

    $ make vclean

## Creating Distributions

From a developer's source tree, you can generate a distribution version by
running:

    $ ./create_distribution.sh
