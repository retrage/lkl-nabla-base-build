# lkl-nabla-base-build

This repository provides building of LKL Nabla base Docker images.

## Building the bases

Clone the repository and update submodules.

```console
$ git clone https://github.com/retrage/lkl-nabla-base-build.git
$ git submodule update --init
```

Since Solo5 expects its source code is either a release tarball
or a full git repository, `git submodule update solo5` will fail to build.
So clone the repositoty manually.

```console
$ cd frankenlibc
$ git clone https://github.com/Solo5/solo5.git
$ git submodule update --init --recursive
```

Run
```console
$ make world
```
or
```console
$ make hello-base
```
