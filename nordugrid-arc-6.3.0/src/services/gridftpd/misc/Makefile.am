noinst_LTLIBRARIES = libmisc.la

if LDAP_ENABLED
libmisc_la_SOURCES = \
	ldapquery.cpp proxy.cpp \
	ldapquery.h   proxy.h
else
libmisc_la_SOURCES = \
	proxy.cpp \
	proxy.h
endif

libmisc_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(GLOBUS_GSSAPI_GSI_CFLAGS) $(AM_CXXFLAGS)
libmisc_la_LIBADD = \
	$(top_builddir)/src/hed/libs/credentialstore/libarccredentialstore.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LDAP_LIBS) -lpthread
