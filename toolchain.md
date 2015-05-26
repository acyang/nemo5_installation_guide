## 1.1.選定工具鏈
###開發工具
* make

 沒特殊限制。
* cmake

 沒特殊限制。
* imake

 沒特殊限制。

###編譯器
* GCC

 4.3.4:系統預設值

 cpp -v
 ```
Using built-in specs.
Target: x86_64-suse-linux
Configured with: ../configure --prefix=/usr --infodir=/usr/share/info --mandir=/usr/share/man --libdir=/usr/lib64 --libexecdir=/usr/lib64 --enable-languages=c,c++,objc,fortran,obj-c++,java,ada --enable-checking=release --with-gxx-include-dir=/usr/include/c++/4.3 --enable-ssp --disable-libssp --with-bugurl=http://bugs.opensuse.org/ --with-pkgversion='SUSE Linux' --disable-libgcj --disable-libmudflap --with-slibdir=/lib64 --with-system-zlib --enable-__cxa_atexit --enable-libstdcxx-allocator=new --disable-libstdcxx-pch --enable-version-specific-runtime-libs --program-suffix=-4.3 --enable-linux-futex --without-system-libunwind --with-cpu=generic --build=x86_64-suse-linux
Thread model: posix
gcc version 4.3.4 [gcc-4_3-branch revision 152973] (SUSE Linux)
COLLECT_GCC_OPTIONS='-E' '-v' '-mtune=generic'
 /usr/lib64/gcc/x86_64-suse-linux/4.3/cc1 -E -quiet -v - -mtune=generic
#include "..." search starts here:
#include <...> search starts here:
 /usr/local/include
 /usr/lib64/gcc/x86_64-suse-linux/4.3/include
 /usr/lib64/gcc/x86_64-suse-linux/4.3/include-fixed
 /usr/lib64/gcc/x86_64-suse-linux/4.3/../../../../x86_64-suse-linux/include
 /usr/include
End of search list.
 ```
 4.6.1: 使用前要先 ```source /pkg/local/gcc/4.6.1/gcc461.sh```

 cpp -v
```
Using built-in specs.
COLLECT_GCC=cpp
COLLECT_LTO_WRAPPER=/pkg/local/gcc/4.6.1/libexec/gcc/x86_64-unknown-linux-gnu/4.6.1/lto-wrapper
Target: x86_64-unknown-linux-gnu
Configured with: ../configure --prefix=/pkg/local/gcc/4.6.1
Thread model: posix
gcc version 4.6.1 (GCC)
COLLECT_GCC_OPTIONS='-E' '-v' '-mtune=generic' '-march=x86-64'
 /pkg/local/gcc/4.6.1/libexec/gcc/x86_64-unknown-linux-gnu/4.6.1/cc1 -E -quiet -v - -mtune=generic -march=x86-64
ignoring nonexistent directory "/pkg/local/gcc/4.6.1/lib/gcc/x86_64-unknown-linux-gnu/4.6.1/../../../../x86_64-unknown-linux-gnu/include"
#include "..." search starts here:
#include <...> search starts here:
 /pkg/local/gcc/4.6.1/lib/gcc/x86_64-unknown-linux-gnu/4.6.1/include
 /usr/local/include
 /pkg/local/gcc/4.6.1/include
 /pkg/local/gcc/4.6.1/lib/gcc/x86_64-unknown-linux-gnu/4.6.1/include-fixed
 /usr/include
End of search list.
```
 4.8.3: 使用前要先 ```source /pkg/local/gcc/4.8.3/gcc483.sh```

 cpp -v
 ```
 Using built-in specs.
COLLECT_GCC=cpp
Target: x86_64-suse-linux
Configured with: ../configure --prefix=/pkg/local/gcc/4.8.3 --with-cpu-64=amdfam10 --with-arch-64=amdfam10 --with-tune-64=amdfam10 --enable-languages=c,c++,objc,fortran,obj-c++,java,ada --enable-checking=release --enable-ssp --disable-libgcj --with-slibdir=/pkg/local/gcc/4.8.3/lib64 --with-pkgversion='SUSE Linux' --with-system-zlib --enable-__cxa_atexit --enable-version-specific-runtime-libs --enable-linux-futex --without-system-libunwind --build=x86_64-suse-linux --disable-multilib --enable-werror --with-gmp=/pkg/gnu --with-mpfr=/pkg/gnu --with-mpc=/pkg/gnu
Thread model: posix
gcc version 4.8.3 (SUSE Linux)
COLLECT_GCC_OPTIONS='-E' '-v' '-mtune=amdfam10' '-march=amdfam10'
 /pkg/local/gcc/4.8.3/libexec/gcc/x86_64-suse-linux/4.8.3/cc1 -E -quiet -v - -mtune=amdfam10 -march=amdfam10
ignoring nonexistent directory "/pkg/local/gcc/4.8.3/lib/gcc/x86_64-suse-linux/4.8.3/../../../../x86_64-suse-linux/include"
#include "..." search starts here:
#include <...> search starts here:
 /pkg/local/gcc/4.8.3/lib/gcc/x86_64-suse-linux/4.8.3/include
 /usr/local/include
 /pkg/local/gcc/4.8.3/include
 /pkg/local/gcc/4.8.3/lib/gcc/x86_64-suse-linux/4.8.3/include-fixed
 /usr/include
End of search list.
 ```
註1：4.3.4版本太舊不支援C++11規範，無法編譯NEMO5主程式。
註2：ALPS上的4.8.3無法成功編譯VTK5.10.0，但在另外一台CENTOS的原生4.8.3卻可以編譯成功。
* INTEL

 2015:使用前要先 ```source /pkg/intel/2015/composer_xe_2015.2.164/bin/compilervars.sh intel64```

 2013:使用前要先```source /pkg/intel/2013/composer_xe_2013.5.192/bin/compilervars.sh intel64```

 12:使用前要先```source /pkg/intel/12/composer_xe_2011_sp1.9.293/bin/compilervars.sh intel64```

 11.1:未測試。

 10:未測試。

 註1：LIBMESH很挑INTEL編譯器版本，例如intel V14版的要到libmesh0.9.3才支援。
 
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

