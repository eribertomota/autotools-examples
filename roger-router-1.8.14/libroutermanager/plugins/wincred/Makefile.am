plugin_in_files = wincred.plugin

include ../Makefile.plugins

plugindir = $(libdir)/roger/wincred

plugin_LTLIBRARIES = libwincred.la

libwincred_la_SOURCES = \
	wincred.c

libwincred_la_CFLAGS = $(plugin_cflags) $(wincred_CFLAGS)
libwincred_la_LDFLAGS = $(plugin_ldflags) $(wincred_LIBS)
libwincred_la_LIBADD  = $(plugin_libadd) $(wincred_LIBS)
