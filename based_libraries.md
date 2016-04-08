# 2.編譯底層函式庫
* vtk

 進去$(LIB_TOP)/vtk，修改Makefile內關於parallel make的設定，可以把17改大一點。

```
include ../make.inc

VTK_VERSION = 5.10.0
INSTALL_DIR = $(PWD)

all: static shared

static: VTK/CMakeLists.txt
	(cd VTK/; export CC="$(MPICC)"; export CXX="$(MPICXX)"; \
	 cmake -DBUILD_EXAMPLES=OFF -DBUILD_SHARED_LIBS=OFF -DBUILD_TESTING=OFF -DCMAKE_INSTALL_PREFIX=$(PWD) .; \
	 make -j 24; make install)

shared: VTK/CMakeLists.txt
	(cd VTK/; export CC="$(MPICC)"; export CXX="$(MPICXX)"; \
	 cmake -DBUILD_EXAMPLES=OFF -DBUILD_SHARED_LIBS=ON -DBUILD_TESTING=OFF -DCMAKE_INSTALL_PREFIX=$(PWD) .; \
	 make -j 24; make install)

VTK/CMakeLists.txt:
	tar zxvf vtk-$(VTK_VERSION).tar.gz
	chmod -R a+w VTK/;
```
修改後存檔，再make。

註：5.10.1是5系列最終般本，不要用到更新的。

```wget http://www.vtk.org/files/release/5.10/vtk-5.10.1.tar.gz```

~~註2：libs/vtk/VTK/CMake/vtkDetermineCompilerFlags.cmake裡刪除-i_dynamic選項，新版編譯器已不支援。~~

~~IF(_MAY_BE_INTEL_COMPILER)
  INCLUDE(${VTK_CMAKE_DIR}/TestNO_ICC_IDYNAMIC_NEEDED.cmake)
  TESTNO_ICC_IDYNAMIC_NEEDED(NO_ICC_IDYNAMIC_NEEDED ${VTK_CMAKE_DIR})
  IF(NO_ICC_IDYNAMIC_NEEDED)
    SET(VTK_REQUIRED_CXX_FLAGS "${VTK_REQUIRED_CXX_FLAGS}")
  ELSE(NO_ICC_IDYNAMIC_NEEDED)
    SET(VTK_REQUIRED_CXX_FLAGS "${VTK_REQUIRED_CXX_FLAGS}")
  ENDIF(NO_ICC_IDYNAMIC_NEEDED)
ENDIF(_MAY_BE_INTEL_COMPILER)~~

* python

修改configure部分以及取消patch，原檔案只有COPY執行檔和函式庫到資料夾，所以再用正規作法加上make install安裝比較不會有問題。
為了要與BOOST連動所以configure參數要加上--enable-unicode=ucs4 --enable-shared

```
include ../../make.inc
PYTHON_VERSION   = Python-2.7.3
PYTHON_PREFIX    = $(PWD)
all: $(PYTHON_VERSION)/python



$(PYTHON_VERSION)/configure:
	 tar zxvf $(PYTHON_VERSION).tgz

build:
	 mkdir -p build


$(PYTHON_VERSION)/Makefile:$(PYTHON_VERSION)/configure
	(cd $(PYTHON_VERSION); \
	 ./configure --prefix="$(PYTHON_PREFIX)" --enable-unicode=ucs4 --enable-shared --without-gcc --with-valgrind --with-wctype-functions --with-ensurepip --with-libs=-lz CC=$(CC) CXX=$(CXX); )

$(PYTHON_VERSION)/python: build $(PYTHON_VERSION)/Makefile
	@echo "##################################################################"
	@echo "#                   Building Static Python                       #"
	@echo "##################################################################"
	(cd $(PYTHON_VERSION); \
	 #cp -r ../jaguar_patch/* .; \
	 make; make install; \
	 cp -r libpython2.7.a libpython2.7.so libpython2.7.so.1.0 Lib Include python ../build/; \
   	 cp pyconfig.h ../build/Include; \
	)

clean:
	rm -rf build/ $(PYTHON_VERSION)/
```


之後利用到python的指令都要加上

```
LD_LIBRARY_PATH=/pkg/biology/Nemo5/Nemo5_intel/libs/python/lib:$LD_LIBRARY_PATH
```

註1：有2.7.11可以嘗試，不要用到3版的。

```wget https://www.python.org/ftp/python/2.7.11/Python-2.7.11.tgz```

註2：NEMO5不支援statically link to python，所以不編static library也可以。

註3：ALPS作業系統升級後，安裝在/pkg/free/Python-2.7.11的python，有支援ucs4，以及編譯成動態函式庫，可以直接拿來使用，使用前請先module load tools/Python-2.7.11。

* boost

因為要讓自編的python和boost連動必須修改project-config.jam檔，而project-config.jam又是由bootstrap.sh所產生，所以直接為該檔案打上patch。
Makefile

```
include ../make.inc

BOOST_VERSION = 1_51_0
INSTALL_DIR = $(PWD)

all: boost_dist

boost_dist:
	tar zxvf boost_$(BOOST_VERSION).tar.gz
	(cd boost_$(BOOST_VERSION); patch -p0 < ../bootstrap.sh_1_51_0.patch; ./bootstrap.sh --prefix=$(INSTALL_DIR) --with-python-root=../../python --with-python-version=2.7 --with-toolset=intel-linux; ./bjam install -j 16 toolset=intel -a)
```

bootstrap.sh_1_51_0.patch

```
--- bootstrap.sh	2012-07-28 02:15:55.000000000 +0800
+++ bootstrap.sh.new	2015-05-06 16:58:16.000000000 +0800
@@ -345,7 +345,12 @@
   cat >> project-config.jam <<EOF

 # Python configuration
-using python : $PYTHON_VERSION : $PYTHON_ROOT ;
+using python : $PYTHON_VERSION
+             : $PYTHON_ROOT/bin/python
+             : $PYTHON_ROOT/include/python2.7
+             : $PYTHON_ROOT/lib/python2.7
+             : <toolset>$TOOLSET
+             ;
 EOF
 fi
```
註1：安裝完訊息應該是...updated 10698 targets...而不是...failed updating 56 targets...。

註2：有1_60_0可以嘗試。patch檔可以直接沿用。

註3：

* hdf5

由於新版intel編譯器把libirc改成libintlc所以要在LDFLAGS加上-lintlc
LDFLAGS       = -Wl,-rpath=$(INTEL_HOME)/lib/intel64 -L$(INTEL_HOME)/lib/intel64 -lintlc
```
cd petsc
tar -zxv -f hdf5-1.8.10-patch1.tar.gz
cd hdf5-1.8.10-patch1
./configure --prefix=/pkg/biology/Nemo5/Nemo5_intel/libs/hdf5/hdf5-1.8.10-patch1 --enable-fortran --enable-fortran2003 --enable-cxx CC=icc CXX=icpc FC=ifort FC2003=ifort
make
make install
```


