pkglib_LTLIBRARIES = libdmcsrm.la

SUBDIRS = srmclient

libdmcsrm_la_SOURCES = DataPointSRM.cpp DataPointSRM.h
libdmcsrm_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
libdmcsrm_la_LIBADD = \
	srmclient/libsrmclient.la \
	$(top_builddir)/src/hed/libs/communication/libarccommunication.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS)
libdmcsrm_la_LDFLAGS = -no-undefined -avoid-version -module
