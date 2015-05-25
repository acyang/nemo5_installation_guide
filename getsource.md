##1.2.取得原始碼

* 下載tarball

註冊nanohub後，下載tarball
https://nanohub.org/resources/21695/download/Nemo5_r17881.tgz

* svn checkout

針對緊密開發者可以從nanohub的repository取得最新開發版，帳號密碼與登入帳號相同

```
svn checkout https://nanohub.org/tools/nemo/svn/trunk/NEMO .
```

* 檔案結構

/ : NEMO5s root directory

prototype/: NEMO 5 source code


libs/: 3rd party libraries


manual/: user manual (compile using latex ../bin/nemo --manual)


doc/: doxygen documentation (developer manual)
include/: .h-files, needed e.g. for using NEMO 5 as a library
src/: .cpp-files
bin/: location of nemo executable



