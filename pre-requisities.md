#1.編譯前準備

先準備好咖啡和披薩，以及一顆愉快的心。

NEMO5的編譯相依於許多函式庫，下圖代表的是這些函式庫的相依關係。
![](https://docs.google.com/drawings/d/1m1TBePrY2XmDlTR_a1IOcLhuyTXrUtb7K9uU5FjmhBE/pub?w=960&h=720)
圖例說明

0: make, cmake, imake, valgrind, papi opengl使用系統自帶的即可。

1: C/C++, Fortran compiler, MPI library, MKL library在1.1節中說明。

2: VTK, python, boost, hdf5在2章中說明。

3: arpack, amd, umfpack, silo tensor3D, tetgen, qhull, krp在3章說明。

3a~3c: petsc, slepc, libmesh, tao有相依關係請依序安裝在3章說明。
