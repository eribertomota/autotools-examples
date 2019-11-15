SUBDIRS = data

plugin_in_files = fritzfon.plugin

include ../Makefile.plugins

plugindir = $(libdir)/roger/fritzfon

plugin_LTLIBRARIES = libfritzfon.la

libfritzfon_la_SOURCES = \
	fritzfon.c

libfritzfon_la_CFLAGS = $(plugin_cflags) $(EXTRA_CFLAGS) $(SOUP_CFLAGS)
libfritzfon_la_LDFLAGS = $(plugin_ldflags) $(EXTRA_LIBS) $(SOUP_LIBS)
libfritzfon_la_LIBADD  = $(plugin_libadd) $(EXTRA_LIBS) $(SOUP_LIBS)
