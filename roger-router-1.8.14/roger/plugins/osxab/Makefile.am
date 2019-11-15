plugin_in_files = osxab.plugin

include ../Makefile.plugins

plugindir = $(libdir)/roger/osxab

plugin_LTLIBRARIES = libosxab.la

libosxab_la_SOURCES = \
	osxab.c

libosxab_la_CFLAGS = $(plugin_cflags)
libosxab_la_LDFLAGS = $(plugin_ldflags) -framework AddressBook -framework CoreFoundation -framework Accounts
libosxab_la_LIBADD  = $(plugin_libadd)
