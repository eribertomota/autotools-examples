plugin_in_files = areacodes_global.plugin

include ../Makefile.plugins

plugindir = $(libdir)/routermanager/areacodes_global

plugin_LTLIBRARIES = libareacodes_global.la

sharedir = $(libdir)/routermanager/areacodes_global
share_DATA  = share/globalareacodes.csv

EXTRA_DIST += $(share_DATA)

libareacodes_global_la_SOURCES = \
	areacodes_global.c \
	csv.c \
	csv.h

libareacodes_global_la_CFLAGS = $(plugin_cflags) -DPLUGIN_DIR=\"$(plugindir)\"
libareacodes_global_la_LDFLAGS = $(plugin_ldflags)
libareacodes_global_la_LIBADD  = $(plugin_libadd)
