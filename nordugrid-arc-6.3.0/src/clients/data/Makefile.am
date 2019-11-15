bin_PROGRAMS = arccp arcls arcrm arcmkdir arcrename

man_MANS = arccp.1 arcls.1 arcrm.1 arcmkdir.1 arcrename.1

CLILIBS = \
	$(top_builddir)/src/hed/libs/compute/libarccompute.la \
	$(top_builddir)/src/hed/libs/data/libarcdata.la \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la

arccp_SOURCES  = arccp.cpp
arccp_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
arccp_LDADD    = $(CLILIBS) $(GLIBMM_LIBS)

arcls_SOURCES  = arcls.cpp
arcls_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
arcls_LDADD    = $(CLILIBS) $(GLIBMM_LIBS)

arcrm_SOURCES  = arcrm.cpp
arcrm_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
arcrm_LDADD    = $(CLILIBS) $(GLIBMM_LIBS)

arcmkdir_SOURCES  = arcmkdir.cpp
arcmkdir_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
arcmkdir_LDADD    = $(CLILIBS) $(GLIBMM_LIBS)

arcrename_SOURCES  = arcrename.cpp
arcrename_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
arcrename_LDADD    = $(CLILIBS) $(GLIBMM_LIBS)
