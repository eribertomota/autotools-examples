pgmpkglibdir = $(pkglibdir)

noinst_LTLIBRARIES = libdmcgridftp.la 
pkglib_LTLIBRARIES = libdmcgridftpdeleg.la
pgmpkglib_PROGRAMS = arc-dmcgridftp

libdmcgridftp_la_SOURCES = DataPointGridFTP.cpp Lister.cpp \
                           DataPointGridFTP.h   Lister.h
libdmcgridftp_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(GLOBUS_FTP_CLIENT_CFLAGS) $(AM_CXXFLAGS)
libdmcgridftp_la_LIBADD = \
	$(top_builddir)/src/hed/libs/globusutils/libarcglobusutils.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/crypto/libarccrypto.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS) $(GLOBUS_FTP_CLIENT_LIBS) \
	$(GLOBUS_FTP_CONTROL_LIBS) $(GLOBUS_COMMON_LIBS) $(GLOBUS_IO_LIBS)
libdmcgridftp_la_LDFLAGS = -no-undefined -avoid-version -module

libdmcgridftpdeleg_la_SOURCES = DataPointGridFTPDelegate.cpp \
                                DataPointGridFTPDelegate.h
libdmcgridftpdeleg_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
libdmcgridftpdeleg_la_LIBADD = \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/crypto/libarccrypto.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS)
libdmcgridftpdeleg_la_LDFLAGS = -no-undefined -avoid-version -module

arc_dmcgridftp_SOURCES = DataPointGridFTPHelper.cpp Lister.cpp \
                         DataPointGridFTPHelper.h   Lister.h
arc_dmcgridftp_CXXFLAGS = -I$(top_srcdir)/include \
	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(GLOBUS_FTP_CLIENT_CFLAGS) $(AM_CXXFLAGS)
arc_dmcgridftp_LDADD = \
	$(top_builddir)/src/hed/libs/globusutils/libarcglobusutils.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/crypto/libarccrypto.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(LIBXML2_LIBS) $(GLIBMM_LIBS) $(GLOBUS_FTP_CLIENT_LIBS) \
	$(GLOBUS_FTP_CONTROL_LIBS) $(GLOBUS_COMMON_LIBS) $(GLOBUS_IO_LIBS)

