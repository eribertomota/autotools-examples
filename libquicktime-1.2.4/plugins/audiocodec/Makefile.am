localedir = $(datadir)/locale
AM_CFLAGS = -DLOCALE_DIR=\"$(localedir)\"
pkglib_LTLIBRARIES = lqt_audiocodec.la

INCLUDES = -I$(top_srcdir)/include -I$(top_builddir)/include

lqt_audiocodec_la_SOURCES = \
ima4.c \
pcm.c \
lqt_audiocodec.c

lqt_audiocodec_la_LDFLAGS = -avoid-version -module
lqt_audiocodec_la_LIBADD = @MODULE_LIBADD@

noinst_HEADERS = \
alaw_tables.h \
audiocodec.h \
ulaw_tables.h

