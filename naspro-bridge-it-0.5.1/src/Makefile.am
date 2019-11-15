#
# NASPRO - The NASPRO Architecture for Sound PROcessing
# LV2 bridging helper library
#
# Copyright (C) 2007-2014 Stefano D'Angelo
#
# See the COPYING file for license conditions.
#

AM_CFLAGS = -pedantic -Wall -Werror @NACORE_CFLAGS@ @LV2_CFLAGS@
AM_LDFLAGS = -no-undefined -version-info @LT_CURRENT@:@LT_REVISION@:@LT_AGE@ \
	     @NACORE_LIBS@ @LV2_LIBS@
AM_CPPFLAGS = -I$(top_srcdir)/include

lib_LTLIBRARIES = libnabrit.la
libnabrit_la_SOURCES = internal.h bridge.h bridge.c pluglib.h pluglib.c \
		       plugin.h plugin.c port.h port.c preset.h preset.c \
		       manifest.c util.c
