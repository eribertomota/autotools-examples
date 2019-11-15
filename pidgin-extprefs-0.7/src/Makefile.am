plugindir = $(libdir)/pidgin

libextprefs_la_LDFLAGS = -module -avoid-version

if PLUGINS

plugin_LTLIBRARIES = libextprefs.la

libextprefs_la_SOURCES = extendedprefs.c

endif

AM_CPPFLAGS = \
	-DEP_VERSION=\"$(VERSION)\" \
	-DLIBDIR=\"$(libdir)/pidgin/\" \
	-DDATADIR=\"$(datadir)\" \
	$(GTK_CFLAGS) \
	$(PIDGIN_CFLAGS) \
	$(PURPLE_CFLAGS) \
	$(DEBUG_CFLAGS)
