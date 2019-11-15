#
# NASPRO - The NASPRO Architecture for Sound PROcessing
# Portable runtime library
#
# Copyright (C) 2007-2014 Stefano D'Angelo
#
# See the COPYING file for license conditions.
#

if WIN32
AM_CFLAGS = -pedantic -Wall -Werror @THREAD_FLAGS@
AM_LDFLAGS = -no-undefined -version-info @LT_CURRENT@:@LT_REVISION@:@LT_AGE@ \
	     @THREAD_FLAGS@
AM_CPPFLAGS = -I$(top_srcdir)/include -I$(top_srcdir)/src

noinst_LTLIBRARIES = libnacoreos.la
libnacoreos_la_SOURCES = env.c locale.c fs.c dl.c thread.c mutex.c sem.c
endif
