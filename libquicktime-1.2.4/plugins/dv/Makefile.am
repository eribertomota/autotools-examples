localedir = $(datadir)/locale
AM_CFLAGS = @LIBDV_CFLAGS@ -DLOCALE_DIR=\"$(localedir)\"
INCLUDES = -I$(top_srcdir)/include -I$(top_builddir)/include/
pkglib_LTLIBRARIES = lqt_dv.la

lqt_dv_la_SOURCES = dv.c lqt_dv.c
lqt_dv_la_LDFLAGS = -avoid-version -module -lm

lqt_dv_la_LIBADD = @MODULE_LIBADD@ @LIBDV_LIBS@

noinst_HEADERS = dv.h

