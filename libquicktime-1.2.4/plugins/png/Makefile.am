localedir = $(datadir)/locale
AM_CFLAGS = @LIBPNG_CFLAGS@ -DLOCALE_DIR=\"$(localedir)\"
INCLUDES = -I$(top_srcdir)/include -I$(top_builddir)/include
pkglib_LTLIBRARIES = lqt_png.la

lqt_png_la_SOURCES = qtpng.c lqt_png.c
lqt_png_la_LDFLAGS = -avoid-version -module
lqt_png_la_LIBADD = @MODULE_LIBADD@ @LIBPNG_LIBS@ -lz -lm

noinst_HEADERS = qtpng.h
