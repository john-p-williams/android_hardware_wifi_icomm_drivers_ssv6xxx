TARGET ?= ssv6051-sw

OBJS := \
	apps/app_main.o \
	apps/mac80211/cmd_engine.o \
	apps/mac80211/soft-main.o \
	apps/msgevt.o \
	apps/pbuf.o \
	apps/soc_global.o \
	apps/soc_log.o \
	bsp/boot.o \
	bsp/bsp.o \
	bsp/cpu.o \
	bsp/irq.o \
	bsp/serial.o \
	cli/cli.o \
	cli/cmds/cli_cmd.o \
	cli/cmds/mac_monitor.o \
	driver/ampdu/drv_ampdu.o \
	driver/dbg_timer/dbg_timer.o \
	driver/hwmac/drv_mac.o \
	driver/hw_regs_api.o \
	driver/idmanage/drv_idmanage.o \
	driver/mbox/drv_mbox.o \
	driver/p2p/drv_p2p.o \
	driver/phy/drv_phy.o \
	driver/pmu/drv_pmu.o \
	driver/rate-control/drv_rc.o \
	driver/rtc/drv_rtc.o \
	driver/timer/drv_timer.o \
	driver/uart/drv_uart.o \
	driver/watchdog/sw_watchdog.o \
	lib/lib-impl.o \
	lib/ssv_lib.o \
	rtos/FreeRTOS/rtos_glue.o \
	rtos/FreeRTOS/Source/croutine.o \
	rtos/FreeRTOS/Source/list.o \
	rtos/FreeRTOS/Source/portable/GCC/SSV6200/portISR.o \
	rtos/FreeRTOS/Source/portable/GCC/SSV6200/port.o \
	rtos/FreeRTOS/Source/portable/MemMang/heap_3.o \
	rtos/FreeRTOS/Source/queue.o \
	rtos/FreeRTOS/Source/tasks.o \
	rtos/FreeRTOS/Source/timers.o \
	rtos/rtos.o

CC = arm-none-eabi-gcc
LD = arm-none-eabi-gcc
OBJCOPY = arm-none-eabi-objcopy
OBJDUMP = arm-none-eabi-objdump
NM = arm-none-eabi-nm

CPPFLAGS := -D__SSV6200__
CPPFLAGS += -I.
CPPFLAGS += -Iinclude
CPPFLAGS += -I../../include
CPPFLAGS += -Idriver
CPPFLAGS += -Irtos/FreeRTOS/Source/include
CPPFLAGS += -Icli

CFLAGS := -Os
CFLAGS += -fno-builtin
CFLAGS += -fomit-frame-pointer
CFLAGS += -mcpu=arm7
CFLAGS += -mno-thumb-interwork
CFLAGS += -Wall
CFLAGS += -Wno-trigraphs

LDFLAGS := -Bstatic
LDFLAGS += -nostartfiles
LDFLAGS += -Tbsp/ldscript.ld

all: $(TARGET).bin

$(TARGET): $(OBJS)
	$(LD) $(LDFLAGS) -o $(TARGET) $(OBJS)

$(TARGET).bin: $(TARGET)
	$(OBJCOPY) -O binary $(TARGET) $(TARGET).bin

$(TARGET).lss: $(TARGET)
	$(OBJDUMP) -ChrS $(TARGET) > $(TARGET).lss

$(TARGET).sym: $(TARGET)
	$(NM) -CnS $(TARGET) > $(TARGET).sym

clean:
	rm -f $(OBJS) $(TARGET) $(TARGET).bin $(TARGET).lss $(TARGET).sym
