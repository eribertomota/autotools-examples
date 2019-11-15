SUBDIRS = data

plugin_in_files = indicator.plugin

include ../Makefile.plugins

plugindir = $(libdir)/roger/indicator

plugin_LTLIBRARIES = libindicator.la

libindicator_la_SOURCES = \
	indicator.c

libindicator_la_CFLAGS = $(plugin_cflags) $(APPINDICATOR_CFLAGS) $(EXTRA_CFLAGS)
libindicator_la_LDFLAGS = $(plugin_ldflags)
libindicator_la_LIBADD  = $(plugin_libadd) $(APPINDICATOR_LIBS)
