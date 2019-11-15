pkglib_LTLIBRARIES = libdmcldap.la

libdmcldap_la_SOURCES = DataPointLDAP.cpp LDAPQuery.cpp \
                        DataPointLDAP.h   LDAPQuery.h
libdmcldap_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)

THR_LIBS = -lpthread

libdmcldap_la_LIBADD = \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS) $(LDAP_LIBS) $(THR_LIBS)
libdmcldap_la_LDFLAGS = -no-undefined -avoid-version -module
