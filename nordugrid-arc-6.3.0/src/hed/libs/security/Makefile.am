SUBDIRS = ArcPDP

lib_LTLIBRARIES = libarcsecurity.la

libarcsecurity_ladir = $(pkgincludedir)/security
libarcsecurity_la_HEADERS = PDP.h   Security.h   ClassLoader.h
libarcsecurity_la_SOURCES = PDP.cpp Security.cpp ClassLoader.cpp
libarcsecurity_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libarcsecurity_la_LIBADD = \
	ArcPDP/libarcpdp.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS) $(GTHREAD_LIBS)
libarcsecurity_la_LDFLAGS  = -version-info 3:0:0
