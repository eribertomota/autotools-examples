lib_LTLIBRARIES = libarcdata.la
pgmpkglibdir = $(pkglibdir)
pgmpkglib_PROGRAMS = arc-dmc

DIRS = $(TEST_DIR) examples

SUBDIRS = $(DIRS)
DIST_SUBDIRS = test examples
EXTRA_DIST = cache-clean cache-list

pkglibexec_SCRIPTS = cache-clean cache-list

libarcdata_ladir = $(pkgincludedir)/data
libarcdata_la_HEADERS = DataPoint.h DataPointDirect.h \
	DataPointIndex.h DataBuffer.h \
	DataSpeed.h DataMover.h URLMap.h \
	DataCallback.h DataHandle.h FileInfo.h DataStatus.h \
	FileCache.h FileCacheHash.h \
	DataExternalComm.h DataPointDelegate.h
libarcdata_la_SOURCES = DataPoint.cpp DataPointDirect.cpp \
	DataPointIndex.cpp DataBuffer.cpp \
	DataSpeed.cpp DataMover.cpp URLMap.cpp \
	DataStatus.cpp \
	FileCache.cpp FileCacheHash.cpp \
	DataExternalComm.cpp DataPointDelegate.cpp
libarcdata_la_CXXFLAGS = -I$(top_srcdir)/include $(GLIBMM_CFLAGS) \
	$(LIBXML2_CFLAGS) $(GTHREAD_CFLAGS) $(OPENSSL_CFLAGS) $(AM_CXXFLAGS)
libarcdata_la_LIBADD = \
	$(top_builddir)/src/hed/libs/credential/libarccredential.la \
	$(top_builddir)/src/hed/libs/loader/libarcloader.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS) $(GTHREAD_LIBS) \
	$(OPENSSL_LIBS)
libarcdata_la_LDFLAGS = -version-info 3:0:0

arc_dmc_SOURCES = DataExternalHelper.cpp DataExternalHelper.h
arc_dmc_CXXFLAGS = -I$(top_srcdir)/include \
        $(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)
arc_dmc_LDADD = \
        libarcdata.la \
        $(top_builddir)/src/hed/libs/loader/libarcloader.la \
        $(top_builddir)/src/hed/libs/common/libarccommon.la \
        $(LIBXML2_LIBS) $(GLIBMM_LIBS)

man_MANS = cache-clean.1 cache-list.1
