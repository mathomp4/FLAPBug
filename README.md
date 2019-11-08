# FLAP Bug Reproducer

This is a simple reproducer for FLAP Cmake issue.

First build FLAP:
```
git clone --recursive git@github.com:mathomp4/FLAP.git
cd FLAP
mkdir build
cd build
cmake .. -DCMAKE_INSTALL_PREFIX=../install -DCMAKE_BUILD_TYPE=Release
make install
```
Now you should have FLAP. Next, to emulate how Baselibs works, *remove*
the FLAP `build` directory:
```
cd ..
rm -rf build
```

Next build this repository:
```
git clone git@github.com:mathomp4/FLAPBug.git
cd FLAPBug
mkdir build
cd build
cmake .. -DCMAKE_INSTALL_PREFIX=../install -DCMAKE_BUILD_TYPE=Release -DCMAKE_PREFIX_PATH=<path to install directory from above>
make
```

When you do this, you'll get an error:
```
$ make
Scanning dependencies of target mylib
[ 25%] Building Fortran object src/lib/CMakeFiles/mylib.dir/my_args.F90.o
[ 50%] Linking Fortran static library libmylib.a
[ 50%] Built target mylib
Scanning dependencies of target main.exe
[ 75%] Building Fortran object src/lib/CMakeFiles/main.exe.dir/main.F90.o
make[2]: *** No rule to make target `../FLAP/build/src/lib/libFLAP.a', needed by `src/lib/main.exe'.  Stop.
make[1]: *** [src/lib/CMakeFiles/main.exe.dir/all] Error 2
make: *** [all] Error 2
```

