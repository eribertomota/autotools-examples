gmerlin_plugindir = @gmerlin_plugindir@

INCLUDES = -I$(top_srcdir)/include

AM_LDFLAGS = @GMERLIN_PLUGIN_LDFLAGS@ -avoid-version -module
AM_CFLAGS = @LAME_CFLAGS@ -DLOCALE_DIR=\"$(localedir)\"

if HAVE_SHOUT
shout_plugins = b_lame.la
bgshout_libs    = $(top_builddir)/lib/libbgshout.la @SHOUT_LIBS@
else
shout_plugins =
endif


gmerlin_plugin_LTLIBRARIES = \
e_lame.la \
$(shout_plugins)

e_lame_la_SOURCES = e_lame.c xing.c bglame.c
e_lame_la_LIBADD = @GMERLIN_DEP_LIBS@ $(top_builddir)/lib/libgmerlin_encoders.la @LAME_LIBS@

b_lame_la_CFLAGS = $(AM_CFLAGS)
b_lame_la_SOURCES = b_lame.c bglame.c
b_lame_la_LIBADD = @GMERLIN_DEP_LIBS@ @LAME_LIBS@ $(bgshout_libs)

noinst_HEADERS = xing.h bglame.h