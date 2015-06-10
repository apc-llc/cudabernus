## Metareposotory to experiment with EWE & MOOSE on NVIDIA GPUs

Software Atelier: Supercomputing and Simulations '2015 @ the University of Lugano

Course project

### How to get entire thing to work

```
$ git clone https://github.com/apc-llc/cudabernus.git
$ cd cudabernus
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
$ cd moose/libmesh
$ mkdir build
$ cd build
$ ../configure --prefix=$(pwd)/../installed --enable-openmp LIBS="-L$(pwd)/../../../petsc/install/lib -lpetsc -lblas"
$ CPLUS_INCLUDE_PATH=$(pwd)/../../../petsc/install/include make -j12
$ make install
$ cd ../../..
$ cd ewe
$ NVCC=$(which nvcc) PATH=.:$PATH CPLUS_INCLUDE_PATH=$(pwd)/../petsc/install/include make -j12
```
