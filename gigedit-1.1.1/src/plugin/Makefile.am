AM_CPPFLAGS = $(GTKMM_CFLAGS) $(GTK_CFLAGS) $(GIG_CFLAGS)

pkglibdir = $(LINUXSAMPLER_PLUGIN_DIR)

pkglib_LTLIBRARIES = \
	libgigeditlinuxsamplerplugin.la
libgigeditlinuxsamplerplugin_la_SOURCES = \
	linuxsamplerplugin.cpp \
	linuxsamplerplugin.h
libgigeditlinuxsamplerplugin_la_LIBADD = \
	$(top_builddir)/src/gigedit/libgigedit.la \
	$(GTKMM_LIBS) $(GTK_LIBS) $(GIG_LIBS)
libgigeditlinuxsamplerplugin_la_CXXFLAGS = \
	$(LINUXSAMPLER_CFLAGS)
libgigeditlinuxsamplerplugin_la_LDFLAGS = \
	-module -avoid-version -no-undefined
