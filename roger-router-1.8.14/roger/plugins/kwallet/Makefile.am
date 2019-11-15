plugin_in_files = kwallet.plugin

include ../Makefile.plugins

plugindir = $(libdir)/roger/kwallet

plugin_LTLIBRARIES = libkwallet.la

libkwallet_la_SOURCES = \
	kwallet.cpp \
	kwallet_wrapper.cpp

libkwallet_la_CXXFLAGS = $(plugin_cflags) $(KWALLET_CFLAGS)
libkwallet_la_LDFLAGS = $(plugin_ldflags) $(KWALLET_LIBS)
libkwallet_la_LIBADD  = $(plugin_libadd) $(KWALLET_LIBS)
