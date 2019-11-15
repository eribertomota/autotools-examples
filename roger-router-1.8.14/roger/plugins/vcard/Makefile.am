SUBDIRS = data

plugin_in_files = vcard.plugin

include ../Makefile.plugins

plugindir = $(libdir)/roger/vcard

plugin_LTLIBRARIES = libvcard.la

libvcard_la_SOURCES = \
	vcard.c \
	vcard.h

libvcard_la_CFLAGS = $(plugin_cflags) $(EXTRA_CFLAGS)
libvcard_la_LDFLAGS = $(plugin_ldflags) $(EXTRA_LIBS)
libvcard_la_LIBADD  = $(plugin_libadd) $(EXTRA_LIBS)
