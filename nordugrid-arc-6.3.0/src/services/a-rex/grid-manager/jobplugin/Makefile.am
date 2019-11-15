GLOBUS_JOBPLUGIN_LIBS = $(GLOBUS_RSL_LIBS) $(GLOBUS_IO_LIBS) \
	$(GLOBUS_GSSAPI_GSI_LIBS) $(GLOBUS_GSI_CREDENTIAL_LIBS) \
	$(GLOBUS_GSI_CERT_UTILS_LIBS) $(GLOBUS_COMMON_LIBS)

pkglib_LTLIBRARIES = jobsplugin.la

jobsplugin_la_SOURCES = jobplugin.cpp jobplugin_acl.cpp jobplugin.h init.cpp
jobsplugin_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(DBCXX_CPPFLAGS) \
	$(GLOBUS_FTP_CLIENT_CFLAGS) $(AM_CXXFLAGS)
jobsplugin_la_LDFLAGS = -no-undefined -avoid-version -module

jobsplugin_la_LIBADD = \
	../../../gridftpd/fileplugin/filedirplugin_la-fileplugin.lo \
	../../../gridftpd/libgridftpd_la-userspec.lo \
	../../../gridftpd/libgridftpd_la-names.lo \
	../../../gridftpd/libgridftpd_la-misc.lo \
	../../../gridftpd/auth/libmap.la \
	../conf/libconf.la ../misc/libmisc.la \
	../jobs/libjobs.la ../mail/libmail.la \
	../log/liblog.la ../files/libfiles.la ../run/librun.la \
	../../delegation/libdelegation.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/security/libarcsecurity.la \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(DBCXX_LIBS) $(SQLITE_LIBS) $(GLOBUS_JOBPLUGIN_LIBS) -lpthread
