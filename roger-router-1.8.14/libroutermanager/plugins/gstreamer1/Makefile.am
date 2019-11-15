plugin_in_files = gstreamer1.plugin

include ../Makefile.plugins

plugindir = $(libdir)/routermanager/gstreamer1

plugin_LTLIBRARIES = libgstreamer1.la

libgstreamer1_la_SOURCES = \
	gstreamer.c

libgstreamer1_la_CFLAGS = $(plugin_cflags) $(GSTREAMER1_CFLAGS) -DGST_DISABLE_DEPRECATED
libgstreamer1_la_LDFLAGS = $(plugin_ldflags)
libgstreamer1_la_LIBADD  = $(plugin_libadd) $(GSTREAMER1_LIBS)
