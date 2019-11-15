plugin_in_files = callmonitor.plugin

include ../Makefile.plugins

plugindir = $(libdir)/routermanager/callmonitor

plugin_LTLIBRARIES = libcallmonitor.la

libcallmonitor_la_SOURCES = \
	callmonitor.c

libcallmonitor_la_CFLAGS = $(plugin_cflags)
libcallmonitor_la_LDFLAGS = $(plugin_ldflags)
libcallmonitor_la_LIBADD  = $(plugin_libadd)
