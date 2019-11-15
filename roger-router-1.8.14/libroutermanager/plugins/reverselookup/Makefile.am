plugin_in_files = reverselookup.plugin

include ../Makefile.plugins

plugindir = $(libdir)/routermanager/reverselookup

plugin_LTLIBRARIES = libreverselookup.la

sharedir = $(libdir)/routermanager/reverselookup
share_DATA  = share/lookup.xml

EXTRA_DIST += $(share_DATA)

libreverselookup_la_SOURCES = \
	reverselookup.c \
	reverselookup.h

libreverselookup_la_CFLAGS = $(plugin_cflags) -DPLUGIN_DIR=\"$(plugindir)\" $(SOUP_CFLAGS)
libreverselookup_la_LDFLAGS = $(plugin_ldflags)
libreverselookup_la_LIBADD  = $(plugin_libadd) $(SOUP_LIBADD)
