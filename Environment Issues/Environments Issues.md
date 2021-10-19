```
./opt/cachelib/bin/cachebench: symbol lookup error: ./opt/cachelib/bin/cachebench: undefined symbol: _ZN6google21kLogSiteUninitializedE
/usr/bin/ld: CMakeFiles/BogoShim.dir/test/BogoShim.cpp.o: undefined reference to symbol '_ZN6google11InitVLOG3__EPPiS0_PKci'
```

CacheLib link library wrong: _ZN6google21kLogSiteUninitializedE, related to glog, change the version of glog





```
[ 94%] Linking CXX shared library libfolly.so
/usr/bin/ld: /usr/local/lib/libfmt.a(format.cc.o): relocation R_X86_64_PC32 against symbol `stderr@@GLIBC_2.2.5' can not be used when making a shared object; recompile with -fPIC
/usr/bin/ld: final link failed: Bad value
```

It wants to link a static lib to a shared lib.

Build libfmt as the shared lib (libfmt.so) rather than (libfmt.a) solves the problem.

Using command `cmake -DBUILD_SHARED_LIBS=ON ...`

