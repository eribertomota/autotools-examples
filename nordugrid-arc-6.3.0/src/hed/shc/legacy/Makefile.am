SUBDIRS = schema
DIST_SUBDIRS = schema

pkglib_LTLIBRARIES = libarcshclegacy.la

if GLOBUSUTILS_ENABLED
pkglibexec_PROGRAMS = arc-lcas arc-lcmaps
endif

libarcshclegacy_la_SOURCES = auth_file.cpp auth_subject.cpp \
                             auth_plugin.cpp \
                             auth_voms.cpp auth.cpp auth.h \
                             simplemap.cpp simplemap.h \
                             unixmap_lcmaps.cpp unixmap.cpp unixmap.h \
                             ConfigParser.cpp ConfigParser.h \
                             LegacySecAttr.cpp LegacySecAttr.h \
                             LegacySecHandler.cpp LegacySecHandler.h \
                             LegacyPDP.cpp LegacyPDP.h \
                             LegacyMap.cpp LegacyMap.h \
                             plugin.cpp
libarcshclegacy_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libarcshclegacy_la_LIBADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/security/libarcsecurity.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS)
libarcshclegacy_la_LDFLAGS = -no-undefined -avoid-version -module

arc_lcas_SOURCES  = arc_lcas.cpp cert_util.cpp cert_util.h
arc_lcas_CXXFLAGS = -I$(top_srcdir)/include \
        $(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(GTHREAD_CFLAGS) \
        $(OPENSSL_CFLAGS) $(LCAS_CFLAGS) \
        $(GLOBUS_GSSAPI_GSI_CFLAGS) $(GLOBUS_GSI_CREDENTIAL_CFLAGS) \
        $(GLOBUS_GSI_CERT_UTILS_CFLAGS) $(AM_CXXFLAGS)
arc_lcas_LDADD    = \
	$(top_builddir)/src/hed/libs/globusutils/libarcglobusutils.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(OPENSSL_LIBS) \
	$(GLOBUS_COMMON_LIBS) \
	$(GLOBUS_GSSAPI_GSI_LIBS) $(GLOBUS_GSI_CREDENTIAL_LIBS) \
	$(GLOBUS_GSI_CERT_UTILS_LIBS)

arc_lcmaps_SOURCES  = arc_lcmaps.cpp cert_util.cpp cert_util.h
arc_lcmaps_CXXFLAGS = -I$(top_srcdir)/include \
        $(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(GTHREAD_CFLAGS) \
        $(OPENSSL_CFLAGS) $(LCMAPS_CFLAGS) \
        $(GLOBUS_GSSAPI_GSI_CFLAGS) $(GLOBUS_GSI_CREDENTIAL_CFLAGS) \
        $(GLOBUS_GSI_CERT_UTILS_CFLAGS) $(AM_CXXFLAGS)
arc_lcmaps_LDADD    = \
	$(top_builddir)/src/hed/libs/globusutils/libarcglobusutils.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(OPENSSL_LIBS) \
	$(GLOBUS_COMMON_LIBS) \
	$(GLOBUS_GSSAPI_GSI_LIBS) $(GLOBUS_GSI_CREDENTIAL_LIBS) \
	$(GLOBUS_GSI_CERT_UTILS_LIBS)
