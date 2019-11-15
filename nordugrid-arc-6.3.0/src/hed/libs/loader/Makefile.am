DIST_SUBDIRS = schema test
SUBDIRS = schema $(TEST_DIR)

lib_LTLIBRARIES = libarcloader.la

libarcloader_ladir = $(pkgincludedir)/loader
libarcloader_la_HEADERS = Plugin.h   Loader.h   ModuleManager.h   FinderLoader.h
libarcloader_la_SOURCES = Plugin.cpp Loader.cpp ModuleManager.cpp FinderLoader.cpp
libarcloader_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libarcloader_la_LIBADD = \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS)
libarcloader_la_LDFLAGS = -version-info 3:0:0

#libtestservice_la_SOURCES = TestService.cpp TestService.h
#libtestservice_la_CXXFLAGS = -I$(top_srcdir)/include \
#	$(LIBXML2_CFLAGS) $(GLIBMM_CFLAGS) $(AM_CXXFLAGS)

#noinst_PROGRAMS = test
#test_SOURCES = test.cpp 
#test_CXXFLAGS = -I$(top_srcdir)/include \
#	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
#test_LDADD = ./libarcloader.la \
#	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
#	$(top_builddir)/src/hed/libs/common/libarccommon.la \
#	$(GLIBMM_LIBS) $(LIBXML2_LIBS)
