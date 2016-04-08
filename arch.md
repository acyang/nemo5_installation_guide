## 1.3.選定機器環境
在NEMO5_HOME執行
```
./configure.sh custom
```
將產生make.inc以及mkfiles/make.inc.custom，還有prototype資料夾下的部分檔案。
這些檔案內定義的內容，將在編譯第三方函式庫及主程式時被使用。
根據所選擇的工具組修改make.inc以及mkfiles/make.inc.custom
make.inc
```

#############################################################################
# configure.sh substitutions
#############################################################################

# Top directory
PROJECT_TOP = /pkg/biology/Nemo5/Nemo5_intel

# Platform build type
BUILD_TYPE = custom

#############################################################################
# Should not need to edit below, unless adding new platform
#############################################################################

MAKE      = make
CMAKE     = cmake
AR        = ar
ARFLAGS   = ruv
AR_FLAGS  = ruv
RANLIB    = ranlib
CD        = cd
ECHO      = echo
LN        = ln
LNFLAGS   = -s
RM        = rm
RMFLAGS   = -f
MV        = mv
MVFLAGS   = -f
SHELL     = sh
LIB       = -lm
LEX       = flex
YACC      = bison

USER = $(shell whoami)


#<ss> -axP instead of -msse3; use mpich-intel-10.1.013

ifeq ($(BUILD_TYPE),custom)
include $(PROJECT_TOP)/mkfiles/make.inc.custom
endif

###########################################################################

# Top 3rd-party library directory
# set special LIB_TOP for group builds
LIB_TOP       = $(PROJECT_TOP)/libs

# Common include paths
INCAMD        = -I $(LIB_TOP)/AMD/Include/
INCUFC        = -I $(LIB_TOP)/UFconfig/
INCUMF        = -I $(LIB_TOP)/UMFPACK/Include/
#INCNEMAT      = -I $(LIB_TOP)/../MaterialDB/GroupDB -I $(LIB_TOP)/../MaterialDB/NEMat -I $(LIB_TOP)/../MaterialDB/nml/include
INCQLL        = -I $(LIB_TOP)/qhull-2010.1/cpp -I$(LIB_TOP)/qhull-2010.1/src
INCTENSOR3D   = -I $(LIB_TOP)/tensor3D
INCTET        = -I $(LIB_TOP)/tetgen1.4.3

UMFPACK_DIR=$(LIB_TOP)/UMFPACK
TETGEN_DIR =$(LIB_TOP)/tetgen1.4.3
# Common link options
ARPACK        = -Wl,-rpath,$(LIB_TOP)/ARPACK/ -L$(LIB_TOP)/ARPACK/ -lparpack -larpack
AMD           = -Wl,-rpath,$(LIB_TOP)/AMD/Lib/ -L$(LIB_TOP)/AMD/Lib/ -lamd
QHULL         = -Wl,-rpath,$(LIB_TOP)/qhull-2010.1/lib -L$(LIB_TOP)/qhull-2010.1/lib -lqhull++ -lqhull
TENSOR3D      = -Wl,-rpath,$(LIB_TOP)/tensor3D -L$(LIB_TOP)/tensor3D -ltensor
TETGEN        = -Wl,-rpath,$(LIB_TOP)/tetgen1.4.3 -L$(LIB_TOP)/tetgen1.4.3 -ltet
UMFPACK       = -Wl,-rpath,$(LIB_TOP)/UMFPACK/Lib/ -L$(LIB_TOP)/UMFPACK/Lib/ -lumfpack
MPI           = -Wl,-rpath,$(MPIHOME)/lib -L$(MPIHOME)/lib -lmpi

```


mkfiles/make.inc.custom
```
# Use this file for creating a NEMO5 build on your machine
# https://nanohub.org/groups/nemo5distribution/wiki
# The values below need to be updated for your particular machine
# This particular example using Intel compilers.


MPIHOME       = /pkg/mpi/impi/5.0.3.048/intel64
INCMPI        = -I $(MPIHOME)/include
MPI_LIBS      = -Wl,-rpath,$(MPIHOME)/lib -L$(MPIHOME)/lib -lmpi
MPIEXECTEST   = $(MPIHOME)/bin/mpiexec -n 4

INTEL_HOME= /pkg/intel/2015/composer_xe_2015.2.164
MKLHOME = /pkg/intel/2015/composer_xe_2015.2.164/mkl
MKL_HOME= /pkg/intel/2015/composer_xe_2015.2.164/mkl
#MKLHOME and MKL_HOME should be the same
#use BLAS if available
BLAS_LAPACK_DIR = $(MKL_HOME)
LAPACK          = -Wl,-rpath,$(MKL_HOME)/lib/intel64 -L$(MKL_HOME)/lib/intel64 -Wl,-rpath,$(INTEL_HOME)/compiler/lib/intel64 -L$(INTEL_HOME)/compiler/lib/intel64 -Wl,--start-group -lmkl_intel_lp64 -lmkl_intel_thread -liomp5 -lmkl_core -Wl,--end-group

F90HOME       = /pkg/intel/2015/composer_xe_2015.2.164

#gcc example
CC            = $(INTEL_HOME)/bin/intel64/icc
CXX           = $(INTEL_HOME)/bin/intel64/icpc
CXX_STATIC    = $(CXX)
CPP           = $(CXX)
MPICC         = $(MPIHOME)/bin/mpiicc
MPICXX        = $(MPIHOME)/bin/mpiicpc
GCC           = /pkg/local/gcc/4.8.3/bin/gcc
F90           = $(INTEL_HOME)/bin/intel64/ifort
F77           = $(F90)
MPIF77        = $(MPIHOME)/bin/mpiifort
MPIF90        = $(MPIHOME)/bin/mpiifort
LOADER        = $(MPICXX)

# Compiler flags
O_LEVEL       = -O3
CPPFLAGS      = $(O_LEVEL) -fPIC -DMPICH_IGNORE_CXX_SEEK -DMPICH_SKIP_MPICXX
CFLAGS        = $(O_LEVEL) -fPIC
CXXFLAGS      = $(O_LEVEL) -fPIC
LDFLAGS       =
FCFLAGS       = $(O_LEVEL) -fPIC
GCCFLAGS      = $(O_LEVEL) $(PICFLAG)
F90FLAGS      = $(O_LEVEL) -fPIC
F77_FLAGS     = $(F90FLAGS)
F77FLAGS      = $(F90FLAGS)

# Libraries
# If the various libraries are already installed on your system, you can link to them explicitly, e.g. VTK_HOME = /apps/rhel5/vtk-5.10.0
# If you build the library in the 'libs' directory, then use $(PROJECT_TOP), e.g.,  VTK_HOME = $(PROJECT_TOP)/libs/vtk


ARPACK_DIR    = $(PROJECT_TOP)/libs/ARPACK
ARPACK_LIBS   = -lparpack -larpack

BOOST_DIR     = $(PROJECT_TOP)/libs/boost
BOOST_INCLUDE = -I$(PROJECT_TOP)/libs/boost/include
LINK_BOOST     = -Wl,-rpath,$(PROJECT_TOP)/libs/boost/lib -L$(PROJECT_TOP)/libs/boost/lib -lboost_filesystem -lboost_system -lboost_regex -lboost_serialization -lboost_python

#VTK
VTKINC_PATH = $(PROJECT_TOP)/libs/vtk/include/vtk-5.10
VTKLIB_PATH = $(PROJECT_TOP)/libs/vtk/lib/vtk-5.10

INCVTK       = -I $(VTKINC_PATH)
VTK_INCLUDE = $(INCVTK)
VTK_LIB = -L $(VTKLIB_PATH)

VTK_LIBS     = -Wl,--start-group -Wl,-rpath,$(VTKLIB_PATH) -L$(VTKLIB_PATH) -lvtkFiltering -lvtkIO -lvtkCommon -lvtksys -lvtkDICOMParser  -lvtkpng -lvtkjpeg -lvtktiff -lvtkexpat -lvtkzlib -lvtkGraphics -lvtkImaging -lvtkNetCDF -lvtkNetCDF_cxx -lLSDyna -lvtkmetaio -lvtksqlite -lvtkhdf5_hl -lvtkverdict -lvtkhdf5_hl -lvtkhdf5 -Wl,--end-group

#/apps/rhel6/hdf5/1.8.10_intel-13.0.1.117
# this is set by module load
#HDF5_DIR = $(HDF5_HOME)
#use PETSc HDF5 instead

#PETSc and NEMO5 both need HDF5. They should both use the same build of HDF5, so it is straightforward to use PETSc's for both.

HDF5_DIR = $(PROJECT_TOP)/libs/hdf5/hdf5-1.8.10-patch1
HDF5_INCDIR   = $(HDF5_DIR)/include
HDF5_LIBDIR   = $(HDF5_DIR)/lib
HDF5_LIBS     = -Wl,-rpath,$(HDF5_LIBDIR) -L$(HDF5_LIBDIR) -lhdf5 -lhdf5_hl -lhdf5_fortran -lm -lrt -lz
INCHDF = -I $(HDF5_INCDIR)

SILO_FILE = silo-4.8-bsd
SILO_INC  = -I $(PROJECT_TOP)/libs/silo/include
SILO_LIBS = -Wl,-rpath,$(PROJECT_TOP)/libs/silo/lib -L$(PROJECT_TOP)/libs/silo/lib -lsiloh5  -Wl,-rpath,$(HDF5_DIR)/lib -L$(HDF5_DIR)/lib -lhdf5
CPPFLAGS      += -DSILO

VALGRIND_INCLUDE = -I /usr/include/valgrind

PETSC_VERSION = 3.4.3
PETSC_REAL_ARCH = linux
PETSC_CPLX_ARCH = linux-complex
SLEPC_VERSION = 3.4.3
SLEPC_REAL_ARCH = linux
SLEPC_CPLX_ARCH = linux-complex

PETSC_LIBS            = -lpetscsnes -lpetscts -lpetscksp -lpetscdm -lpetscmat -lpetscvec -lpetscsys
PETSC_EXT_LIBS_REAL   = -lsuperlu_dist_3.3 -lzmumps -ldmumps -lmumps_common -lpord -lparmetis -lmetis -lcmumps -lsmumps
PETSC_EXT_LIBS_CPLX   = -lsuperlu_dist_3.3 -lzmumps -ldmumps -lmumps_common -lpord -lparmetis -lmetis -lcmumps -lsmumps
PETSC_BLAS_LAPACK_DIR = $(MKL_HOME)

PETSC_DIR = $(PROJECT_TOP)/libs/petsc
SLEPC_DIR = $(PROJECT_TOP)/libs/slepc
PETSC_REAL_BUILD = $(PROJECT_TOP)/libs/petsc/build-real
PETSC_CPLX_BUILD = $(PROJECT_TOP)/libs/petsc/build-cplx
SLEPC_REAL_BUILD = $(PROJECT_TOP)/libs/slepc/build-real
SLEPC_CPLX_BUILD = $(PROJECT_TOP)/libs/slepc/build-cplx

PETSC_REAL_INC = -I $(PETSC_REAL_BUILD)/include -I $(PETSC_DIR)/include/include -I $(PETSC_REAL_BUILD)/$(PETSC_REAL_ARCH)/include $(BOOST_INCLUDE) $(INCHDF) $(INCMPI) $(VALGRIND_INCLUDE)
PETSC_CPLX_INC = -I $(PETSC_CPLX_BUILD)/include -I $(PETSC_DIR)/include/include -I $(PETSC_CPLX_BUILD)/$(PETSC_CPLX_ARCH)/include $(BOOST_INCLUDE) $(INCHDF) $(INCMPI) $(VALGRIND_INCLUDE)
SLEPC_REAL_INC = -I $(SLEPC_REAL_BUILD)/include -I $(SLEPC_DIR)/include/include -I $(SLEPC_REAL_BUILD)/$(SLEPC_REAL_ARCH)/include -I $(SLEPC_REAL_BUILD)/include
SLEPC_CPLX_INC = -I $(SLEPC_CPLX_BUILD)/include -I $(SLEPC_DIR)/include/include -I $(SLEPC_CPLX_BUILD)/$(SLEPC_CPLX_ARCH)/include -I $(SLEPC_CPLX_BUILD)/include
PETSC_REAL_LIBDIR = $(PETSC_REAL_BUILD)/$(PETSC_REAL_ARCH)/lib
PETSC_CPLX_LIBDIR = $(PETSC_CPLX_BUILD)/$(PETSC_CPLX_ARCH)/lib
SLEPC_REAL_LIBDIR = $(SLEPC_REAL_BUILD)/$(SLEPC_REAL_ARCH)/lib
SLEPC_CPLX_LIBDIR = $(SLEPC_CPLX_BUILD)/$(SLEPC_CPLX_ARCH)/lib

LIBMESH_VERSION = 0.9.3
LIBMESH_DIR        = $(PROJECT_TOP)/libs/libmesh/libmesh

libmesh_INCLUDE = "-I $(HDF5_INCDIR)"
libmesh_CPPFLAGS = "-I $(HDF5_INCDIR) -I /pkg/local/gcc/4.8.3/include/4.8.3 -I /usr/include"
libmesh_CXXFLAGS = "-O3 -DMPICH_IGNORE_CXX_SEEK"

LIBMESH_ARCH       = x86_64-unknown-linux-gnu_opt
LIBMESH_TECIO_ARCH = x86_64-unknown-linux-gnu
LIBMESH_CONTRIBS   = -Wl,--start-group -ltbb -lGK -lmetis -lparmetis -lexodusii -lgmv -lgzstream -lnetcdf -lsfcurves -ltriangle -llaspack -lHilbert -Wl,--end-group

INCLIBMESH = -I $(HDF5_INCDIR) -I $(LIBMESH_DIR)/include/libmesh -I $(LIBMESH_DIR)/include -I $(LIBMESH_DIR)/include/numerics
LIBMESH_LIBS = -Wl,-rpath,$(LIBMESH_DIR)/.libs -L$(LIBMESH_DIR)/.libs -lmesh_opt -Wl,-rpath,$(LIBMESH_DIR)/contrib/.libs -L$(LIBMESH_DIR)/contrib/.libs -lcontrib_opt
LIBMESH_LIBS += -Wl,-rpath,$(SLEPC_REAL_LIBDIR) -L$(SLEPC_REAL_LIBDIR) -lslepc -Wl,-rpath,$(PETSC_REAL_LIBDIR) -L$(PETSC_REAL_LIBDIR) $(PETSC_LIBS) $(PETSC_EXT_LIBS_REAL)
LIBMESH_LIBS += $(LIBMESH_DIR)/contrib/tecplot/binary/lib/$(LIBMESH_TECIO_ARCH)/tecio.a

TAO_VERSION     = 2.2.0
TAO_FOLDER      = tao-$(TAO_VERSION)
TAO_FOLDER_PATH = $(PROJECT_TOP)/libs/TAO/tao-$(TAO_VERSION)
TAO_INC = -I $(PROJECT_TOP)/libs/TAO/tao-$(TAO_VERSION)/include
TAO_LIB = -Wl,-rpath,$(PROJECT_TOP)/libs/TAO/tao-$(TAO_VERSION)/$(PETSC_REAL_ARCH)/lib -L$(PROJECT_TOP)/libs/TAO/tao-$(TAO_VERSION)/$(PETSC_REAL_ARCH)/lib -ltao

#PYTHON SECTION
PYTHON_ENABLE   = true
PYTHON          =
#set by module load
PYTHONHOME = $(PROJECT_TOP)/libs/python
PYTHON_BIN = $(PYTHONHOME)/bin/python
PYTHON_INCLUDE = -I$(PYTHONHOME)/include/python2.7 -fPIC
PYTHON_LIB     = -Wl,-rpath,$(PYTHONHOME)/lib -L$(PYTHONHOME)/lib -lpython2.7 -lm -lpthread -ldl  -lutil -Xlinker -export-dynamic
```
