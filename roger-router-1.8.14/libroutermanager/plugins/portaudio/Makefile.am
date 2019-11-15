plugin_in_files = portaudio.plugin

include ../Makefile.plugins

plugindir = $(libdir)/routermanager/portaudio

plugin_LTLIBRARIES = libportaudio.la

libportaudio_la_SOURCES = \
	portaudio.c

libportaudio_la_CFLAGS = $(plugin_cflags)
libportaudio_la_LDFLAGS = $(plugin_ldflags)
libportaudio_la_LIBADD  = $(plugin_libadd) $(PORTAUDIO_LIBS)
