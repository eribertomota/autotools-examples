SUBDIRS = data

plugin_in_files = google.plugin

include ../Makefile.plugins

plugindir = $(libdir)/roger/google

plugin_LTLIBRARIES = libgoogle.la

libgoogle_la_SOURCES = \
	google.c

libgoogle_la_CFLAGS = $(plugin_cflags) $(EXTRA_CFLAGS) $(SOUP_CFLAGS) $(GDATA_CFLAGS)
libgoogle_la_LDFLAGS = $(plugin_ldflags) $(EXTRA_LIBS) $(SOUP_LIBS) $(GDATA_LIBS)
libgoogle_la_LIBADD  = $(plugin_libadd) $(EXTRA_LIBS) $(SOUP_LIBS) $(GDATA_LIBS)
