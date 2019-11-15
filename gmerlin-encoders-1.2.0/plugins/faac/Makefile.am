gmerlin_plugindir = @gmerlin_plugindir@

INCLUDES = -I$(top_srcdir)/include

AM_LDFLAGS = @GMERLIN_PLUGIN_LDFLAGS@ -avoid-version -module
AM_CFLAGS = @FAAC_CFLAGS@ -DLOCALE_DIR=\"$(localedir)\"

gmerlin_plugin_LTLIBRARIES = \
e_faac.la

e_faac_la_SOURCES = e_faac.c
e_faac_la_LIBADD = @GMERLIN_DEP_LIBS@ $(top_builddir)/lib/libgmerlin_encoders.la @FAAC_LIBS@
