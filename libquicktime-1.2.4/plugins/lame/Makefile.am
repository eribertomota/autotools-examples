localedir = $(datadir)/locale
pkglib_LTLIBRARIES = lqt_lame.la
INCLUDES = -I$(top_srcdir)/include -I$(top_builddir)/include
lqt_lame_la_SOURCES = \
lame_codec.c \
lqt_lame.c

AM_CFLAGS = @LAME_CFLAGS@ -DLOCALE_DIR=\"$(localedir)\"

lqt_lame_la_LDFLAGS = -avoid-version -module
lqt_lame_la_LIBADD = @MODULE_LIBADD@ @LAME_LIBS@

noinst_HEADERS = lame_codec.h