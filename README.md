## Metareposotory to experiment with EWE & MOOSE on NVIDIA GPUs

Software Atelier: Supercomputing and Simulations '2015 @ the University of Lugano

Course project

### How to build in Linux

```
$ git clone https://github.com/apc-llc/cudabernus.git
$ cd cudabernus
$ git submodule init
$ git submodule update
$ cd moose
$ git submodule init
$ git submodule update
$ cd ../petsc
$ ./configure --prefix=$(pwd)/install
$ make MAKE_NP=12
$ make PETSC_DIR=$(pwd) PETSC_ARCH=arch-linux2-c-debug install
$ cd ..
$ cd moose/libmesh
$ mkdir build
$ cd build
$ ../configure --prefix=$(pwd)/../installed --enable-openmp PETSC_DIR=$(pwd)/../../../petsc PETSC_ARCH=arch-linux2-c-debug LIBS="-L$(pwd)/../../../petsc/arch-linux2-c-debug/lib -lpetsc -lblas"
$ CPLUS_INCLUDE_PATH=$(pwd)/../../../petsc/install/include make -j12
$ make install
$ cd ../../..
$ cd ewe
$ NVCC=$(which nvcc) PATH=.:$PATH CPLUS_INCLUDE_PATH=$(pwd)/../petsc/install/include make -j12
```

### How to build on CSCS Piz Daint

```
$ module switch PrgEnv-cray PrgEnv-gnu
$ module load cudatoolkit
$ module load openblas
$ git clone https://github.com/apc-llc/cudabernus.git
$ cd cudabernus
$ git submodule init
$ git submodule update
$ cd moose
$ git submodule init
$ git submodule update
$ cd ../petsc
$ ./configure --prefix=$(pwd)/install --with-cc=cc --with-cxx=CC --with-fc=ftn --with-f77=ftn
$ make MAKE_NP=12
$ make PETSC_DIR=$(pwd) PETSC_ARCH=arch-linux2-c-debug install
$ cd ..
$ cd moose/libmesh
$ mkdir build
$ cd build
$ CC=cc CXX=CC ../configure --prefix=$(pwd)/../installed --enable-openmp PETSC_DIR=$(pwd)/../../../petsc PETSC_ARCH=arch-linux2-c-debug LIBS="-L$(pwd)/../../../petsc/arch-linux2-c-debug/lib -lpetsc -Wl,-rpath=$(pwd)/../../../petsc/arch-linux2-c-debug/lib -L$BLASDIR -lopenblas"
$ CPLUS_INCLUDE_PATH=$(pwd)/../../../petsc/install/include make -j12
$ make install
$ cd ../../..
$ cd ewe
$ NVCC=$(which nvcc) PATH=.:$PATH CPLUS_INCLUDE_PATH=$(pwd)/../petsc/arch-linux2-c-debug/include make -j12
```

