SUBDIRS = data

plugin_in_files = notification.plugin

include ../Makefile.plugins

plugindir = $(libdir)/roger/notification

plugin_LTLIBRARIES = libnotification.la

libnotification_la_SOURCES = \
	notification.c

libnotification_la_CFLAGS = $(plugin_cflags) $(LIBNOTIFY_CFLAGS)
libnotification_la_LDFLAGS = $(plugin_ldflags)
libnotification_la_LIBADD  = $(plugin_libadd) $(LIBNOTIFY_LIBS)
