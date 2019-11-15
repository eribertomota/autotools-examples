GLOBUS_FILEPLUGIN_LIBS = $(GLOBUS_RSL_LIBS) $(GLOBUS_IO_LIBS) \
	$(GLOBUS_GSI_CREDENTIAL_LIBS) $(GLOBUS_GSI_CERT_UTILS_LIBS) \
	$(GLOBUS_GSSAPI_GSI_LIBS) $(GLOBUS_COMMON_LIBS)

pkglib_LTLIBRARIES = filedirplugin.la

filedirplugin_la_SOURCES = init.cpp fileplugin.cpp fileplugin.h
filedirplugin_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLOBUS_IO_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
filedirplugin_la_LDFLAGS = -no-undefined -avoid-version -module
filedirplugin_la_LIBADD = \
	../libgridftpd_la-misc.lo ../libgridftpd_la-userspec.lo \
	../libgridftpd_la-names.lo ../auth/libmap.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(GLOBUS_FILEPLUGIN_LIBS)
