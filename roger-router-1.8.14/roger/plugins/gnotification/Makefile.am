SUBDIRS = data

plugin_in_files = gnotification.plugin

include ../Makefile.plugins

plugindir = $(libdir)/roger/gnotification

plugin_LTLIBRARIES = libgnotification.la

libgnotification_la_SOURCES = \
	gnotification.c

libgnotification_la_CFLAGS = $(plugin_cflags)
libgnotification_la_LDFLAGS = $(plugin_ldflags)
libgnotification_la_LIBADD  = $(plugin_libadd)
