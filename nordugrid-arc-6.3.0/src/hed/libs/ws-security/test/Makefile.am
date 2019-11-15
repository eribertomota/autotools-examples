if XMLSEC_ENABLED
TESTS = UsernameTokenTest X509TokenTest SAMLTokenTest 
else
TESTS = UsernameTokenTest
endif

TESTS_ENVIRONMENT = srcdir=$(srcdir)

check_PROGRAMS = $(TESTS)

UsernameTokenTest_SOURCES = $(top_srcdir)/src/Test.cpp UsernameTokenTest.cpp
UsernameTokenTest_CXXFLAGS = -I$(top_srcdir)/include \
        $(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
UsernameTokenTest_LDADD = \
        $(top_builddir)/src/hed/libs/message/libarcmessage.la \
        $(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/ws-security/libarcwssecurity.la \
        $(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS)

if XMLSEC_ENABLED
X509TokenTest_SOURCES = $(top_srcdir)/src/Test.cpp X509TokenTest.cpp
X509TokenTest_CXXFLAGS = -I$(top_srcdir)/include \
        $(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(XMLSEC_CFLAGS) $(AM_CXXFLAGS)
X509TokenTest_LDADD = \
        $(top_builddir)/src/hed/libs/message/libarcmessage.la \
        $(top_builddir)/src/hed/libs/common/libarccommon.la \
        $(top_builddir)/src/hed/libs/xmlsec/libarcxmlsec.la \
        $(top_builddir)/src/hed/libs/ws-security/libarcwssecurity.la \
        $(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(XMLSEC_LIBS)

SAMLTokenTest_SOURCES = $(top_srcdir)/src/Test.cpp SAMLTokenTest.cpp
SAMLTokenTest_CXXFLAGS = -I$(top_srcdir)/include \
        $(CPPUNIT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(XMLSEC_CFLAGS) $(AM_CXXFLAGS)
SAMLTokenTest_LDADD = \
        $(top_builddir)/src/hed/libs/message/libarcmessage.la \
        $(top_builddir)/src/hed/libs/common/libarccommon.la \
        $(top_builddir)/src/hed/libs/xmlsec/libarcxmlsec.la \
        $(top_builddir)/src/hed/libs/ws-security/libarcwssecurity.la \
        $(CPPUNIT_LIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(XMLSEC_LIBS)
endif
