lib_LTLIBRARIES = libarcwsaddressing.la
noinst_PROGRAMS = test

libarcwsaddressing_ladir = $(pkgincludedir)/ws-addressing
libarcwsaddressing_la_HEADERS = WSA.h
libarcwsaddressing_la_SOURCES = WSA.cpp
libarcwsaddressing_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libarcwsaddressing_la_LIBADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS)

test_SOURCES = test.cpp
test_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
test_LDADD = libarcwsaddressing.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS)
