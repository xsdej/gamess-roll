# SDSC "gamess" roll

## Overview

This roll bundles the GAMESS quantum chemistry package.

For more information about the various packages included in the gamess roll please visit their official web pages:

- <a href="http://www.msg.chem.iastate.edu/GAMESS/" target="_blank">GAMESS</a> is a general ab initio quantum chemistry package.


## Requirements

To build/install this roll you must have root access to a Rocks development
machine (e.g., a frontend or development appliance).

If your Rocks development machine does *not* have Internet access you must
download the appropriate gamess source file(s) using a machine that does
have Internet access and copy them into the `src/gamess` directories on your
Rocks development machine.


## Dependencies

The sdsc-roll must be installed on the build machine, since the build process
depends on make include files provided by that roll.

The roll sources assume that modulefiles provided by SDSC compiler and mpi
rolls are available, but it will build without them as long as the environment
variables they provide are otherwise defined.

The build process requires the MKL libraries and assumes that the mkl
modulefile provided by the SDSC intel-roll is available.  It will
build without the modulefile as long as the environment variables it provides
are otherwise defined.


## Building

To build the gamess-roll, execute this on a Rocks development
machine (e.g., a frontend or development appliance):

```shell
% make 2>&1 | tee build.log
```

A successful build will create the file `gamess-*.disk1.iso`.  If you built the
roll on a Rocks frontend, proceed to the installation step. If you built the
roll on a Rocks development appliance, you need to copy the roll to your Rocks
frontend before continuing with installation.

This roll source supports building with different compilers and for different
MPI flavors.  The `ROLLCOMPILER` and `ROLLMPI` make variables can be used to
specify the names of compiler and MPI modulefiles to use for building the
software, e.g.,

```shell
make ROLLCOMPILER=intel ROLLMPI=mvapich2_ib 2>&1 | tee build.log
```

The build process recognizes "gnu", "intel" or "pgi" as the value for the
`ROLLCOMPILER` variable; any MPI modulefile name may be used as the value of
the `ROLLMPI` variable.  The default values are "gnu" and "rocks-openmpi".


## Installation

To install, execute these instructions on a Rocks frontend:

```shell
% rocks add roll *.iso
% rocks enable roll gamess
% cd /export/rocks/install
% rocks create distro
% rocks run roll gamess | bash
```

In addition to the software itself, the roll installs gamess environment
module files in:

```shell
/opt/modulefiles/applications/gamess
```


## Testing

The gamess-roll includes a test script which can be run to verify proper
installation of the roll documentation, binaries and module files. To
run the test scripts execute the following command(s):
Note that a total of 47 tests are run and they will take ~8 minutes to finish

```shell
% /root/rolltests/gamess.t 
```
