open.mp Linux build image (Debian 11)
======================================

The server built here runs on Debian 11 (glibc 2.31) and newer.

How to use:

1. `docker build -t open.mp/build:debian-11 .`
1. `docker run --rm -ti -v /path/to/omp/sources:/omp -w /omp open.mp/build:debian-11`
1. Built open.mp is available in /path/to/omp/sources/build
1. Note: You can use `-e CONFIG=Debug` or `-e CONFIG=RelWithDebInfo` in the `docker run` call to change the build type

Or run `DEBIAN_VERSION=11 ./build.sh` from the `docker` folder.
