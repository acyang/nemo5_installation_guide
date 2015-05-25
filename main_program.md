# 4.編譯主程式
```
cd prototype
./configure --with-vtk=../libs/vtk --with-vtk-version=-5.10 --with-boost=../libs/boost  --with-boost-libdir=../libs/boost/lib --with-hdf5=../libs/hdf5/hdf5-1.8.10-patch1/bin/h5cc --with-petsc-version="3.4.3"  --with-petsc-real-arch=linux --with-petsc-complex-arch=linux-complex --with-slepc-version="3.4.3" --with-slepc-real-arch=linux --with-slepc-complex-arch=linux-complex --with-arpack=../libs/ARPACK CC=mpiicc CXX=mpiicpc FC=mpiifort F77=mpiifort MPICC=mpiicc MPICXX=mpiicpc PYTHON=/pkg/biology/Nemo5/Nemo5_intel/libs/python/bin/python LD_LIBRARY_PATH=/pkg/biology/Nemo5/Nemo5_intel/libs/python/lib:$LD_LIBRARY_PATH
mv make.inc make.inc.bak
ln -s ../make.inc make.inc
make clean
mkdir bin
make -j 16
```
Nemo5編譯出的執行檔會放在prototype/bin裡面，但是該目錄不存在，所以需要在make之前手動建立。
