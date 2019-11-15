if XMLSEC_ENABLED
LIBS_WITH_XMLSEC = \
	x509tokensh/libx509tokensh.la \
	samltokensh/libsamltokensh.la \
	saml2sso_assertionconsumersh/libsaml2ssoassertionconsumersh.la
SUBDIRS_XMLSEC = x509tokensh samltokensh saml2sso_assertionconsumersh
else
LIBS_WITH_XMLSEC = 
SUBDIRS_XMLSEC =
endif

SUBDIRS = allowpdp denypdp simplelistpdp arcpdp xacmlpdp \
	pdpserviceinvoker arcauthzsh delegationpdp usernametokensh gaclpdp \
	$(SUBDIRS_XMLSEC) delegationsh legacy
DIST_SUBDIRS = allowpdp denypdp simplelistpdp arcpdp xacmlpdp \
	pdpserviceinvoker arcauthzsh delegationpdp usernametokensh gaclpdp \
	x509tokensh samltokensh saml2sso_assertionconsumersh delegationsh legacy
noinst_PROGRAMS = test testinterface_arc testinterface_xacml

pkglib_LTLIBRARIES = libarcshc.la

libarcshc_la_SOURCES = SecHandlerPlugin.cpp
libarcshc_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libarcshc_la_LIBADD = \
	allowpdp/liballowpdp.la denypdp/libdenypdp.la \
	simplelistpdp/libsimplelistpdp.la arcpdp/libarcpdp.la \
	xacmlpdp/libxacmlpdp.la gaclpdp/libgaclpdp.la \
	pdpserviceinvoker/libarcpdpserviceinvoker.la \
	delegationpdp/libdelegationpdp.la \
	arcauthzsh/libarcauthzsh.la usernametokensh/libusernametokensh.la \
	$(LIBS_WITH_XMLSEC) \
	delegationsh/libdelegationsh.la \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/security/libarcsecurity.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS)
libarcshc_la_LDFLAGS = -no-undefined -avoid-version -module

test_SOURCES = test.cpp
test_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
test_LDADD = \
	$(top_builddir)/src/hed/libs/security/libarcsecurity.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS)

testinterface_arc_SOURCES = testinterface_arc.cpp
testinterface_arc_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
testinterface_arc_LDADD = \
	$(top_builddir)/src/hed/libs/security/libarcsecurity.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS)

testinterface_xacml_SOURCES = testinterface_xacml.cpp
testinterface_xacml_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
testinterface_xacml_LDADD = \
	$(top_builddir)/src/hed/libs/security/libarcsecurity.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS)

#classload_test_SOURCES = classload_test.cpp
#classload_test_CXXFLAGS = -I$(top_srcdir)/include \
#	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
#classload_test_LDADD = \
#	$(top_builddir)/src/hed/libs/security/libarcsecurity.la \
#	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
#	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
#	$(top_builddir)/src/hed/libs/common/libarccommon.la \
#	$(GLIBMM_LIBS) $(LIBXML2_LIBS)
