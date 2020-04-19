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

.PHONY: rumprun-packages-nginx
rumprun-packages-nginx: rumprun FORCE
	echo RUMPRUN_TOOLCHAIN_TUPLE=x86_64-rumprun-linux > $(RUMPPKGS)/config.mk
	export PATH=$(RUMPRUN)/rump/bin:$(PATH) && \
	$(MAKE) -C $(RUMPPKGS)/nginx
	cp -rpf $(RUMPPKGS)/nginx/images/data data
	cp -pf $(RUMPPKGS)/nginx/build/objs/nginx nginx.nabla

rumprun-packages-nginx-clean:
	$(MAKE) -C $(RUMPPKGS)/nginx clean

build_docker: submodule_warning $(FILES) rumprun-packages-nginx
	docker build -f Dockerfile -t retrage/lkl-nabla-nginx-base .

clean:
	rm -rf data nginx.nabla

distclean: clean rumprun-packages-nginx-clean rumprun-clean
