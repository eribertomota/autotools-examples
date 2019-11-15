localedir = $(datadir)/locale
noinst_HEADERS = \
jpeg.h \
libmjpeg.h

AM_CFLAGS = @JPEG_CFLAGS@ -DLOCALE_DIR=\"$(localedir)\"
INCLUDES = -I$(top_srcdir)/include -I$(top_builddir)/include

pkglib_LTLIBRARIES = lqt_mjpeg.la

lqt_mjpeg_la_SOURCES = \
jpeg.c \
lqt_mjpeg.c \
libmjpeg.c

lqt_mjpeg_la_LDFLAGS = -avoid-version -module
lqt_mjpeg_la_LIBADD = @MODULE_LIBADD@ @JPEG_LIBS@

