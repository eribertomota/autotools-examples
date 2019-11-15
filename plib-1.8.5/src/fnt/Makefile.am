if BUILD_FNT

lib_LTLIBRARIES = libplibfnt.la

include_HEADERS = fnt.h

libplibfnt_la_SOURCES = fnt.cxx fntTXF.cxx fntLocal.h fntBitmap.cxx
libplibfnt_la_LIBADD = ../util/libplibul.la
libplibfnt_la_LDFLAGS = -version-info 9:5:8

INCLUDES = -I$(top_srcdir)/src/sg -I$(top_srcdir)/src/util

endif

EXTRA_DIST = fnt.dsp

