extpkglib_LTLIBRARIES = libdmcxrootd.la
pkglib_LTLIBRARIES = libdmcxrootddeleg.la

libdmcxrootd_la_SOURCES = DataPointXrootd.cpp DataPointXrootd.h
libdmcxrootd_la_CXXFLAGS = -I$(top_srcdir)/include $(XROOTD_CPPFLAGS) \
  $(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
libdmcxrootd_la_LIBADD = \
  $(top_builddir)/src/hed/libs/data/libarcdata.la \
  $(top_builddir)/src/hed/libs/message/libarcmessage.la \
  $(top_builddir)/src/hed/libs/loader/libarcloader.la \
  $(top_builddir)/src/hed/libs/common/libarccommon.la \
  $(LIBXML2_LIBS) $(GLIBMM_LIBS) \
  $(XROOTD_LIBS)
libdmcxrootd_la_LDFLAGS = -no-undefined -avoid-version -module

libdmcxrootddeleg_la_SOURCES = DataPointXrootdDelegate.cpp \
                                DataPointXrootdDelegate.h
libdmcxrootddeleg_la_CXXFLAGS = -I$(top_srcdir)/include \
        $(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
libdmcxrootddeleg_la_LIBADD = \
        $(top_builddir)/src/hed/libs/data/libarcdata.la \
        $(top_builddir)/src/hed/libs/crypto/libarccrypto.la \
        $(top_builddir)/src/hed/libs/loader/libarcloader.la \
        $(top_builddir)/src/hed/libs/common/libarccommon.la \
        $(LIBXML2_LIBS) $(GLIBMM_LIBS)
libdmcxrootddeleg_la_LDFLAGS = -no-undefined -avoid-version -module

