if BUILD_NET

lib_LTLIBRARIES = libplibnet.la

include_HEADERS = netBuffer.h netChannel.h netChat.h netMessage.h \
	netMonitor.h netSocket.h net.h

libplibnet_la_SOURCES = netBuffer.cxx netChannel.cxx netChat.cxx \
	netMessage.cxx netMonitor.cxx netSocket.cxx
libplibnet_la_LIBADD = ../util/libplibul.la
libplibnet_la_LDFLAGS = -version-info 9:5:8

INCLUDES = -I$(top_srcdir)/src/util

endif

EXTRA_DIST = net.dsp

