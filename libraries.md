# 3.編譯函式庫
準備好底層函式庫之後，回到libs根據實際上要使用的編譯器、函式庫的版本、安裝路徑餵給./configure，他會在需要編譯的函式庫資料夾產生Makefil以及make.inc，如果心臟夠大顆可以直接使用build.sh直接批次編譯，但是我還是喜歡一個一個編完確定結果。
```
cd libs
./configure --with-vtk=vtk --with-vtk-version=-5.10 --with-hdf5=hdf5/hdf5-1.8.10-patch1/bin/h5cc --with-petsc-version="3.4.3" --with-petsc-real-arch=linux --with-petsc-complex-arch=linux-complex --with-slepc-version="3.4.3" --with-slepc-real-arch=linux  --with-slepc-complex-arch=linux-complex --with-arpack=ARPACK --with-libmesh-version="0.9.2.1" --with-tao-version="2.2.0" CC=icc CXX=icpc FC=ifort F77=ifort MPICC=mpiicc MPICXX=mpiicpc MPIFC=mpiifort MPIF77=mpiifort PYTHON=python/bin/python LD_LIBRARY_PATH=/pkg/biology/Nemo5/Nemo5_intel/libs/python/lib:$LD_LIBRARY_PATH
```

* ARPACK
```
cd ARPACK
mv make.inc make.inc.bak
ln -s ../make.inc make.inc
make
```
註：mpif77不要傻傻設為mpif77要設為mpiifort，不然後面slepc在link時就會出錯。
* AMD
```
cd AMD
mv make.inc make.inc.bak
ln -s ../make.inc make.inc
make
```
* UMFPACK
```
cd UMFPACK
mv make.inc make.inc.bak
ln -s ../make.inc make.inc
make
```
* silo
```
cd silo
mv make.inc make.inc.bak
ln -s ../make.inc make.inc
make
```
註：有4.10.2可以嘗試。
* qhull
```
cd qhull-2010.1
mv make.inc make.inc.bak
ln -s ../make.inc make.inc
make
```
註：有2012.1可以嘗試。
* tensor3D
```
cd tensor3D
mv make.inc make.inc.bak
ln -s ../make.inc make.inc
make
```
* tetgen
```
cd tetgen1.4.3
mv make.inc make.inc.bak
ln -s ../make.inc make.inc
make
```
註：在Makefile裡會把CXXFLAGS和PRECXXFLAGS設為-O0，不要積極最佳化，避免執行時出錯。
* krp
```
cd krp
vi Makefile
make
```
註：修正編譯器名稱以及PAPI路徑。

Makefile內容如下
```
all: krp-init.o krp-rpt-init.o krp-rpt-init-sum.o krp-rpt.o get-crnd.o example.o
	mpiicc --version
	mpiifort --version
	mpiifort -c f-usr-krp.f90
	mpiifort -o xfusrkrp f-usr-krp.o krp-init.o krp-rpt-init.o krp-rpt-init-sum.o krp-rpt.o get-crnd.o -lm -L/usr/lib64 -lpapi


example: example.o krp-init.o krp-rpt.o
	mpiicpc -o example.bin example.o krp-init.o krp-rpt.o -lm -L/usr/lib64 -lpapi

.cpp.o:
	mpiicpc -c $< -DAdd_ -I /usr/include

.c.o:
	mpiicc -c $< -I /usr/include

clean:
	rm *.o

```

以下套件均有相依性，請依序安裝。
* petsc
```
cd petsc
mv make.inc make.inc.bak
ln -s ../make.inc make.inc
make
```
修改Makefile

```
# -------------------------------------------------------------
# NEMO 5 Makefile for PETSc - both double and complex version
# Sebastian Steiger, steiger@purdue.edu, Mar-Aug 2010
# -------------------------------------------------------------

# get compilers
include ./make.inc

PETSC_VERSION   := petsc-$(PETSC_VERSION)

COMPILERS = --with-cc="$(MPICC)" --with-fc="$(MPIF90)" --with-cxx="$(MPICXX)" COPTFLAGS="$(O_LEVEL)" CXXOPTFLAGS="$(O_LEVEL)" FOPTFLAGS="$(O_LEVEL)" --CFLAGS="$(CFLAGS)" --CXXFLAGS="$(CXXFLAGS)" --FFLAGS="$(FFLAGS) $(FCFLAGS)" --LDFLAGS="$(LDFLAGS)" --with-cmake=$(CMAKE)
# COMPILERS = --with-mpi-dir=$(MPI_HOME)

BLAS_LAPACK     = --with-blas-lapack-dir="$(MKLROOT)"

# for RCAC machines make ABSOLUTELY sure:
# - you have no modules loaded except mpich2-1.2.1-gcc64 or whatever MPI compiler you use (and its dependencies)
# - your LD_LIBRARY_PATH contains only the MPI directory and the directory of the underlying compiler
# - your PATH probably should also contain very few entries
# you might have to enter your RCAC password once during each configuration

# Random notes:
# - PETSc 3.1 is NOT compatible with SLEPc-3.0!!! reconfirmed w/ SLEPc team.
# - hypre is only for real matrices
# - blacs is mandatory for scalapack, scalapack is mandatory for mumps
#
# do not install! no prefix --> no install.
# shared libs: do not forget to specify "shared" for make all


all: $(PETSC_VERSION)/configure real cplx incl conf/variables $(PETSC_REAL_ARCH)/lib/libpetsc.a $(PETSC_CPLX_ARCH)/lib/libpetsc.a $(PETSC_REAL_ARCH)/lib/libsuperlu_dist.a
#all: incl conf/variables $(PETSC_REAL_ARCH)/lib/libpetsc.so $(PETSC_CPLX_ARCH)/lib/libpetsc.so $(PETSC_REAL_ARCH)/lib/libsuperlu_dist.a


$(PETSC_VERSION)/configure:
	tar zxvf $(PETSC_VERSION).tar.gz


real:
	@echo "##################################################################"
	@echo "#                                                                #"
	@echo "#                  build DOUBLE version of PETSc                 #"
	@echo "#                                                                #"
	@echo "##################################################################"
	@echo "Creating symbolic links in build-real/ directory..."
	(mkdir -p build-real; \
	 cd build-real; \
	 lndir ../$(PETSC_VERSION)/; \
	 export PETSC_DIR=$(PETSC_REAL_BUILD); \
	 export PETSC_ARCH=$(PETSC_REAL_ARCH); \
	 export LD_LIBRARY_PATH=$(PYTHONHOME)/lib:$(LD_LIBRARY_PATH); \
	 echo "Starting REAL configure-make process..."; \
	 $(PYTHON_BIN) ./config/configure.py --with-x=0 --with-hdf5 --with-hdf5-dir=$(HDF5_DIR) --with-scalar-type=real --with-single-library=0  --with-pic=1 --with-shared-libraries=0 $(BLAS_LAPACK) --with-clanguage=C++ --with-fortran --with-debugging=1 $(COMPILERS) --download-metis=1 --download-parmetis=1 --download-superlu_dist=1 --download-mumps=1 --with-boost --with-boost-dir=$(BOOST_DIR) --with-scalapack --with-scalapack-include=$(MKLROOT)/include --with-scalapack-lib="-L$(MKLROOT)/lib/intel64 -lmkl_scalapack_lp64 -lmkl_intel_lp64 -lmkl_core -lmkl_sequential -lmkl_blacs_intelmpi_lp64 -lpthread -lm" --with-blacs-include=$(MKLROOT)/include --with-blacs-lib="-L$(MKLROOT)/lib/intel64 -lmkl_blacs_intelmpi_lp64"; \
	 make PETSC_DIR=$(PETSC_REAL_BUILD) PETSC_ARCH=$(PETSC_REAL_ARCH) shared all; )
	@echo "Linking petsc/$(PETSC_REAL_ARCH)/ directory..."
	@(rm -rf $(PETSC_REAL_ARCH)/; mkdir $(PETSC_REAL_ARCH)/; cd $(PETSC_REAL_ARCH)/; lndir ../build-real/$(PETSC_REAL_ARCH)/)


cplx:
	@echo "##################################################################"
	@echo "#                                                                #"
	@echo "#                  build COMPLEX version of PETSc                #"
	@echo "#                                                                #"
	@echo "##################################################################"
	@echo "Creating symbolic links in build-cplx/ directory..."
	(mkdir -p build-cplx; \
	 cd build-cplx; \
	 lndir ../$(PETSC_VERSION)/; \
	 export PETSC_DIR=$(PETSC_CPLX_BUILD); \
	 export PETSC_ARCH=$(PETSC_CPLX_ARCH); \
	 export LD_LIBRARY_PATH=$(PYTHONHOME)/lib:$(LD_LIBRARY_PATH); \
	 echo "Starting COMPLEX configure-make process..."; \
	 $(PYTHON_BIN) ./config/configure.py --with-x=0 --with-hdf5 --with-hdf5-dir=$(HDF5_DIR) --with-scalar-type=complex --with-single-library=0 --with-pic=1 --with-shared-libraries=0 $(BLAS_LAPACK) --with-clanguage=C++ --with-fortran --with-debugging=1 $(COMPILERS) --download-metis=1 --download-parmetis=1 --download-superlu_dist=1 --download-mumps=1 --with-boost --with-boost-dir=$(BOOST_DIR) --with-scalapack --with-scalapack-include=$(MKLROOT)/include --with-scalapack-lib="-L$(MKLROOT)/lib/intel64 -lmkl_scalapack_lp64 -lmkl_intel_lp64 -lmkl_core -lmkl_sequential -lmkl_blacs_intelmpi_lp64 -lpthread -lm" --with-blacs-include=$(MKLROOT)/include --with-blacs-lib="-L$(MKLROOT)/lib/intel64 -lmkl_blacs_intelmpi_lp64"; \
	 make PETSC_DIR=$(PETSC_CPLX_BUILD) PETSC_ARCH=$(PETSC_CPLX_ARCH) shared all; )
	@echo "Linking petsc/$(PETSC_CPLX_ARCH)/ directory..."
	(rm -rf $(PETSC_CPLX_ARCH)/; mkdir $(PETSC_CPLX_ARCH)/; cd $(PETSC_CPLX_ARCH)/; lndir ../build-cplx/$(PETSC_CPLX_ARCH)/)


incl:
	@echo "Linking petsc/include/ directory..."
	(rm -rf include/; mkdir include/; cd include/; lndir ../$(PETSC_VERSION)/include/)

test:
	(cd build-real; make PETSC_DIR=$(PETSC_REAL_BUILD) PETSC_ARCH=$(PETSC_REAL_ARCH) LD_LIBRARY_PATH=$(PYTHONHOME)/lib:$(LD_LIBRARY_PATH) test)
	(cd build-cplx; make PETSC_DIR=$(PETSC_CPLX_BUILD) PETSC_ARCH=$(PETSC_CPLX_ARCH) LD_LIBRARY_PATH=$(PYTHONHOME)/lib:$(LD_LIBRARY_PATH) test)

# conf/variables is necessary for libmesh
conf/variables:
	mkdir -p conf
	cp build-real/conf/variables conf/.

# starting with petsc 3.1 libpetsc.{a,so} is called libpetscsys.{a,so}
# the following commands will only be executed if libpetsc.so does not exist, i.e. only for >=3.1
$(PETSC_REAL_ARCH)/lib/libpetsc.so:
	cp $(PETSC_REAL_ARCH)/lib/libpetscsys.so $(PETSC_REAL_ARCH)/lib/libpetsc.so
$(PETSC_CPLX_ARCH)/lib/libpetsc.so:
	cp $(PETSC_CPLX_ARCH)/lib/libpetscsys.so  $(PETSC_CPLX_ARCH)/lib/libpetsc.so
$(PETSC_REAL_ARCH)/lib/libpetsc.a:
	cp $(PETSC_REAL_ARCH)/lib/libpetscsys.a  $(PETSC_REAL_ARCH)/lib/libpetsc.a
$(PETSC_CPLX_ARCH)/lib/libpetsc.a:
	cp $(PETSC_CPLX_ARCH)/lib/libpetscsys.a $(PETSC_CPLX_ARCH)/lib/libpetsc.a

# libsuperlu has the version number attached. to circumvent this obstacle we copy whatever version
# is included to version 2.3 (which is the one provided with petsc 3.0.0
$(PETSC_REAL_ARCH)/lib/libsuperlu_dist.a:
	cp $(PETSC_REAL_ARCH)/lib/libsuperlu_dist_*.a $(PETSC_REAL_ARCH)/lib/libsuperlu_dist.a
	cp $(PETSC_CPLX_ARCH)/lib/libsuperlu_dist_*.a $(PETSC_CPLX_ARCH)/lib/libsuperlu_dist.a


clean:
	rm -rf build-real build-cplx conf  include  linux  linux-complex

```
註：有3.5.4可以嘗試。
* slepc
```
cd slepc
mv make.inc make.inc.bak
ln -s ../make.inc make.inc
make
```
修改Makefile

```
# NEMO 5 Makefile for SLEPc - both double and complex version

# get compilers
include ./make.inc

#ARPACK_DIR      = $(PWD)/../ARPACK
#ARPACK_DIR      = $(PWD)/../ARPACK2/ARPACK
ARPACK_LINK = $(ARPACK_DIR)
#ARPACK_LINK = /usr/lib

#SLEPC_VERSION   = slepc-3.3-p3
SLEPC_VERSION   := slepc-$(SLEPC_VERSION)

# PETSc 3.1 is NOT compatible with SLEPc-3.0!!! reconfirmed w/ SLEPc team.

# do not install! no prefix specified --> no install


all: $(SLEPC_VERSION)/configure real cplx incl


$(SLEPC_VERSION)/configure:
	tar zxvf $(SLEPC_VERSION).tgz


real:
	@echo "##################################################################"
	@echo "#                                                                #"
	@echo "#                  build DOUBLE version of SLEPc                 #"
	@echo "#                                                                #"
	@echo "##################################################################"
	@echo "Creating symbolic links in build-real/ directory..."
	(mkdir -p build-real; \
	 cd build-real; \
	 lndir ../$(SLEPC_VERSION)/; \
	 export PETSC_DIR=$(PETSC_REAL_BUILD); \
	 export PETSC_ARCH=$(PETSC_REAL_ARCH); \
	 export SLEPC_DIR=$(SLEPC_REAL_BUILD); \
	 export LD_LIBRARY_PATH=$(PYTHONHOME)/lib:$(LD_LIBRARY_PATH); \
	 $(PYTHON_BIN) ./configure --with-arpack --with-arpack-dir=$(ARPACK_DIR); \
	 make PETSC_DIR=$(PETSC_REAL_BUILD) PETSC_ARCH=$(PETSC_REAL_ARCH) SLEPC_DIR=$(SLEPC_REAL_BUILD) all; )
	@echo "Linking slepc/$(PETSC_REAL_ARCH)/ directory..."
	(rm -rf $(PETSC_REAL_ARCH)/; mkdir -p $(PETSC_REAL_ARCH)/; cd $(PETSC_REAL_ARCH)/; lndir ../build-real/$(PETSC_REAL_ARCH)/)


cplx:
	@echo "##################################################################"
	@echo "#                                                                #"
	@echo "#                  build COMPLEX version of SLEPc                #"
	@echo "#                                                                #"
	@echo "##################################################################"
	@echo "Creating symbolic links in build-cplx/ directory..."
	(mkdir -p build-cplx; \
	 cd build-cplx; \
	 lndir ../$(SLEPC_VERSION)/; \
	 export PETSC_DIR=$(PETSC_CPLX_BUILD); \
	 export PETSC_ARCH=$(PETSC_CPLX_ARCH); \
	 export SLEPC_DIR=$(SLEPC_CPLX_BUILD); \
	 export LD_LIBRARY_PATH=$(PYTHONHOME)/lib:$(LD_LIBRARY_PATH); \
	 $(PYTHON_BIN) ./configure --with-arpack --with-arpack-dir=$(ARPACK_DIR);\
	 make PETSC_DIR=$(PETSC_CPLX_BUILD) PETSC_ARCH=$(PETSC_CPLX_ARCH) SLEPC_DIR=$(SLEPC_CPLX_BUILD) all; )
	@echo "Linking slepc/$(PETSC_CPLX_ARCH)/ directory..."
	(rm -rf $(PETSC_CPLX_ARCH)/; mkdir -p $(PETSC_CPLX_ARCH)/; cd $(PETSC_CPLX_ARCH)/; lndir ../build-cplx/$(PETSC_CPLX_ARCH)/)

incl:
	@echo "Linking slepc/include/ directory..."
	(rm -rf include/; mkdir include/; cd include/; lndir ../$(SLEPC_VERSION)/include/)

# test example
# ./ex1 -n 2000 -eps_nev 5 -eps_ncv 60 -eps_max_it 400 -eps_tol 1e-6 -eps_monitor_draw -eps_type arnoldi
ex1:
	(cd build-real/src/eps/examples/tutorials;\
	$(MPICXX) $(CPPFLAGS) -I../../../../include -I../../../../linux/include -I../../../../../../petsc/build-real/include  -I../../../../../../petsc/linux/include $(VALGRIND_INCLUDE)  \
	   -o ex1 ex1.c \
	   $(MPI_LIBS) -lz $(LDFLAGS) -lifport -Wl,-rpath,$(MKL_HOME)/lib/intel64 -L$(MKL_HOME)/lib/intel64 -lifcore  -lmkl_scalapack_lp64 -lmkl_blacs_intelmpi_lp64   $(LAPACK) $(MPI_LIBS)  -Wl,-rpath,../../../../../linux/lib -L../../../../../linux/lib -lslepc  -Wl,-rpath,$(PETSC_REAL_LIBDIR) -L$(PETSC_REAL_LIBDIR) $(PETSC_LIBS)  $(PETSC_EXT_LIBS_REAL)  $(HDF5_LIBS)  $(ARPACK))
#	(cd build-cplx/src/examples; \
#	$(MPICXX) -I../../include -I../../../../../../petsc/include  -I../../../../../../petsc/linux-complex/include \
#	   -o ex1 ex1.c \
#	   -Wl,-rpath,../../../../../linux-complex/lib -L../../../../../linux-complex/lib -lslepc $(ARPACK) \
#	   -Wl,-rpath,../../../../../../petsc/linux-complex/lib -L../../../../../../petsc/linux-complex/lib $(PETSC_LIBS))

clean:
	rm -rf build-*/ include/ linux*/ $(SLEPC_VERSION)/
```
註：有3.5.4可以嘗試。
* libmesh
```
cd libmesh
mv make.inc make.inc.bak
ln -s ../make.inc make.inc
make
```
Makefile

```
# get PETSC_DIR, PETSC_ARCH and MPIHOME from NEMO 5 build system
#LIBMESH_VERSION = 0.8.0
include ./make.inc

#all: libmesh/configure static dynamic
all: libmesh/configure dynamic
# <ss 12/09/10> static stuff is only needed on jaguar

libmesh/configure:
	@echo "Extracting libmesh-$(LIBMESH_VERSION).tar.gz..."
	tar zxf libmesh-$(LIBMESH_VERSION).tar.gz

# <ss 17.7.2010> PETSc now is mandatory for libmesh - however, libmesh takes MPI configuration from petsc configuration files in that case.
# libmesh searches for $PETSC_DIR/include/petsc.h and needs $PETSC_ARCH to be set
# On nanohub, things got messed up and OpenMIP libraries linked to executables. to prevent this, I had to disable VTK within libmesh.
# <ss 13.8.2010> disabled tetgen because libtetgen.a seems to contain an int main() which makes static linking impossible.
# Note: the 'make clean' before 'make all' for the contributions is mandatory, otherwise shared LASPACK will not compile.

static: libmesh/configure
	@echo "###########################################"
	@echo "#                                         #"
	@echo "# Configuring Libmesh (STATIC libraries)  #"
	@echo "#                                         #"
	@echo "###########################################"
	(export libmesh_CXXFLAGS=$(libmesh_CXXFLAGS) ; \
	export libmesh_INCLUDE=$(libmesh_INCLUDE); \
	export SLEPC_DIR=$(SLEPC_REAL_BUILD); \
	cd libmesh-$(LIBMESH_VERSION); ./configure --prefix=$(LIBMESH_DIR) PETSC_DIR=$(PETSC_REAL_BUILD) PETSC_ARCH=$(PETSC_REAL_ARCH) SLEPC_DIR=$(SLEPC_REAL_BUILD) MPIHOME=$(MPIHOME) FC="$(MPIF90)" F77="$(MPIF90)" CC="$(MPICC)" CXX="$(MPICXX)" GCC="$(GCC)" --enable-vtk --with-vtk-include=$(VTKINC_PATH) \
--with-vtk-lib=$(VTKLIB_PATH) --disable-tetgen --disable-nemesis --disable-examples --disable-glpk --disable-tecplot \
--enable-parmesh --enable-amr --disable-shared --enable-slepc --enable-legacy-include-paths --with-metis=PETSc --with-methods=opt --enable-hdf5 --with-hdf5=$(HDF5_DIR) --enable-boost --with-boost=$(BOOST_DIR); \
	make clean; make; \
	cd contrib; make clean; make all; cd ..;)

dynamic: libmesh/configure
	@echo "###########################################"
	@echo "#                                         #"
	@echo "# Configuring Libmesh (DYNAMIC libraries) #"
	@echo "#                                         #"
	@echo "###########################################"
	(export libmesh_CXXFLAGS=$(libmesh_CXXFLAGS); \
	export libmesh_CPPFLAGS=$(libmesh_CPPFLAGS); \
	export libmesh_INCLUDE=$(libmesh_INCLUDE); \
	export SLEPC_DIR=$(SLEPC_REAL_BUILD); \
	cd libmesh-$(LIBMESH_VERSION); ./configure --prefix=$(LIBMESH_DIR) PETSC_DIR=$(PETSC_REAL_BUILD) PETSC_ARCH=$(PETSC_REAL_ARCH) SLEPC_DIR=$(SLEPC_REAL_BUILD) MPIHOME=$(MPIHOME) FC="$(MPIF90)" F77="$(MPIF90)" CC="$(MPICC)" CXX="$(MPICXX)" GCC="$(GCC)" --enable-vtk --with-vtk-include=$(VTKINC_PATH) \
--with-vtk-lib=$(VTKLIB_PATH) --disable-tetgen --disable-nemesis --disable-examples --disable-glpk \
--enable-parmesh --enable-amr --enable-shared --enable-slepc --enable-legacy-include-paths --with-metis=PETSc --with-methods=opt --enable-hdf5 --with-hdf5=$(HDF5_DIR) --enable-boost --with-boost=$(BOOST_DIR); \
	make clean; make -j 8; \
	cd contrib; make clean; make -j 8 all; cd ..;)

clean:
	cd libmesh-$(LIBMESH_VERSION); make clean

```
註：有0.9.4可以嘗試。
* TAO
```
cd TAO
mv make.inc make.inc.bak
ln -s ../make.inc make.inc
make
```
Makefile第40行~~PETSC_ARCH=$(PETSC_ARCH_REAL)~~要改成PETSC_ARCH=$(PETSC_REAL_ARCH)

註：有2.2.2可以嘗試。
