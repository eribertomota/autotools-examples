plugin_in_files = fritzbox.plugin

include ../Makefile.plugins

plugindir = $(libdir)/routermanager/fritzbox

plugin_LTLIBRARIES = libfritzbox.la

libfritzbox_la_SOURCES = \
	fritzbox.c \
	fritzbox.h \
	firmware-common.c \
	firmware-common.h \
	firmware-04-00.c \
	firmware-04-00.h \
	firmware-04-74.c \
	firmware-04-74.h \
	firmware-05-50.c \
	firmware-05-50.h \
	firmware-06-35.c \
	firmware-06-35.h \
	csv.c \
	csv.h

libfritzbox_la_CFLAGS = $(plugin_cflags) $(SOUP_CFLAGS)
libfritzbox_la_LDFLAGS = $(plugin_ldflags)
libfritzbox_la_LIBADD  = $(plugin_libadd) $(SOUP_LIBS)
