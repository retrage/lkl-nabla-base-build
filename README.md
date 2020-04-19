# lkl-nabla-base-build

This repository provides building of LKL Nabla base Docker images.
Below base images available.

* hello-base
* nginx-base
* python3-base

## Building the Bases

Clone the repository and update submodules.

```console
$ git clone https://github.com/retrage/lkl-nabla-base-build.git
$ git submodule update --init
```

Since Solo5 expects its source code is either a release tarball
or a full git repository, `git submodule update solo5` will fail to build.
So clone the repository manually.

```console
$ cd frankenlibc
$ git clone https://github.com/Solo5/solo5.git
$ git submodule update --init --recursive
```

To build all the images, run:
```console
$ make world
```
or build one image by:
```console
$ make -C hello-base
```

## Pre-built Docker Images

The following pre-built docker images are available on Docker Hub.

* [retrage/lkl-nabla-hello-base](https://hub.docker.com/repository/docker/retrage/lkl-nabla-hello-base)
* [retrage/lkl-nabla-nginx-base](https://hub.docker.com/repository/docker/retrage/lkl-nabla-nginx-base)
* [retrage/lkl-nabla-python3-base](https://hub.docker.com/repository/docker/retrage/lkl-nabla-python3-base)
