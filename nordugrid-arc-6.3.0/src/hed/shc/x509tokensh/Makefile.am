SUBDIRS = schema

noinst_LTLIBRARIES = libx509tokensh.la

libx509tokensh_la_SOURCES = X509TokenSH.cpp X509TokenSH.h

libx509tokensh_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) \
	$(XMLSEC_OPENSSL_CFLAGS) $(XMLSEC_CFLAGS) $(AM_CXXFLAGS)
libx509tokensh_la_LIBADD = \
	$(top_builddir)/src/hed/libs/ws-security/libarcwssecurity.la \
	$(top_builddir)/src/hed/libs/xmlsec/libarcxmlsec.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(XMLSEC_OPENSSL_LIBS) $(XMLSEC_LIBS)
