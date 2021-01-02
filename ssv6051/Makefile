LINUX ?= /lib/modules/$(shell uname -r)/build

EXTRA_CFLAGS := -I$(PWD) -I$(PWD)/include

include $(PWD)/ssv6051.cfg

obj-m := ssv6051.o

ssv6051-y := \
	hci/ssv_hci.o \
	hwif/sdio/sdio.o \
	smac/ampdu.o \
	smac/ap.o \
	smac/dev.o \
	smac/efuse.o \
	smac/init.o \
	smac/sar.o \
	smac/ssv6xxx_debugfs.o \
	smac/ssv_ht_rc.o \
	smac/ssv_pm.o \
	smac/ssv_rc.o \
	ssv6051-generic-wlan.o \
	ssvdevice/ssv_cmd.o \
	ssvdevice/ssvdevice.o

all:
	make -C $(LINUX) CONFIG_STACKPROTECTOR=n CONFIG_STACKPROTECTOR_STRONG=n M=$(PWD) modules

install:
	make -C $(LINUX) M=$(PWD) modules_install

clean:
	make -C $(LINUX) M=$(PWD) clean
