SUBDIRS = . TEST

lib_LTLIBRARIES = libau-c-unit.la
pkginclude_HEADERS = autounit.h
noinst_HEADERS = au-netstring.h autounit-private.h

AM_CFLAGS = \
	$(GLIB_CFLAGS) \
	-I$(top_srcdir)/c-unit \
	-I.. \
	-I../intl \
	-I$(top_srcdir)/intl

libau_c_unit_la_SOURCES = test.c au-netstring.c suite.c assert.c
libau_c_unit_la_LIBADD = $(GLIB_LIBS)
libau_c_unit_la_LDFLAGS = -version-info 4:0:2
