localedir = $(datadir)/locale

AM_CFLAGS = -DLOCALE_DIR=\"$(localedir)\" @SCHROEDINGER_CFLAGS@

pkglib_LTLIBRARIES = lqt_schroedinger.la
INCLUDES = -I$(top_srcdir)/include -I$(top_builddir)/include

lqt_schroedinger_la_SOURCES = \
schroedinger.c \
schroedinger_decode.c \
schroedinger_encode.c \
lqt_schroedinger.c

lqt_schroedinger_la_LDFLAGS = -avoid-version -module
lqt_schroedinger_la_LIBADD = @MODULE_LIBADD@ @SCHROEDINGER_LIBS@

noinst_HEADERS = schroedinger.h

EXTRA_DIST = extract_settings.c


