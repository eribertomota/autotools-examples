SUBDIRS = schema

pkglib_LTLIBRARIES = libmcchttp.la
noinst_PROGRAMS = http_test http_test_withtls

libmcchttp_la_SOURCES = PayloadHTTP.cpp MCCHTTP.cpp PayloadHTTP.h MCCHTTP.h
libmcchttp_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libmcchttp_la_LIBADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la
libmcchttp_la_LDFLAGS  = $(LIBXML2_LIBS) -no-undefined -avoid-version -module

http_test_SOURCES = http_test.cpp
http_test_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
http_test_LDADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS)

http_test_withtls_SOURCES = http_test_withtls.cpp
http_test_withtls_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
http_test_withtls_LDADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(OPENSSL_LIBS)
