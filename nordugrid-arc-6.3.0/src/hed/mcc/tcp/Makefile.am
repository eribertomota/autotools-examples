SUBDIRS = schema

pkglib_LTLIBRARIES = libmcctcp.la

libmcctcp_la_SOURCES = MCCTCP.cpp PayloadTCPSocket.cpp \
                       MCCTCP.h   PayloadTCPSocket.h
libmcctcp_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libmcctcp_la_LIBADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS)
libmcctcp_la_LDFLAGS  = -no-undefined -avoid-version -module
