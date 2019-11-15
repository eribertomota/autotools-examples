plugin_in_files = webjournal.plugin

include ../Makefile.plugins

plugindir = $(libdir)/routermanager/webjournal

plugin_LTLIBRARIES = libwebjournal.la

sharedir = $(libdir)/routermanager/webjournal
share_DATA  = share/header.html
share_DATA  += share/entry.html
share_DATA  += share/footer.html
share_DATA  += share/style.css

EXTRA_DIST += $(share_DATA)

libwebjournal_la_SOURCES = \
	webjournal.c \
	webjournal.h

libwebjournal_la_CFLAGS = $(plugin_cflags) -DPLUGIN_DIR=\"$(plugindir)\" $(SOUP_CFLAGS)
libwebjournal_la_LDFLAGS = $(plugin_ldflags)
libwebjournal_la_LIBADD  = $(plugin_libadd) $(SOUP_LIBADD)
