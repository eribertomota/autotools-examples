TEST_DIR = test
DIST_SUBDIRS = test schema
SUBDIRS = schema $(TEST_DIR)

lib_LTLIBRARIES = libarcinfosys.la
#noinst_PROGRAMS = test test_cache # test_register

libarcinfosys_ladir = $(pkgincludedir)/infosys
libarcinfosys_la_HEADERS = InformationInterface.h
libarcinfosys_la_SOURCES = InformationInterface.cpp
libarcinfosys_la_CXXFLAGS = -I$(top_srcdir)/include \
	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
libarcinfosys_la_LIBADD = \
	$(top_builddir)/src/hed/libs/communication/libarccommunication.la \
	$(top_builddir)/src/hed/libs/security/libarcsecurity.la \
	$(top_builddir)/src/hed/libs/message/libarcmessage.la \
	$(top_builddir)/src/hed/libs/common/libarccommon.la \
	$(GLIBMM_LIBS) $(LIBXML2_LIBS)

#test_SOURCES = test.cpp
#test_CXXFLAGS = -I$(top_srcdir)/include $(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS)
#test_LDADD = libinfosys.la $(GLIBMM_LIBS) $(LIBXML2_LIBS)

#test_cache_SOURCES = test_cache.cpp
#test_cache_CXXFLAGS = -I$(top_srcdir)/include \
#	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
#test_cache_LDADD = libinfosys.la $(GLIBMM_LIBS) $(LIBXML2_LIBS)

#test_register_SOURCES = test_register.cpp
#test_register_CXXFLAGS = -I$(top_srcdir)/include \
#	$(GLIBMM_CFLAGS) $(LIBXML2_CFLAGS) $(AM_CXXFLAGS)
#test_register_LDADD = libinfosys.la $(GLIBMM_LIBS) $(LIBXML2_LIBS) 
