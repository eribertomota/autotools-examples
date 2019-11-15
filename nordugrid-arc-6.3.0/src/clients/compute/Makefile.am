bin_PROGRAMS = arcsub arcget arcstat arcinfo arckill arcclean arccat arcsync \
	arcresub arcresume arcrenew arctest

man_MANS = arcsub.1 arcget.1 arcstat.1 arcinfo.1 arckill.1 arcclean.1 arccat.1 \
	arcresub.1 arcsync.1 arcresume.1 arcrenew.1 arctest.1

CLILIBS = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la

arcsub_SOURCES  = arcsub.cpp utils.cpp utils.h
arcsub_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(DBCXX_CPPFLAGS) $(AM_CXXFLAGS)
arcsub_LDADD    = $(CLILIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS) $(DBCXX_LIBS)

arctest_SOURCES  = arctest.cpp utils.cpp utils.h
arctest_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(DBCXX_CPPFLAGS) $(AM_CXXFLAGS)
arctest_LDADD    = $(CLILIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS) $(DBCXX_LIBS)

arcget_SOURCES  = arcget.cpp utils.cpp utils.h
arcget_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(DBCXX_CPPFLAGS) $(AM_CXXFLAGS)
arcget_LDADD    = $(CLILIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS) $(DBCXX_LIBS)

arcstat_SOURCES  = arcstat.cpp utils.cpp utils.h
arcstat_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(DBCXX_CPPFLAGS) $(AM_CXXFLAGS)
arcstat_LDADD    = $(CLILIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS) $(DBCXX_LIBS)

arcinfo_SOURCES  = arcinfo.cpp utils.cpp utils.h
arcinfo_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
arcinfo_LDADD    = $(CLILIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS)

arckill_SOURCES  = arckill.cpp utils.cpp utils.h
arckill_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(DBCXX_CPPFLAGS) $(AM_CXXFLAGS)
arckill_LDADD    = $(CLILIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS) $(DBCXX_LIBS)

arcclean_SOURCES  = arcclean.cpp utils.cpp utils.h
arcclean_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(DBCXX_CPPFLAGS) $(AM_CXXFLAGS)
arcclean_LDADD    = $(CLILIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS) $(DBCXX_LIBS)

arccat_SOURCES  = arccat.cpp utils.cpp utils.h
arccat_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(DBCXX_CPPFLAGS) $(AM_CXXFLAGS)
arccat_LDADD    = $(CLILIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS) $(DBCXX_LIBS)

arcsync_SOURCES  = arcsync.cpp utils.cpp utils.h
arcsync_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(DBCXX_CPPFLAGS) $(AM_CXXFLAGS)
arcsync_LDADD    = $(CLILIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS) $(DBCXX_LIBS)

arcresub_SOURCES  = arcresub.cpp utils.cpp utils.h
arcresub_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(DBCXX_CPPFLAGS) $(AM_CXXFLAGS)
arcresub_LDADD    = $(CLILIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS) $(DBCXX_LIBS)

arcrenew_SOURCES  = arcrenew.cpp utils.cpp utils.h
arcrenew_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(DBCXX_CPPFLAGS) $(AM_CXXFLAGS)
arcrenew_LDADD    = $(CLILIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS) $(DBCXX_LIBS)

arcresume_SOURCES  = arcresume.cpp utils.cpp utils.h
arcresume_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(DBCXX_CPPFLAGS) $(AM_CXXFLAGS)
arcresume_LDADD    = $(CLILIBS) $(GLIBMM_LIBS) $(LIBXML2_LIBS) $(OPENSSL_LIBS) $(DBCXX_LIBS)
