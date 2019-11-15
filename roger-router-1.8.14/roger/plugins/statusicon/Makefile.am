SUBDIRS = data

plugin_in_files = statusicon.plugin

include ../Makefile.plugins

plugindir = $(libdir)/roger/statusicon

plugin_LTLIBRARIES = libstatusicon.la

libstatusicon_la_SOURCES = \
	gtk.c

libstatusicon_la_CFLAGS = $(plugin_cflags)
libstatusicon_la_LDFLAGS = $(plugin_ldflags)
libstatusicon_la_LIBADD  = $(plugin_libadd)
