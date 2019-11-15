lib_LTLIBRARIES = libarcxmlsec.la

libarcxmlsec_ladir = $(pkgincludedir)/xmlsec
libarcxmlsec_la_HEADERS = XmlSecUtils.h XMLSecNode.h saml_util.h
libarcxmlsec_la_SOURCES = XmlSecUtils.cpp XMLSecNode.cpp saml_util.cpp
libarcxmlsec_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(OPENSSL_CFLAGS) \
	$(XMLSEC_OPENSSL_CFLAGS) $(XMLSEC_CFLAGS) $(AM_CXXFLAGS)
libarcxmlsec_la_LIBADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS) $(OPENSSL_LIBS) \
	$(XMLSEC_OPENSSL_LIBS) $(XMLSEC_LIBS) $(ZLIB_LIBS)
libarcxmlsec_la_LDFLAGS  = -version-info 3:0:0

noinst_PROGRAMS = test_xmlsecnode

test_xmlsecnode_SOURCES = test_xmlsecnode.cpp
test_xmlsecnode_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(XMLSEC_CFLAGS) $(AM_CXXFLAGS)
test_xmlsecnode_LDADD = \
	libarcxmlsec.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(XMLSEC_LIBS)
