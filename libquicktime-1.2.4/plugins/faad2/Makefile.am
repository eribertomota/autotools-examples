localedir = $(datadir)/locale
AM_CFLAGS = @FAAD2_CFLAGS@ -DLOCALE_DIR=\"$(localedir)\"
INCLUDES = -I$(top_srcdir)/include -I$(top_builddir)/include
pkglib_LTLIBRARIES = lqt_faad2.la

lqt_faad2_la_SOURCES = faad2.c lqt_faad2.c
lqt_faad2_la_LDFLAGS = -avoid-version -module
lqt_faad2_la_LIBADD = @MODULE_LIBADD@ @FAAD2_LIBS@

noinst_HEADERS = faad2.h 
