TESTS = CredentialTest VOMSUtilTest listfuncTest
TESTS_ENVIRONMENT = srcdir=$(srcdir)
check_PROGRAMS = $(TESTS)
check_DATA = ca_key.pem ca_cert.pem

CredentialTest_SOURCES = $(top_srcdir)/src/Test.cpp CredentialTest.cpp
CredentialTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
CredentialTest_LDADD = \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS)

VOMSUtilTest_SOURCES = $(top_srcdir)/src/Test.cpp VOMSUtilTest.cpp
VOMSUtilTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
VOMSUtilTest_LDADD = \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

listfuncTest_SOURCES = $(top_srcdir)/src/Test.cpp listfuncTest.cpp
listfuncTest_CXXFLAGS = -I$(top_srcdir)/include \
	$(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
listfuncTest_LDADD = \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

ca_key.pem ca_cert.pem:
	openssl req -x509 -set_serial 1 -passout pass:password -newkey rsa:2048 -keyout ca_key.pem -out ca_cert.pem -config $(srcdir)/ca.cnf

EXTRA_DIST = ca.cnf

CLEANFILES = *.pem ca_serial
