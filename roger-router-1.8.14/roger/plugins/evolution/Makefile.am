SUBDIRS = data

plugin_in_files = evolution.plugin

include ../Makefile.plugins

plugindir = $(libdir)/roger/evolution

plugin_LTLIBRARIES = libevolution.la

libevolution_la_SOURCES = \
	ebook-sources.h \
	evolution.c

libevolution_la_CFLAGS = $(plugin_cflags) $(EBOOK_CFLAGS)
libevolution_la_LDFLAGS = $(plugin_ldflags)  $(EBOOK_FLAGS)
libevolution_la_LIBADD  = $(plugin_libadd) $(EBOOK_LIBS)
