#pkglib_LTLIBRARIES = libsaml2sp.la
noinst_LTLIBRARIES = libsaml2ssoassertionconsumersh.la

#libsaml2sp_la_SOURCES = SPService.cpp SPService.h
#libsaml2sp_la_CXXFLAGS = -I$(top_srcdir)/include \
#	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) \
#	$(XMLSEC_OPENSSL_CFLAGS) $(XMLSEC_CFLAGS) $(AM_CXXFLAGS)
#libsaml2sp_la_LIBADD = \
#	$(top_builddir)/src/hed/libs/xmlsec/libarcxmlsec.la \
#	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
#	$(top_builddir)/src/hed/libs/common/libarccommon.la \
#	$(XMLSEC_OPENSSL_LIBS) $(XMLSEC_LIBS) $(LIBXML2_LIBS)
#libsaml2sp_la_LDFLAGS = -no-undefined -avoid-version -module

libsaml2ssoassertionconsumersh_la_SOURCES = \
	SAML2SSO_AssertionConsumerSH.cpp SAML2SSO_AssertionConsumerSH.h
libsaml2ssoassertionconsumersh_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) \
	$(XMLSEC_OPENSSL_CFLAGS) $(XMLSEC_CFLAGS) $(AM_CXXFLAGS)
libsaml2ssoassertionconsumersh_la_LIBADD = \
	$(top_builddir)/src/hed/libs/ws-security/libarcwssecurity.la \
	$(top_builddir)/src/hed/libs/xmlsec/libarcxmlsec.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(XMLSEC_OPENSSL_LIBS) $(XMLSEC_LIBS)
