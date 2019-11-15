lib_LTLIBRARIES = libarccommunication.la

if XMLSEC_ENABLED
ARCLIBS_WITH_XMLSEC = $(top_builddir)/src/hed/libs/xmlsec/libarcxmlsec.la
LIBS_WITH_XMLSEC = $(XMLSEC_OPENSSL_LIBS) $(XMLSEC_LIBS)
CFLAGS_WITH_XMLSEC = $(XMLSEC_OPENSSL_CFLAGS) $(XMLSEC_CFLAGS)
HEADER_WITH_XMLSEC = ClientSAML2SSO.h
SOURCE_WITH_XMLSEC = ClientSAML2SSO.cpp
else
ARCLIBS_WITH_XMLSEC =
LIBS_WITH_XMLSEC =
CFLAGS_WITH_XMLSEC =
HEADER_WITH_XMLSEC =
SOURCE_WITH_XMLSEC =
endif

libarccommunication_ladir = $(pkgincludedir)/communication
libarccommunication_la_HEADERS = ClientInterface.h ClientX509Delegation.h $(HEADER_WITH_XMLSEC)
libarccommunication_la_SOURCES = ClientInterface.cpp ClientX509Delegation.cpp $(SOURCE_WITH_XMLSEC)
libarccommunication_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(CFLAGS_WITH_XMLSEC) $(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(OPENSSL_CFLAGS) \
	$(AM_CXXFLAGS)
libarccommunication_la_LIBADD = \
	$(ARCLIBS_WITH_XMLSEC) \
	$(top_builddir)/src/hed/libs/delegation/libarcdelegation.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBS_WITH_XMLSEC) $(LIBXML2_LIBS) $(GLIBMM_LIBS)
libarccommunication_la_LDFLAGS = -version-info 3:0:0
