pkglib_LTLIBRARIES = libaccLDAP.la

libaccLDAP_la_SOURCES  = DescriptorsLDAP.cpp \
	Extractor.h \
	JobListRetrieverPluginLDAPNG.cpp JobListRetrieverPluginLDAPNG.h \
	JobListRetrieverPluginLDAPGLUE2.cpp JobListRetrieverPluginLDAPGLUE2.h \
	TargetInformationRetrieverPluginLDAPNG.cpp TargetInformationRetrieverPluginLDAPNG.h \
	TargetInformationRetrieverPluginLDAPGLUE2.cpp TargetInformationRetrieverPluginLDAPGLUE2.h \
	ServiceEndpointRetrieverPluginEGIIS.cpp ServiceEndpointRetrieverPluginEGIIS.h
libaccLDAP_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
libaccLDAP_la_LIBADD = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS)
libaccLDAP_la_LDFLAGS = -no-undefined -avoid-version -module
