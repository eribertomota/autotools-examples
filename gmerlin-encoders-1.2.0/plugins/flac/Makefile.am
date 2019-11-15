gmerlin_plugindir = @gmerlin_plugindir@

INCLUDES = -I$(top_srcdir)/include

AM_LDFLAGS = @GMERLIN_PLUGIN_LDFLAGS@ -avoid-version -module
AM_CFLAGS = @FLAC_CFLAGS@ -DLOCALE_DIR=\"$(localedir)\"

gmerlin_plugin_LTLIBRARIES = \
e_flac.la

e_flac_la_SOURCES = e_flac.c
e_flac_la_LIBADD = @GMERLIN_DEP_LIBS@ $(top_builddir)/lib/libgmerlin_encoders.la $(top_builddir)/lib/libbgflac.la @FLAC_LIBS@
