# SPDX-License-Identifier: ISC
# Copyright (c) 2020 Contributors as noted in the AUTHORS file
#
# Permission to use, copy, modify, and/or distribute this software
# for any purpose with or without fee is hereby granted, provided
# that the above copyright notice and this permission notice appear
# in all copies.
#
# THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL
# WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED
# WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE
# AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR
# CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS
# OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT,
# NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN
# CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

export TOP=$(abspath ..)
all: build_docker

RUMPPKGS=$(TOP)/rumprun-packages
RUMPRUN=$(TOP)/frankenlibc
include ../Makefile.inc

FILES= \
	   Dockerfile \
	   Makefile \

.PHONY: rumprun-packages-redis
rumprun-packages-redis: rumprun FORCE
	echo RUMPRUN_TOOLCHAIN_TUPLE=x86_64-rumprun-linux > $(RUMPPKGS)/config.mk
	export PATH=$(RUMPRUN)/rump/bin:$(PATH) && \
	$(MAKE) -C $(RUMPPKGS)/redis cache
	cp -rpf $(RUMPPKGS)/redis/images/data data
	cp -pf $(RUMPPKGS)/redis/bin/redis-server redis.nabla

rumprun-packages-redis-clean:
	$(MAKE) -C $(RUMPPKGS)/redis clean

build_docker: submodule_warning $(FILES) rumprun-packages-redis
	docker build -f Dockerfile -t retrage/lkl-nabla-redis-base .

clean:
	rm -rf data redis.nabla

distclean: clean rumprun-packages-redis-clean rumprun-clean
