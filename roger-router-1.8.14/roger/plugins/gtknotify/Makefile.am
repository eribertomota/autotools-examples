SUBDIRS = data

plugin_in_files = gtknotify.plugin

include ../Makefile.plugins

plugindir = $(libdir)/roger/gtknotify

plugin_LTLIBRARIES = libgtknotify.la

libgtknotify_la_SOURCES = \
	gtknotify.c

libgtknotify_la_CFLAGS = $(plugin_cflags) $(EXTRA_CFLAGS)
libgtknotify_la_LDFLAGS = $(plugin_ldflags) $(EXTRA_LIBS)
libgtknotify_la_LIBADD  = $(plugin_libadd) $(EXTRA_LIBS)
