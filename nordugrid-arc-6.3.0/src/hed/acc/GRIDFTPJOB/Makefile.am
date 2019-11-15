pkglib_LTLIBRARIES = libaccGRIDFTPJOB.la

libaccGRIDFTPJOB_la_SOURCES = \
	SubmitterPluginGRIDFTPJOB.cpp SubmitterPluginGRIDFTPJOB.h \
	DescriptorsGRIDFTPJOB.cpp \
	JobControllerPluginGRIDFTPJOB.cpp JobControllerPluginGRIDFTPJOB.h \
	FTPControl.cpp FTPControl.h JobStateGRIDFTPJOB.cpp JobStateGRIDFTPJOB.h
libaccGRIDFTPJOB_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) \
	$(GLOBUS_IO_CFLAGS) $(GLOBUS_FTP_CONTROL_CFLAGS) \
	$(AM_CXXFLAGS)
libaccGRIDFTPJOB_la_LIBADD = \
	$(top_builddir)/src/hed/libs/crypto/libarccrypto.la \
	$(top_builddir)/src/hed/libs/globusutils/libarcglobusutils.la \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS) $(GLOBUS_FTP_CONTROL_LIBS) \
	$(GLOBUS_IO_LIBS) $(GLOBUS_COMMON_LIBS)
libaccGRIDFTPJOB_la_LDFLAGS = -no-undefined -avoid-version -module
