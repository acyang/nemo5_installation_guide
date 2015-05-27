# 6.總結
在ALPS上安裝的工具組太多太複雜，ALPI1~5與ALPS登入及計算節點環境也不完全一致，也增加了編譯和執行的困難。以下整理出使用過的工具組合。讀者在自己的機器上編譯時請依實際情況適當修正。

###可成功編譯之工具組
INTEL composer_xe_2015.2.164 + impi4.1.3.049(何博)

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