plugin_in_files = secret.plugin

include ../Makefile.plugins

plugindir = $(libdir)/routermanager/secret

plugin_LTLIBRARIES = libsecret.la

libsecret_la_SOURCES = \
	secret.c \
	secret.h

libsecret_la_CFLAGS = $(plugin_cflags) $(SECRET_CFLAGS)
libsecret_la_LDFLAGS = $(plugin_ldflags) $(SECRET_LIBS)
libsecret_la_LIBADD  = $(plugin_libadd) $(SECRET_LIBS)
