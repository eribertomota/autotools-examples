sbin_PROGRAMS = gridftpd
noinst_LTLIBRARIES = libgridftpd.la

if SYSV_SCRIPTS_ENABLED
GRIDFTPD_SCRIPT = arc-gridftpd
else
GRIDFTPD_SCRIPT =
endif
initd_SCRIPTS = $(GRIDFTPD_SCRIPT)

if SYSTEMD_UNITS_ENABLED
GRIDFTPD_UNIT = arc-gridftpd.service
else
GRIDFTPD_UNIT =
endif
units_DATA = $(GRIDFTPD_UNIT)

pkgdata_SCRIPTS = arc-gridftpd-start

libgridftpd_la_SOURCES = userspec.cpp names.cpp misc.cpp
libgridftpd_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLOBUS_FTP_CLIENT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)

gridftpd_SOURCES = commands.cpp config.cpp fileroot.cpp listener.cpp \
	dataread.cpp datawrite.cpp datalist.cpp fileroot_config.cpp \
	commands.h conf.h fileroot.h misc.h names.h userspec.h

gridftpd_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLOBUS_FTP_CLIENT_CFLAGS) $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)

gridftpd_LDADD = libgridftpd.la conf/libconf.la run/librun.la \
	misc/libmisc.la auth/libauth.la auth/libmap.la \
	$(top_builddir)/src/hed/libs/globusutils/libarcglobusutils.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLOBUS_FTP_CONTROL_LIBS) $(GLOBUS_GSS_ASSIST_LIBS) \
	$(GLOBUS_GSSAPI_GSI_LIBS) $(GLOBUS_IO_LIBS) \
	$(GLOBUS_GSI_CERT_UTILS_LIBS) $(GLOBUS_GSI_CREDENTIAL_LIBS) \
	$(GLOBUS_OPENSSL_MODULE_LIBS) $(GLOBUS_COMMON_LIBS)

gridftpd_LDFLAGS = -rdynamic

SUBDIRS = misc conf run auth . fileplugin

DIST_SUBDIRS = misc conf run auth . fileplugin

man_MANS = gridftpd.8
