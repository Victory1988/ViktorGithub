#******************************************************************************
# Copyright (C) 2017 by Alex Fosdick - University of Colorado
#
# Redistribution, modification or use of this software in source or binary
# forms is permitted as long as the files maintain this copyright. Users are 
# permitted to modify this and use it to learn about the field of embedded
# software. Alex Fosdick and the University of Colorado are not liable for any
# misuse of this material. 
#
#*****************************************************************************

#------------------------------------------------------------------------------
# Simple makefile for multitarget build system
#
# Use: make [TARGET] [PLATFORM-OVERRIDES]
#
# Build Targets:
#      <FILE>.o - Builds <FILE>.o object file
#	   build - Builds and links all source files
#	   all - Same as build
#	   clean - Removes all generated files		
#	
# Platform Overrides:
#      CPU - ARM Cortex Architecture (cotex-m0plus, cortex-m4
#	   ARCH - ARM Architecture (arm, thumb)
#	   SPECS - Specs file to give the linker (nosys.specs, nano.specs)
#
#------------------------------------------------------------------------------
include sources.mk

# Platform Overrides

#PLATFORM = MSP432


# Architectures Specific Flags
LINKER_FILE = msp432p401r.lds	# Pfad?
CPU = cortex-m4
ARCH = thumb
SPECS = nosys.specs

# Compiler Flags and Defines
	#MSP	
ifeq	($(PLATFORM),MSP432)
	CC = arm-none-eabi-gcc
	LD = arm-none-eabi-ld
	BASENAME = demo_vik
	LDFLAGS = -Wl, -Map=$(BASENAME).map -T $(LINKER_FILE)
	CFLAGS = -mcpu=$(CPU) -m$(ARCH) --specs=$(SPECS) -Wall
	CPPFLAGS = -DMSP432
	endif
ifeq	($(PLATFORM),HOST)	
#	CC = -gcc
endif


OBJS = $(SOURCES:.c=.o)

%.o : %.c
	$(CC) $(CPPFLAGS) -c $< $(CFLAGS) -o $@

.PHONY: build
build: all

.PHONY: all
all: $(BASENAME).out

$(BASENAME).out: $(OBJS)
	$(CC) $(OBJS) $(CFLAGS) $(CPPFLAGS) $(LDFLAGS) -o $@

.PHONY: clean
clean:
	rm -f $(OBJS) $(BASENAME).out $(BASENAME).map
