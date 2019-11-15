plugin_in_files = keychain.plugin

include ../Makefile.plugins

plugindir = $(libdir)/roger/keychain

plugin_LTLIBRARIES = libkeychain.la

libkeychain_la_SOURCES = keychain.c

libkeychain_la_CXXFLAGS = $(plugin_cflags) $(KEYCHAIN_CFLAGS)
libkeychain_la_LDFLAGS = $(plugin_ldflags) $(KEYCHAIN_LIBS) -framework ApplicationServices
libkeychain_la_LIBADD  = $(plugin_libadd) $(KEYCHAIN_LIBS)
