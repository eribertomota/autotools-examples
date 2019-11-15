if BUILD_JS

lib_LTLIBRARIES = libplibjs.la

include_HEADERS = js.h

libplibjs_la_SOURCES = js.cxx jsLinux.cxx jsLinuxOld.cxx jsMacOS.cxx \
                             jsMacOSX.cxx jsWindows.cxx jsBSD.cxx   \
                             jsNone.cxx
libplibjs_la_LIBADD = ../util/libplibul.la
libplibjs_la_LDFLAGS = -version-info 9:5:8


INCLUDES = -I$(top_srcdir)/src/util

endif

EXTRA_DIST = js.dsp


