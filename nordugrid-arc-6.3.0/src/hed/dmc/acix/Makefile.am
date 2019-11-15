pkglib_LTLIBRARIES = libdmcacix.la

libdmcacix_la_SOURCES = DataPointACIX.cpp DataPointACIX.h
libdmcacix_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS) $(OPENSSL_CFLAGS)
libdmcacix_la_LIBADD = \
    $(top_builddir)/src/external/cJSON/libcjson.la \
	$(top_builddir)/src/hed/libs/communication/libarccommunication.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS) $(OPENSSL_LIBS)
libdmcacix_la_LDFLAGS = -no-undefined -avoid-version -module
