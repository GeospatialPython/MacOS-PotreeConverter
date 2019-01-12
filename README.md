# MacOS-PotreeConverter

MacOS binary for [PotreeConverter](https://github.com/potree/PotreeConverter) which can be tricky to compile.

It was compiled on MacOS Mojave 10.14.2 (18C54) using gcc gcc8 8.2.0_3 installed via MacPorts.

You will also need to copy the resources directory from the original repository which must be in the same directory as the executable.

You may also run into this error which is easy to fix:
https://github.com/potree/PotreeConverter/issues/281

The following steps were used to compile.

```
sudo port install gcc8
sudo port select --set gcc mp-gcc8
cd ~/Downloads
mkdir lastools
cd lastools
git clone https://github.com/m-schuetz/LAStools.git master
cd master/LASzip
mkdir build
cd build
/opt/local/bin/cmake -DCMAKE_BUILD_TYPE=Release ..
make

cd ~/Downloads
mkdir PotreeConverter
cd PotreeConverter
git clone https://github.com/potree/PotreeConverter.git master
cd master
mkdir build
cd build
/opt/local/bin/cmake -DCMAKE_BUILD_TYPE=Release -DLASZIP_INCLUDE_DIRS=/Users/<username>/Downloads/lastools/master/LASzip/dll/ -DLASZIP_LIBRARY=/Users/<username>/Downloads/lastools/master/LASzip/build/src/liblaszip.dylib -DCMAKE_C_COMPILER=/opt/local/bin/gcc -DCMAKE_CXX_COMPILER=/opt/local/bin/g++ ..
make
```

