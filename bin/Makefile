###############################################################################
# Makefile for the project main
###############################################################################

## General Flags
PROJECT = main
MCU = atmega128
TARGET = main.elf
CC = avr-gcc

CPP = avr-g++

## Options common to compile, link and assembly rules
COMMON = -mmcu=$(MCU)

## Compile options common for all C compilation units.
CFLAGS = $(COMMON)
CFLAGS += -Wall -gdwarf-2 -std=gnu99                           -DF_CPU=16000000UL -Os -funsigned-char -funsigned-bitfields -fpack-struct -fshort-enums
CFLAGS += -MD -MP -MT $(*F).o -MF dep/$(@F).d 

## Assembly specific flags
ASMFLAGS = $(COMMON)
ASMFLAGS += $(CFLAGS)
ASMFLAGS += -x assembler-with-cpp -Wa,-gdwarf2

## Linker flags
LDFLAGS = $(COMMON)
LDFLAGS +=  -Wl,-Map=main.map


## Intel Hex file production flags
HEX_FLASH_FLAGS = -R .eeprom -R .fuse -R .lock -R .signature

HEX_EEPROM_FLAGS = -j .eeprom
HEX_EEPROM_FLAGS += --set-section-flags=.eeprom="alloc,load"
HEX_EEPROM_FLAGS += --change-section-lma .eeprom=0 --no-change-warnings


## Include Directories
INCLUDES = -I"D:\Developments\Elektronika\MCU\ATMEL\AVR\AVR-IO-MODULE\v.0.0.9\B21.08.2017\github\RS485-Channel\arch" -I"D:\Developments\Elektronika\MCU\ATMEL\AVR\AVR-IO-MODULE\v.0.0.9\B21.08.2017\github\RS485-Channel\modbus" -I"D:\Developments\Elektronika\MCU\ATMEL\AVR\AVR-IO-MODULE\v.0.0.9\B21.08.2017\github\RS485-Channel\modbus\rtu" -I"D:\Developments\Elektronika\MCU\ATMEL\AVR\AVR-IO-MODULE\v.0.0.9\B21.08.2017\github\RS485-Channel\modbus\tcp" -I"D:\Developments\Elektronika\MCU\ATMEL\AVR\AVR-IO-MODULE\v.0.0.9\B21.08.2017\github\RS485-Channel\rs485Device" -I"D:\Developments\Elektronika\MCU\ATMEL\AVR\AVR-IO-MODULE\v.0.0.9\B21.08.2017\github\RS485-Channel\modbus\port" -I"D:\Developments\Elektronika\MCU\ATMEL\AVR\AVR-IO-MODULE\v.0.0.9\B21.08.2017\github\RS485-Channel\modbus\ascii" -I"D:\Developments\Elektronika\MCU\ATMEL\AVR\AVR-IO-MODULE\v.0.0.9\B21.08.2017\github\RS485-Channel\modbus\include" -I"D:\Developments\Elektronika\MCU\ATMEL\AVR\AVR-IO-MODULE\v.0.0.9\B21.08.2017\github\RS485-Channel\modbus\functions" -I"D:\Developments\Elektronika\MCU\ATMEL\AVR\AVR-IO-MODULE\v.0.0.9\B21.08.2017\github\RS485-Channel\digital_in_out_func" -I"D:\Developments\Elektronika\MCU\ATMEL\AVR\AVR-IO-MODULE\v.0.0.9\B21.08.2017\github\RS485-Channel\modbus_master" 

## Objects that must be built in order to link
OBJECTS = main.o mbrtu.o mbascii.o mbfunccoils.o mbfuncdiag.o mbfuncdisc.o mbfuncholding.o mbfuncinput.o mbfuncother.o mbutils.o mbcrc.o portevent.o portserial.o porttimer.o mb.o mbtcp.o digital_in_out_func.o spi.o modbus-rtu.o rs485Channel.o 

## Objects explicitly added by the user
LINKONLYOBJECTS = 

## Build
all: $(TARGET) main.hex main.eep main.lss size

## Compile
main.o: ../main.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

mbrtu.o: ../modbus/rtu/mbrtu.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

mbascii.o: ../modbus/ascii/mbascii.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

mbfunccoils.o: ../modbus/functions/mbfunccoils.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

mbfuncdiag.o: ../modbus/functions/mbfuncdiag.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

mbfuncdisc.o: ../modbus/functions/mbfuncdisc.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

mbfuncholding.o: ../modbus/functions/mbfuncholding.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

mbfuncinput.o: ../modbus/functions/mbfuncinput.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

mbfuncother.o: ../modbus/functions/mbfuncother.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

mbutils.o: ../modbus/functions/mbutils.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

mbcrc.o: ../modbus/port/mbcrc.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

portevent.o: ../modbus/port/portevent.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

portserial.o: ../modbus/port/portserial.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

porttimer.o: ../modbus/port/porttimer.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

mb.o: ../modbus/mb.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

mbtcp.o: ../modbus/tcp/mbtcp.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

digital_in_out_func.o: ../digital_in_out_func/digital_in_out_func.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

spi.o: ../arch/spi.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

modbus-rtu.o: ../modbus_master/modbus-rtu.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

rs485Channel.o: ../rs485Channel/rs485Channel.c
	$(CC) $(INCLUDES) $(CFLAGS) -c  $<

##Link
$(TARGET): $(OBJECTS)
	 $(CC) $(LDFLAGS) $(OBJECTS) $(LINKONLYOBJECTS) $(LIBDIRS) $(LIBS) -o $(TARGET)

%.hex: $(TARGET)
	avr-objcopy -O ihex $(HEX_FLASH_FLAGS)  $< $@

%.eep: $(TARGET)
	-avr-objcopy $(HEX_EEPROM_FLAGS) -O ihex $< $@ || exit 0

%.lss: $(TARGET)
	avr-objdump -h -S $< > $@

size: ${TARGET}
	@echo
	@avr-size -C --mcu=${MCU} ${TARGET}

## Clean target
.PHONY: clean
clean:
	-rm -rf $(OBJECTS) main.elf dep/* main.hex main.eep main.lss main.map


## Other dependencies
-include $(shell mkdir dep 2>/dev/null) $(wildcard dep/*)

