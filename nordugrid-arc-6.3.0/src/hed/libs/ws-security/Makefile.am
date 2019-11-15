DIST_SUBDIRS = test
SUBDIRS = $(TEST_DIR)

lib_LTLIBRARIES = libarcwssecurity.la

if XMLSEC_ENABLED
noinst_PROGRAMS = test_usernametoken test_x509token test_samltoken
else 
noinst_PROGRAMS = test_usernametoken
endif

libarcwssecurity_ladir = $(pkgincludedir)/ws-security
if XMLSEC_ENABLED
libarcwssecurity_la_HEADERS = UsernameToken.h X509Token.h SAMLToken.h 
libarcwssecurity_la_SOURCES = UsernameToken.cpp X509Token.cpp SAMLToken.cpp
libarcwssecurity_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(OPENSSL_CFLAGS) \
	$(XMLSEC_CFLAGS) $(XMLSEC_OPENSSL_CFLAGS) $(AM_CXXFLAGS)
libarcwssecurity_la_LIBADD = \
	$(top_builddir)/src/hed/libs/xmlsec/libarcxmlsec.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS) $(OPENSSL_LIBS) \
	$(XMLSEC_LIBS) $(XMLSEC_OPENSSL_LIBS)
else
libarcwssecurity_la_HEADERS = UsernameToken.h
libarcwssecurity_la_SOURCES = UsernameToken.cpp
libarcwssecurity_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
libarcwssecurity_la_LIBADD = \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS) $(OPENSSL_LIBS)
endif
libarcwssecurity_la_LDFLAGS = -version-info 3:0:0

test_usernametoken_SOURCES = test_usernametoken.cpp 
test_usernametoken_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
test_usernametoken_LDADD = \
	libarcwssecurity.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS)

if XMLSEC_ENABLED
test_x509token_SOURCES = test_x509token.cpp
test_x509token_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(XMLSEC_OPENSSL_CFLAGS) $(XMLSEC_CFLAGS) $(AM_CXXFLAGS)
test_x509token_LDADD = \
	libarcwssecurity.la \
	$(top_builddir)/src/hed/libs/xmlsec/libarcxmlsec.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(OPENSSL_LIBS) $(XMLSEC_OPENSSL_LIBS) $(XMLSEC_LIBS)

test_samltoken_SOURCES = test_samltoken.cpp
test_samltoken_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(XMLSEC_OPENSSL_CFLAGS) $(XMLSEC_CFLAGS) $(AM_CXXFLAGS)
test_samltoken_LDADD = \
	libarcwssecurity.la \
	$(top_builddir)/src/hed/libs/xmlsec/libarcxmlsec.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(OPENSSL_LIBS) $(XMLSEC_OPENSSL_LIBS) $(XMLSEC_LIBS)
endif
