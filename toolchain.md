## 1.1.選定工具鏈
###開發工具
* make

 沒特殊限制。
* cmake

 編譯VTK需要cmake2.8.8以上。
* imake

 沒特殊限制。

###編譯器
* GCC

 4.8.3:系統預設值

 gcc -v
 ```
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=/usr/libexec/gcc/x86_64-redhat-linux/4.8.3/lto-wrapper
Target: x86_64-redhat-linux
Configured with: ../configure --prefix=/usr --mandir=/usr/share/man --infodir=/usr/share/info --with-bugurl=http://bugzilla.redhat.com/bugzilla --enable-bootstrap --enable-shared --enable-threads=posix --enable-checking=release --with-system-zlib --enable-__cxa_atexit --disable-libunwind-exceptions --enable-gnu-unique-object --enable-linker-build-id --with-linker-hash-style=gnu --enable-languages=c,c++,objc,obj-c++,java,fortran,ada,go,lto --enable-plugin --enable-initfini-array --disable-libgcj --with-isl=/builddir/build/BUILD/gcc-4.8.3-20140911/obj-x86_64-redhat-linux/isl-install --with-cloog=/builddir/build/BUILD/gcc-4.8.3-20140911/obj-x86_64-redhat-linux/cloog-install --enable-gnu-indirect-function --with-tune=generic --with-arch_32=x86-64 --build=x86_64-redhat-linux
Thread model: posix
gcc version 4.8.3 20140911 (Red Hat 4.8.3-9) (GCC)
 ```
 5.3.0: 使用前要先 ```module load compiler/gcc/5.3.0```

 gcc -v
```
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=/pkg/gcc/5.3.0/libexec/gcc/x86_64-redhat-linux/5.3.0/lto-wrapper
Target: x86_64-redhat-linux
Configured with: ../configure --prefix=/pkg/gcc/5.3.0 --mandir=/pkg/gcc/5.3.0/man --libdir=/pkg/gcc/5.3.0/lib64 --build=x86_64-redhat-linux --disable-multilib --enable-version-specific-runtime-libs=yes --enable-bootstrap --enable-shared --enable-threads=posix --enable-checking=release --with-system-zlib --enable-__cxa_atexit --disable-libunwind-exceptions --enable-gnu-unique-object --with-slibdir=/pkg/gcc/5.3.0/lib64 --with-mpc-include=/usr/include --with-mpc-lib=/usr/lib64 --with-mpfr-include=/usr/include --with-mpfr-lib=/usr/lib64 --with-gmp-include=/usr/include --with-gmp-lib=/usr/lib64 --enable-linker-build-id --with-linker-hash-style=gnu --enable-languages=c,c++,objc,obj-c++,fortran,ada,go,lto --enable-plugin --enable-initfini-array --disable-libgcj --with-isl-include=/pkg/gnu/include --with-isl-lib=/pkg/gnu/lib64 --with-cloog-include=/pkg/gnu/include --with-cloog-lib=/pkg/gnu/lib64 --enable-gnu-indirect-function --with-tune=amdfam10 --with-arch_32=x86-64
Thread model: posix
gcc version 5.3.0 (GCC)
```
註：選用GCC版本時要挑選支援C++11規範，否則無法成功編譯NEMO5主程式。

* INTEL

 2015:使用前要先 ```module load compiler/intel/2015```

 2013:使用前要先```module load compiler/intel/2013```

 12.1:使用前要先```module load compiler/intel/12.1```
 
 註1：LIBMESH很挑INTEL編譯器版本，如果要用intel V14版以後的，LIBMESH要用libmesh-0.9.3以後的。
 
 註2：主程式內會用到FEAST Eigenvalue Solver，MKL要11.0 Update 2才有這功能，所以如果要使用MKL的FEAST Eigenvalue Solver，編譯器最少要用2013以上的。

* PGI

 未測試。

###平行函式庫
* openmpi

 未測試。
* mpich

 未測試。
* mvapich2

 太多組合，不一一詳列，根據所選擇的編譯器工具決定要用哪一組。
* impi

 4.1.3.049:使用前要先```source /pkg/mpi/impi/4.1.3.049/intel64/bin/mpivars.sh```

 5.0.3.048:使用前要先```source /pkg/mpi/impi/5.0.3.048/intel64/bin/mpivars.sh```


###可用工具組
INTEL composer_xe_2015.2.164 + impi4.1.3.049(何博成功)

執行檔位於
/pkg/chem/nemo5-r17881/prototype/bin/nemo

gcc4.3.4/4.8.3+mvapich2-1.9(最後編譯主程式改用4.8.3)

執行檔位於
/pkg/biology/Nemo5/Nemo5_r17881/prototype/bin/nemo

gcc4.8.3+mpich3(在另外的centos6上成功)

###失敗的工具組
gcc4.8.3+mvapich2-1.9(VTK編譯失敗)

INTEL composer_xe_2015.2.164 + impi5.0.3.048

INTEL composer_xe_2013.5.192 + impi4.1.1.036都是在編譯主程式時出現以下錯誤
```
ModeSpace.cpp(2770): error: no instance of overloaded function "std::complex<double>::real" matches the argument list
            argument types are: (double)
            object type is: cplx
          Matrix_element.real(Real_part[i+j*Mat_num_rows]);
                         ^

ModeSpace.cpp(2771): error: no instance of overloaded function "std::complex<double>::imag" matches the argument list
            argument types are: (double)
            object type is: cplx
          Matrix_element.imag(Imag_part[i+j*Mat_num_rows]);
                         ^
```