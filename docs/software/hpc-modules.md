# HPC software environment

[//]: # (TODO HPC modules, Env Variables, Easybuild, ...)
## Description

On our HPCs we provide a Linux bash environment. 
The Basic Linux commands are immediately available while more elevated software packages need to be loaded. 
For managing the your environment and accessing software products we use the **module** tool Lmod. 
With Modules software packages can be enabled or disables one by one. 

!!! types note ""
    On the HPCs we provide multiple software stacks. Packages installed by us ar build for each architecture. Furthermore, VITAL-IT provides a software stack targeting mainly bioinformatics users, see [Bioinformatics Software](pre-installed-software.md#BioinformaticsSoftware).

## Basic commands
in the following you find commands for listing, loading and unloading modules. 
Later a more advanced view is presented.

### List available Modules
There are various ways to search for a software package. You can list all currently available packages using:
```Bash
module avail
```

You can search for an packages starting with a specific string, e.g. all version of GCC:
```Bash
module avail GCC
```

Furthermore, the following command list you all the modules containg a certain substring in the name, even in other software stacks:
```Bash
module spider Assambler
```
In the example above all modules with the substring *Assambler* will be listed, in this case the ones from the Vital-It software stack. 

### Load/Add a Modules

```Bash
module load OpenMPI/3.1.3-GCC-8.2.0-2.31.1
```

or equivalently:

```Bash
$ module add OpenMPI/3.1.3-GCC-8.2.0-2.31.1
```

!!! types note ""
    This may also load modules of dependencies, e.g. by loading OpenMPI, other modules like GCC and libraries are additionally loaded.

### List all Loaded Modules

```Bash
$ module list

Currently Loaded Modules:
  1) GCCcore/8.2.0                    3) binutils/.2.31.1-GCCcore-8.2.0 (H)   5) numactl/2.0.12-GCCcore-8.2.0       7) libxml2/.2.9.8-GCCcore-8.2.0     (H)   9) hwloc/1.11.11-GCCcore-8.2.0
  2) zlib/.1.2.11-GCCcore-8.2.0 (H)   4) GCC/8.2.0-2.31.1                     6) XZ/.5.2.4-GCCcore-8.2.0      (H)   8) libpciaccess/.0.14-GCCcore-8.2.0 (H)  10) OpenMPI/3.1.3-GCC-8.2.0-2.31.1

  Where:
   H:  Hidden Module
```

### Unload/remove a Modules

!!! types note ""
    This will only unload the specified modulefile, but not the dependencies that where automatically loaded when loading the specified modulefile (see purge below).

```Bash
$ module unload OpenMPI/3.1.3-GCC-8.2.0-2.31.1
```
or equivalently:

```Bash
$ module rm OpenMPI/3.1.3-GCC-8.2.0-2.31.1
```

### Purge all Modules

!!! types note ""
    This will unload all previously loaded modulefiles.

```Bash
$ module purge
```


### Show information

Most modules provide a short description which software package they contain and a link to the homepage, as well as information about the changes of environment undertaken. From short to full detail:

```Bash
$ module whatis OpenMPI
```

```Bash
$ module help OpenMPI
```

```Bash
$ module show OpenMPI
```

## Modules background

### Architectural software stacks

On our HPCs we use LMOD (Lua modules) to provide access to different software packages and different versions. Beside different packages and versions, we provide software stacks build for the different CPU architectures. This enables us to have the packages build e.g. with AVX2 for Broadwell CPUs, but also a version with only SSE4 for Sandy bridge CPUs. These software stacks are completely transparent to the user and will be used automatically when loading a module on the related architecture. 

If you want to build your own software build for specific Hardware, we provide tools which help you, see [Installing Custom Software](installing-custom-software.md)

### Scientific Software Managment

Our scientific software stack, available via module files are mainly build with Easybuild. This tool helps us to install and maintian software packages and recycle existing installation procedures. There are plenty of install instructions available [Easybuild/Easyconfigs](https://github.com/easybuilders/easybuild-easyconfigs), which can be installed also in the user space with low effort, see [Installing Custom Software](installing-custom-software.md)