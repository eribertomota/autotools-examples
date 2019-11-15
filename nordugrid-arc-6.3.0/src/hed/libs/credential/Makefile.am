lib_LTLIBRARIES = libarccredential.la
#noinst_PROGRAMS = testproxy testcertinfo testproxy2proxy testvoms testeec

VOMS_HEADER = VOMSUtil.h VOMSConfig.h
VOMS_SOURCE = VOMSUtil.cpp VOMSConfig.cpp

if NSS_ENABLED
NSS_HEADER = NSSUtil.h nssprivkeyinfocodec.h
NSS_SOURCE = NSSUtil.cpp nssprivkeyinfocodec.cpp
else
NSS_HEADER =
NSS_SOURCE =
endif

libarccredential_ladir = $(pkgincludedir)/credential
libarccredential_la_HEADERS  = Credential.h CertUtil.h Proxycertinfo.h PasswordSource.h \
                               VOMSAttribute.h $(VOMS_HEADER) $(NSS_HEADER)
libarccredential_la_SOURCES  = Proxycertinfo.cpp CertUtil.cpp PasswordSource.cpp \
                               Credential.cpp listfunc.cpp listfunc.h \
                               VOMSAttribute.cpp $(VOMS_SOURCE) $(NSS_SOURCE)
libarccredential_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(NSS_CFLAGS) $(AM_CXXFLAGS)
libarccredential_la_CFLAGS = $(libarccredential_la_CXXFLAGS)
libarccredential_la_LIBADD = \
	$(top_builddir)/src/hed/libs/crypto/libarccrypto.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(OPENSSL_LIBS) $(NSS_LIBS)
libarccredential_la_LDFLAGS  = -version-info 3:0:0

testproxy_SOURCES = testproxy.cpp
testproxy_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
testproxy_LDADD = ./libarccredential.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS)

testcertinfo_SOURCES = testcertinfo.cpp
testcertinfo_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
testcertinfo_LDADD = ./libarccredential.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS)

testproxy2proxy_SOURCES = testproxy2proxy.cpp
testproxy2proxy_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
testproxy2proxy_LDADD = ./libarccredential.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS)

testvoms_SOURCES = testvoms.cpp
testvoms_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
testvoms_LDADD = ./libarccredential.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS)

testeec_SOURCES = testeec.cpp
testeec_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
testeec_LDADD = ./libarccredential.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS)

DIST_SUBDIRS = test
SUBDIRS = $(TEST_DIR)
