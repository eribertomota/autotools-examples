if BUILD_SG

lib_LTLIBRARIES = libplibsg.la

include_HEADERS = sg.h

libplibsg_la_SOURCES = sg.cxx sgd.cxx \
                      sgIsect.cxx sgdIsect.cxx \
                      sgPerlinNoise.cxx
libplibsg_la_LIBADD = ../util/libplibul.la
libplibsg_la_LDFLAGS = -version-info 9:5:8

INCLUDES = -I$(top_srcdir)/src/util

endif

EXTRA_DIST = sg.dsp

