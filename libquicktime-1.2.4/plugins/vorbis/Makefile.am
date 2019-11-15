localedir = $(datadir)/locale
AM_CFLAGS = @VORBIS_CFLAGS@ -DLOCALE_DIR=\"$(localedir)\"
INCLUDES = -I$(top_srcdir)/include -I$(top_builddir)/include/
pkglib_LTLIBRARIES = lqt_vorbis.la

lqt_vorbis_la_SOURCES = vorbis.c lqt_vorbis.c
lqt_vorbis_la_LDFLAGS = -avoid-version -module
lqt_vorbis_la_LIBADD = @MODULE_LIBADD@ @VORBISENC_LIBS@ @VORBIS_LIBS@ @VORBISFILE_LIBS@

noinst_HEADERS = qtvorbis.h

