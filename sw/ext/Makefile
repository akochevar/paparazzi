# Hey Emacs, this is a -*- makefile -*-
#
#   Paparazzi main $Id$
#   Copyright (C) 2004 Pascal Brisset Antoine Drouin
#
# This file is part of paparazzi.
#
# paparazzi is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2, or (at your option)
# any later version.
#
# paparazzi is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with paparazzi; see the file COPYING.  If not, write to
# the Free Software Foundation, 59 Temple Place - Suite 330,
# Boston, MA 02111-1307, USA.

# The default is to produce a quiet echo of compilation commands
# Launch with "make Q=''" to get full echo

Q=@
PAPARAZZI_SRC=../..
EXT_DIR=$(PAPARAZZI_SRC)/sw/ext

PREFIX = arm-none-eabi

#
# if we can find arm-none-eabi-gcc in the path, overwrite PREFIX with explicit path
#
HAVE_ARM_NONE_EABI_GCC := $(shell which arm-none-eabi-gcc)

ifeq ($(strip $(HAVE_ARM_NONE_EABI_GCC)),)
# not found in PATH, check paparazzi toolchains

	TOOLCHAIN=$(shell find -L /opt/paparazzi/arm-multilib /opt/paparazzi/stm32 -maxdepth 1 -type d -name arm-none-eabi 2>/dev/null | head -n 1)
	ifneq ($(TOOLCHAIN),)
		TOOLCHAIN_DIR=$(shell dirname $(TOOLCHAIN))
		PREFIX = $(TOOLCHAIN_DIR)/bin/arm-none-eabi
	endif
endif


all: libopencm3.module

libopencm3.module:
	$(Q)if [ ! -f $(PAPARAZZI_SRC)/libopencm3/Makefile ]; then \
		cd $(PAPARAZZI_SRC); \
		git submodule init; \
		git submodule update; \
		cd -; \
	fi
	make -C libopencm3 lib PREFIX=$(PREFIX)

clean:
	if [ -f libopencm3/Makefile ]; then \
		make -C $(EXT_DIR)/libopencm3 clean; \
	fi
