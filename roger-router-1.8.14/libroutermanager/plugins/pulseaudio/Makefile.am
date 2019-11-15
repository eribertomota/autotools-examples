plugin_in_files = pulseaudio.plugin

include ../Makefile.plugins

plugindir = $(libdir)/routermanager/pulseaudio

plugin_LTLIBRARIES = libpulseaudio.la

libpulseaudio_la_SOURCES = \
	pulseaudio.c

libpulseaudio_la_CFLAGS = $(plugin_cflags)
libpulseaudio_la_LDFLAGS = $(plugin_ldflags)
libpulseaudio_la_LIBADD  = $(plugin_libadd) $(PULSEAUDIO_LIBS)
