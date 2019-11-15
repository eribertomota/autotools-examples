#
# NASPRO - The NASPRO Architecture for Sound PROcessing
# Portable runtime library
#
# Copyright (C) 2007-2014 Stefano D'Angelo
#
# See the COPYING file for license conditions.
#

AM_CFLAGS = -pedantic -Wall -Werror @THREAD_FLAGS@
if WIN32
AM_CFLAGS += -Wno-error=format
endif
AM_LDFLAGS = -no-undefined -version-info @LT_CURRENT@:@LT_REVISION@:@LT_AGE@ \
	     @THREAD_FLAGS@
AM_CPPFLAGS = -I$(top_srcdir)/include

lib_LTLIBRARIES = libnacore.la
libnacore_la_SOURCES = internal.h localepvt.h types.c list.c avl.c string.c \
		       msg.c

if WIN32
libnacore_la_LIBADD = win32/libnacoreos.la
else
libnacore_la_LIBADD = posix/libnacoreos.la
endif

SUBDIRS = posix win32
