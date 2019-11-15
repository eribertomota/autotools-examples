pkglib_LTLIBRARIES = libmccsoap.la

libmccsoap_la_SOURCES = MCCSOAP.cpp MCCSOAP.h
libmccsoap_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libmccsoap_la_LIBADD = \
	$(top_builddir)/src/hed/libs/ws-addressing/libarcwsaddressing.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS)
libmccsoap_la_LDFLAGS  = -no-undefined -avoid-version -module
