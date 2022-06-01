#
# Makefile for the IPVS TOA  modules on top of IPv4.
#

KERNEL ?= $(shell uname -r)
KSRC ?=/lib/modules/$(shell uname -r)/build
PWD ?=$(CURDIR)
mkfile_path := $(abspath $(lastword $(MAKEFILE_LIST)))
CURRENT_DIR := $(notdir $(patsubst %/,%,$(dir $(mkfile_path))))
obj-$(CONFIG_TOA) += toa.o

default:
	make CONFIG_TOA=m  -C $(KSRC) M=$(CURDIR) modules

debug:
	make CONFIG_TOA=m  -C $(KSRC) M=$(CURDIR) modules EXTRA_CFLAGS="-DTOA_DBG_MSG"
clean:
	rm -f .*.cmd *.o *.ko *.mod.c modules.order Module.symvers
	rm -rf .tmp_versions
install:
	test -d "$(DESTDIR)//lib/modules/$(KERNEL)/extra/net/toa" \
		|| mkdir -p "$(DESTDIR)/lib/modules/$(KERNEL)/extra/net/toa"
	cp *.ko  "$(DESTDIR)/lib/modules/$(KERNEL)/extra/net/toa"
