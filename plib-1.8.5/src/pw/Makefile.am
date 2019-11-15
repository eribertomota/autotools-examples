if BUILD_PW

lib_LTLIBRARIES = libplibpw.la

include_HEADERS = pw.h

libplibpw_la_SOURCES = pw.cxx pwX11.cxx pwWindows.cxx pwMacOSX.cxx
libplibpw_la_LDFLAGS = -version-info 9:5:8

INCLUDES = -I$(top_srcdir)/src/util

endif

EXTRA_DIST = pw.dsp

