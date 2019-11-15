SUBDIRS = data

plugin_in_files = thunderbird.plugin

include ../Makefile.plugins

plugindir = $(libdir)/roger/thunderbird

plugin_LTLIBRARIES = libthunderbird.la

libthunderbird_la_SOURCES = \
	thunderbird.c

libthunderbird_la_CFLAGS = $(plugin_cflags) $(EXTRA_CFLAGS) $(SOUP_CFLAGS)
libthunderbird_la_LDFLAGS = $(plugin_ldflags) $(EXTRA_LIBS) $(SOUP_LIBS)
libthunderbird_la_LIBADD  = $(plugin_libadd) $(EXTRA_LIBS) $(SOUP_LIBS)
