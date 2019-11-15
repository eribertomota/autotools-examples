pkglib_LTLIBRARIES = libaccARCHERY.la

libaccARCHERY_la_SOURCES  = DescriptorsARCHERY.cpp \
    ServiceEndpointRetrieverPluginARCHERY.cpp ServiceEndpointRetrieverPluginARCHERY.h
libaccARCHERY_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS) $(LDNS_CFLAGS)
libaccARCHERY_la_LIBADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/communication/libarccommunication.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS) $(LDNS_LIBS)
libaccARCHERY_la_LDFLAGS = -no-undefined -avoid-version -module
