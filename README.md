## Metareposotory to experiment with EWE & MOOSE on NVIDIA GPUs

Software Atelier: Supercomputing and Simulations '2015 @ the University of Lugano

Course project

### How to get entire thing to work

```
$ git clone https://github.com/apc-llc/cudabernus.git
$ git submodule init
$ git submodule update
$ cd moose
$ git submodule init
$ git submodule update
$ cd petsc
$ ./configure --prefix=$(pwd)/install
$ make MAKE_NP=12
$ make PETSC_DIR=$(pwd) PETSC_ARCH=arch-linux2-c-debug install
$ cd ..
$ cd moose/libtool
$ mkdir build
$ cd build
$ ../configure --prefix=$(pwd)/../installed --enable-openmp PETSC_DIR=$(pwd)/../../../petsc/install 
$ make -j12
$ make install
$ cd ../../..
$ cd ewe
$ make -j12
```
