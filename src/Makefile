CONFIG_FB_UVESA = y

ifneq ($(KERNELRELEASE),)
        obj-m := uvesafb.o
        EXTRA_CFLAGS += -DCONFIG_FB_UVESA
else
        BASEDIR := /lib/modules/$(shell uname -r)
        KERNELDIR ?= $(BASEDIR)/build
        PWD :=$(shell pwd)
        DRIVERDIR := $(BASEDIR)/kernel/drivers/video/fbdev
        FBDEVDIR := $(subst $(BASEDIR)/,,$(DRIVERDIR))

.PHONY: all
all: clean modules install

.PHONY:modules
modules:
        $(MAKE) -C $(KERNELDIR) SUBDIRS=$(PWD) modules

.PHONY:clean
clean:
        $(MAKE) -C $(KERNELDIR) SUBDIRS=$(PWD) clean

.PHONY:install
install:
        $(MAKE) -C $(KERNELDIR) SUBDIRS=$(PWD) INSTALL_MOD_DIR=$(FBDEVDIR) modules_install

endif
